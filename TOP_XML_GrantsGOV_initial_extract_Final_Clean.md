# Grants.gov XML extract, filtered and pushed to MongoDB
 By. Angie Marchany-Rivera & Sara Smithers  
 August 19<sup>th</sup>, 2022

## Executive Summary

The goal of the this project is to provide a tool that allows users to search for environmental remediation grants funded by the Bipartisan Infrastructure Law. This project was completed as part of the Opportunity Project led by the US Census Bureau, The White House OSTP, and the US Department of Commerce. The following code extracts, cleans and filters available grant data from the Grants.gov website. The intial data can then be uploaded to MongoDB, with additional code that can be run daily to check for new grants and updates to grants.

### Extracting the Data from the Grants.gov XML extract


```python
#pip install xmltodict
#pip install pymongo
#pip install pymongo[srv]
```


```python
from io import BytesIO
import ssl
from zipfile import ZipFile
from urllib.request import urlopen
import xmltodict
import os
import pymongo
from pymongo import MongoClient
from pymongo.server_api import ServerApi
import sys
import pandas as pd
import numpy as np
import shutil
```

*Module documentation:* [io](https://docs.python.org/3/library/io.html), [zipfile](https://docs.python.org/3/library/zipfile.html?highlight=zipfile#module-zipfile), 
[urrllib.request](https://docs.python.org/3/library/urllib.request.html), [xmltodict](https://pypi.org/project/xmltodict/), 
[os](https://docs.python.org/3/library/os.html?highlight=os#module-os), [pymongo](https://pypi.org/project/pymongo/), 
[sys](https://docs.python.org/3/library/sys.html?highlight=sys#module-sys), 
[pandas](https://pandas.pydata.org/docs/), [numpy](https://numpy.org/), 
[shutil](https://docs.python.org/3/library/shutil.html?highlight=shutil#module-shutil)


```python
print (sys.version)
```

The Grants.gov database is exported to an XML file everyday by the federal government. The XML file is compressed into a zip file that is named _'GrantsDBExtractYYYYMMDD.zip'_ with the updated date of the extract.  More information about the XML extract can be found here: https://www.grants.gov/help/html/help/index.htm?rhcsh=1&callingApp=custom#t=XMLExtract%2FXMLExtract.htm

## Extract

The following URL format can be used to download the data. To extract the data from the XML file, first use Timestamp function to insert today's date into the the zip file URL. 


```python
# Direct link to updated Grants.gov XML extract. 
# Example link --> https://www.grants.gov/extract/GrantsDBExtract20220813v2.zip

today = pd.Timestamp('today')
link = "https://www.grants.gov/extract/GrantsDBExtract{:%Y%m%d}v2.zip".format(today)
```

A temporary directory is then created where the zip file can be saved, opened, and read. From there, the XML data gets parsed into a dictionary. The grant data is then extracted from the XML dictionary as a list of dictionaries, where each dictionary contains the data for one grant. This list of dictionaries is then converted to a Pandas dataframe to be cleaned.  

The cleaning process includes updating data types and correcting errors. We found errors in the ```ArchiveDate``` column, where the years were listed as _7009_ and _3010_. We assumed this was due to human error and corrected the years to _2009_ and _2010_.


```python
# Extract most up-to-date XML from Grants.gov zip file.
# SLOW STEP - It collects the new XML file in the temp folder.

# Make a temporary directory inside local host working directory.
if not os.path.exists('tempDir'):
    os.makedirs('tempDir')

# Open the link to Grants.gov xml extract zip file.
url = urlopen(link, context = ssl._create_unverified_context())

# Read the zipfile.
zipfile = ZipFile(BytesIO(url.read()))

# Save zipfile to temporary directory.
zipfile.extractall('tempDir/temp')

# Save the file name as a string.
filename = os.listdir('tempDir/temp')

# Read the xml file and save it to xml_data.
with open(os.path.join('tempDir/temp', filename[0]), 'r') as f:
    xml_data = f.read()

# Delete the temporary directory from local host working directory.
shutil.rmtree(f'{os.getcwd()}\\tempDir', ignore_errors = True)
```


```python
# Parse the xml data into a dictionary dtype.

xml_dict = xmltodict.parse(xml_data)
```


```python
# Extract the data from the dictionary. It comes as a list of dictionaries where each dictionary
# stores the data of one grant on Grants.gov.

data_list_dict = xml_dict['Grants']['OpportunitySynopsisDetail_1_0']
```


```python
# Convert the list of dictionaries into a pandas dataframe to perform cleaning.

xml_df = pd.DataFrame(data_list_dict)
```


```python
# Update data types. Numbers = "pd.to_numeric" & dates = "pd.to_datetime":

xml_df['OpportunityID'] = pd.to_numeric(xml_df['OpportunityID'], errors='coerce')
xml_df['AwardCeiling'] = pd.to_numeric(xml_df['AwardCeiling'], errors='coerce')
xml_df['AwardFloor'] = pd.to_numeric(xml_df['AwardFloor'], errors='coerce')
xml_df['EstimatedTotalProgramFunding'] = pd.to_numeric(xml_df['EstimatedTotalProgramFunding'], errors='coerce')
xml_df['ExpectedNumberOfAwards'] = pd.to_numeric(xml_df['ExpectedNumberOfAwards'], errors='coerce')
xml_df['PostDate'] = pd.to_datetime(xml_df['PostDate'], format='%m%d%Y', errors='ignore')
xml_df['CloseDate'] = pd.to_datetime(xml_df['CloseDate'], format='%m%d%Y', errors='ignore')
xml_df['LastUpdatedDate'] = pd.to_datetime(xml_df['LastUpdatedDate'], format='%m%d%Y', errors='ignore')
```


```python
# Found errors on Archive Date - possible cause: human-entered.

xml_df.loc[xml_df['ArchiveDate']=='08157009','ArchiveDate'] = '08152009'
xml_df.loc[xml_df['ArchiveDate']=='03023010','ArchiveDate'] = '03022010'
```


```python
# Update data type for Archive Date after correcting typos:

xml_df['ArchiveDate'] = pd.to_datetime(xml_df['ArchiveDate'], format='%m%d%Y')
```

**Note:** Run the following code if you want to download the cleaned and formatted version of ```xml_df``` into a _csv file_.


```python
# Replace pd.NaT on datetime columns to np.nan for Tableau.

# xml_df['PostDate'].replace({pd.NaT: np.nan}, inplace = True)
# xml_df['CloseDate'].replace({pd.NaT: np.nan}, inplace = True)
# xml_df['LastUpdatedDate'].replace({pd.NaT: np.nan}, inplace = True)
# xml_df['ArchiveDate'].replace({pd.NaT: np.nan}, inplace = True)

# Create CSV for exploratory analysis on Tableau Desktop.

# xml_df[xml_df['ArchiveDate'].dt.year >= 2022].to_csv('grants_active.csv', index = False)
```

## Filtering the data to get all the opportunities listed for environmental remediation in the USA

Now that the Grants.gov extract is in a clean dataframe, it can be filtered for available environmental remediation funding. The dataframe can be filtered by the ```ArchiveDate``` column to remove any funding opportunities that have been archived prior to the current year. The ```CategoryOfFundingActivity``` column can then be filtered to only environment (ENV) funding opportunities. 


```python
# Filter by 'ArchiveDate' >= current year. 
# This will reduce the number of rows since all archived grants will be ignored.

current_year = int(pd.Timestamp('today').strftime('%Y'))
xml_new_df = xml_df[xml_df['ArchiveDate'].dt.year >= current_year]

# Collect all rows that have 'ENV' on the 'CategoryOfFundingActivity' column.
ENV_df = xml_new_df[xml_new_df['CategoryOfFundingActivity'].astype(str).str.contains("ENV", na = False)]
```

There are 8 environmental remediation programs to be funded by the Bipartisan Infrastructure Law (BIL). Three agencies are responsible for funding these programs: the Department of the Interior, the Environmental Protection Agency (EPA), and the Department of Energy (DOE). We created a new dataframe from a dictionary that lists each of the parent agencies and indicated whether the agency has BIL funding available for environmental remediation grants.  

The CFDA number is used to determine the ```parent_agency_number``` on which to join the new dataframe to the filtered environmental grants dataframe (```ENV_df```). The CFDA Number is a unique identifier assigned to each funding opportunity listed on the database (XX.XXX). The first two digits (XX) identify the parent agency number, and the decimals (.XXX) identify each individual program offered by the parent agency.  

A ```parent_agency_number``` was matched to the ```ENV_df['CFDANumbers']``` column and was used to merge the environmental grants dataframe (```ENV_df```) with the agencies reference dataframe (```ENV_Agencies_df```).


```python
# All agencies providing Grants/CA/Loans/Other with the agency CFDA number (2-digit). 
# New columns include 'BIL_ERG_funds', which identifies the 3 agencies 
# that have BIL funding for environmental remediation - Department of Interior, EPA and DOE.

# Create the dictionary, `ENV_Agencies_dict`, using the fromkeys() method.
col_headers = ('parent_agency_number','parent_agency_name', 'BIL_ERG_funds')
ENV_Agencies_dict = dict.fromkeys(col_headers)

# Fill in the parent_agency_number, parent_agency_name, and BIL_ERG_funds.
ENV_Agencies_dict['parent_agency_number'] = ['10','11','15','20','21','59','66','81','93','94','97','98']
ENV_Agencies_dict['parent_agency_name'] = ['Department of Agriculture','Department of Commerce','Department of Interior','Department of Transportation','Department of Treasury','Small Business Administration','Environmental Protection Agency','Department of Energy','Department of Health and Human Services','Corporation for National & Community Service','Department of Homeland Security','United States Agency for International Development']
ENV_Agencies_dict['BIL_ERG_funds'] = ['no','no','yes','no','no','no','yes','yes','no','no','no','no']

#Create a pandas dataframe with the dictionary to be able to merge it with the ENV_df.
ENV_Agencies_df = pd.DataFrame.from_dict(ENV_Agencies_dict, dtype = object)
```


```python
# Create a pattern to search for the parent_agency_number in the ENV_df.

pat = "|".join(ENV_Agencies_df.parent_agency_number)
ENV_df.insert(0, 'parent_agency_number', ENV_df['CFDANumbers'].astype(str).str.extract("(" + pat + ')', expand=False))
```


```python
# Merge the ENV_df (grants data) with the reference table including the parent agencies.

filtered_df = pd.merge(ENV_df,ENV_Agencies_df,on='parent_agency_number')
```


```python
# Replace pd.NaT on datetime columns to 'None' because pd.NaT is not accepted in MongoDB.

filtered_df['PostDate'].replace({pd.NaT: None}, inplace = True)
filtered_df['CloseDate'].replace({pd.NaT: None}, inplace = True)
filtered_df['LastUpdatedDate'].replace({pd.NaT: None}, inplace = True)
filtered_df['ArchiveDate'].replace({pd.NaT: None}, inplace = True)
```


```python
# Create updated dictionary using the 'records’ format : list like [{column -> value}, … , {column -> value}]

updated_dict = filtered_df.to_dict('records')
```

## MongoDB - Project Database

MongoDB was chosen by the Software Engineering leads to host the project database. The following code makes a connection to the Mongo Client, checks the server status, and connects to the _Grants_ collection hosted in the _grantaccess_ database.

### Connecting to MongoDB


```python
# connect to MongoDB - Justin's Project, change the << MONGODB URL >> to reflect your own connection string
# User must input their credentials on the MongoClient link below by replacing <<username>>:<<password>>.

client = pymongo.MongoClient("mongodb+srv://<<username>>:<<password>>@cluster0.mktistr.mongodb.net/?retryWrites=true&w=majority", server_api=ServerApi('1'))
db = client.admin

```


```python
# Check the server status:

serverStatusResult=db.command("serverStatus")
print(serverStatusResult)
```


```python
# Connect to the grantaccess database in MongoDB

db = client.grantaccess
```


```python
# Connect to the "Grants" collection (a.k.a - table)

collection = db["Grants"]
```

### Initial Push

The first upload of the environmental grants into the database was created on 08-13-2022 using the _pymongo_ module.  

**Note:** The code below should be run again only if the original database gets corrupted or deleted.


```python
# Insert a list of dictionaries instead of a pandas df --> https://stackoverflow.com/questions/49221550/pandas-insert-a-dataframe-to-mongodb
# Slow step

#for i in range(1,len(updated_dict)):
    #collection.insert_one(updated_dict[i])
```

### Database Update

Since Grants.gov is continuously updating and/or adding new funding opportunities, the following code is used to update the project database.  

#### How the code works:
- First, call the data in MongoDB (previous version of the database) - comes as a list of dictionaries.  
- Then, compare the old data to the new version of the cleaned and formatted XML extract.    
- If the ```OpportunityID``` number is not in the old database then add the new row of data to the database.  
- If the ```OpportunityID``` number is in the old database and have an updated ```LastUpdatedDate``` then update the row in the database.  
- Else, do nothing.

#### Pymongo functions used:  
new grants identified - ```collection.insert_one()```; updated grants - ```collection.update_one()```


```python
# Bring each document (row of data) stored in MongoDB into python as a dictionary dtype and store it in a list.

old_data_list = []
for old_data in collection.find({}):
    old_data_list.append(old_data)
```


```python
# Creates a dataframe from the list of dictionaries

old_data_df = pd.DataFrame(old_data_list)
```

#### New Grants


```python
# Identify new grants and select only the new grants to be saved as a pd.dataframe.
new_grants_df = filtered_df[~filtered_df['OpportunityID'].isin(old_data_df['OpportunityID'])]

# Create a list of dictionaries, each dictionary is one new record.
new_grants_dict = new_grants_df.to_dict('records')

# Upload each new record to MongoDB.
for new_record in new_grants_dict:
    collection.insert_one(new_record)

```

#### Updated Grants based on ```LastUpdatedDate``` differences


```python
# # Identify updated grants and select only the updated grants to be saved as a pd.dataframe.
updated_grants_df = filtered_df[filtered_df['LastUpdatedDate'].isin(old_data_df['LastUpdatedDate'])== False]

# Create a list of dictionaries, each dictionary is one updated record.
updated_grants_dict = updated_grants_df.to_dict('records')

# Replace each updated record to MongoDB.
for record in updated_grants_dict:
    try:
        record_to_update_dict = [match for match in old_data_list if match['OpportunityID'] == record['OpportunityID']][0]
        collection.update_one({'_id':record_to_update_dict['_id']}, {'$set': record}, upsert = False)
    except: pass
```

### References:

https://www.grants.gov/help/html/help/index.htm#t=Grantors%2FCreateGrantOpportunities.htm  
https://grantsgovprod.wordpress.com/2019/06/05/distinguishing-among-different-types-of-federal-awards-including-block-grants-cooperative-agreements-more/  
https://www.grants.gov/help/html/help/index.htm?rhcsh=1&callingApp=custom#t=XMLExtract%2FXMLExtract.htm  
https://www.grants.gov/xml-extract.html
