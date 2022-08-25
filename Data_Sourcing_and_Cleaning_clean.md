```python
import requests as re
import pandas as pd
import os
import time
```


```python
os.getcwd()
```


```python
os.chdir('set working directory here')
```


```python
ref_file_names = os.listdir('series_id_reference/')
```


```python
ref_file_names
```




    ['series_id_consumption_co_1960_2020 _commercial.csv',
     'series_id_consumption_co_1960_2020_electric_power.csv',
     'series_id_consumption_co_1960_2020_energy_production_nonrenewable.csv',
     'series_id_consumption_co_1960_2020_energy_production_renewable.csv',
     'series_id_consumption_co_1960_2020_GDP_CO.csv',
     'series_id_consumption_co_1960_2020_industrial.csv',
     'series_id_consumption_co_1960_2020_population.csv',
     'series_id_consumption_co_1960_2020_residential.csv']



#### Residential Sector


```python
residential_series_id = pd.read_csv(f'series_id_reference/{ref_file_names[7]}')
```


```python
residential_series_id
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>category</th>
      <th>series_id</th>
      <th>series_id_price</th>
      <th>series_id_expenditures</th>
      <th>notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>All petroleum</td>
      <td>SEDS.PARCB.CO.A</td>
      <td>SEDS.PARCD.CO.A</td>
      <td>SEDS.PARCV.CO.A</td>
      <td>https://www.eia.gov/opendata/v1/qb.php?categor...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Coal</td>
      <td>SEDS.CLRCB.CO.A</td>
      <td>SEDS.CLRCD.CO.A</td>
      <td>SEDS.CLRCV.CO.A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Destillate fuel oil</td>
      <td>SEDS.DFRCB.CO.A</td>
      <td>SEDS.DFRCD.CO.A</td>
      <td>SEDS.DFRCV.CO.A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Electrical system energy losses</td>
      <td>SEDS.LORCB.CO.A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>Billion BTU</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Electricity sales</td>
      <td>SEDS.ESRCB.CO.A</td>
      <td>SEDS.ESRCD.CO.A</td>
      <td>SEDS.ESRCV.CO.A</td>
      <td>Electricity sold to residential sector</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Electricity sales per capita</td>
      <td>SEDS.ESRPP.CO.A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>KWhr</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Geothermal</td>
      <td>SEDS.GERCB.CO.A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Hydrocarbon gas liquids</td>
      <td>SEDS.HLRCB.CO.A</td>
      <td>SEDS.HLRCD.CO.A</td>
      <td>SEDS.HLRCV.CO.A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Kerosene</td>
      <td>SEDS.KSRCB.CO.A</td>
      <td>SEDS.KSRCD.CO.A</td>
      <td>SEDS.KSRCV.CO.A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Natural gas including supplemental gaseous fuels</td>
      <td>SEDS.NGRCB.CO.A</td>
      <td>SEDS.NGRCD.CO.A</td>
      <td>SEDS.NGRCV.CO.A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Propane</td>
      <td>SEDS.PQRCB.CO.A</td>
      <td>SEDS.PQRCD.CO.A</td>
      <td>SEDS.PQRCV.CO.A</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Solar energy</td>
      <td>SEDS.SORCB.CO.A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Total per capita</td>
      <td>SEDS.TERPB.CO.A</td>
      <td>SEDS.TERCD.CO.A</td>
      <td>SEDS.TERCV.CO.A</td>
      <td>Million BTU</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Total energy excluding electrical system energ...</td>
      <td>SEDS.TNRCB.CO.A</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Wood</td>
      <td>SEDS.WDRCB.CO.A</td>
      <td>SEDS.WDRCD.CO.A</td>
      <td>SEDS.WDRCV.CO.A</td>
      <td>Predicted amount https://maps.nrel.gov/slope/d...</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Primary energy</td>
      <td>NaN</td>
      <td>SEDS.PERCD.CO.A</td>
      <td>SEDS.PERCV.CO.A</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
eia_api_key = 'your EIA API key here'
```


```python
# Consumption data for the Residential Sector in Colorado

residential_data_list = []
consumption_id = list(residential_series_id['series_id'])
for i in range(len(consumption_id)):
    try:
        residential_consumption_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={consumption_id[i]}').json()
        residential_consumption_df = pd.DataFrame(residential_consumption_json['series'][0]['data'], columns = ["year","value"])
        residential_consumption_df['series_id'] = pd.Series([residential_consumption_json['series'][0]['series_id'] for x in range(len(residential_consumption_df.index))])
        residential_consumption_df['units'] = pd.Series([residential_consumption_json['series'][0]['units'] for x in range(len(residential_consumption_df.index))])
        residential_data_list.append(residential_consumption_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(consumption_id[i]))
print('Done')    
all_residential_consumption = pd.concat(residential_data_list)    
```

    An error happened: 'series'
    series_id: nan
    Done
    


```python
len(all_residential_consumption.groupby('series_id'))
```




    15




```python
# Price data for the Residential Sector in Colorado
residential_data_list = []
price_id = list(residential_series_id['series_id_price'])
for i in range(len(price_id)):
    try:
        residential_price_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={price_id[i]}').json()
        residential_price_df = pd.DataFrame(residential_price_json['series'][0]['data'], columns = ["year","value"])
        residential_price_df['series_id'] = pd.Series([residential_price_json['series'][0]['series_id'] for x in range(len(residential_price_df.index))])
        residential_price_df['units'] = pd.Series([residential_price_json['series'][0]['units'] for x in range(len(residential_price_df.index))])
        residential_data_list.append(residential_price_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(price_id[i]))
print('Done')    
all_residential_prices = pd.concat(residential_data_list)    
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    


```python
all_residential_prices
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>value</th>
      <th>series_id</th>
      <th>units</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020</td>
      <td>18.24</td>
      <td>SEDS.PARCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019</td>
      <td>20.89</td>
      <td>SEDS.PARCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018</td>
      <td>23.87</td>
      <td>SEDS.PARCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>22.92</td>
      <td>SEDS.PARCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016</td>
      <td>19.68</td>
      <td>SEDS.PARCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>46</th>
      <td>1974</td>
      <td>1.25</td>
      <td>SEDS.PERCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>47</th>
      <td>1973</td>
      <td>1.17</td>
      <td>SEDS.PERCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>48</th>
      <td>1972</td>
      <td>0.93</td>
      <td>SEDS.PERCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>49</th>
      <td>1971</td>
      <td>0.90</td>
      <td>SEDS.PERCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
    <tr>
      <th>50</th>
      <td>1970</td>
      <td>0.88</td>
      <td>SEDS.PERCD.CO.A</td>
      <td>Dollars per million Btu</td>
    </tr>
  </tbody>
</table>
<p>521 rows × 4 columns</p>
</div>




```python
# Expenditures data for the Residential Sector in Colorado

residential_data_list = []
expenditure_id = list(residential_series_id['series_id_expenditures'])
for i in range(len(expenditure_id)):
    try:
        residential_exp_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={expenditure_id[i]}').json()
        residential_exp_df = pd.DataFrame(residential_exp_json['series'][0]['data'], columns = ["year","value"])
        residential_exp_df['series_id'] = pd.Series([residential_exp_json['series'][0]['series_id'] for x in range(len(residential_exp_df.index))])
        residential_exp_df['units'] = pd.Series([residential_exp_json['series'][0]['units'] for x in range(len(residential_exp_df.index))])
        residential_data_list.append(residential_exp_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(expenditure_id[i]))
print('Done')    
all_residential_expenditures = pd.concat(residential_data_list)    
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    


```python
all_residential_expenditures
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>value</th>
      <th>series_id</th>
      <th>units</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020</td>
      <td>222.6</td>
      <td>SEDS.PARCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019</td>
      <td>279.9</td>
      <td>SEDS.PARCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018</td>
      <td>280.8</td>
      <td>SEDS.PARCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>241.2</td>
      <td>SEDS.PARCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016</td>
      <td>219.9</td>
      <td>SEDS.PARCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>46</th>
      <td>1974</td>
      <td>130.4</td>
      <td>SEDS.PERCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>47</th>
      <td>1973</td>
      <td>133.6</td>
      <td>SEDS.PERCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>48</th>
      <td>1972</td>
      <td>100.5</td>
      <td>SEDS.PERCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>49</th>
      <td>1971</td>
      <td>89.7</td>
      <td>SEDS.PERCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
    <tr>
      <th>50</th>
      <td>1970</td>
      <td>85.3</td>
      <td>SEDS.PERCV.CO.A</td>
      <td>Million dollars</td>
    </tr>
  </tbody>
</table>
<p>521 rows × 4 columns</p>
</div>




```python
# 0 = commercial, 1 = Electric power, 5 = industrial
commercial_series_id = pd.read_csv(f'series_id_reference/{ref_file_names[0]}')
electric_power_series_id = pd.read_csv(f'series_id_reference/{ref_file_names[1]}')
industrial_series_id = pd.read_csv(f'series_id_reference/{ref_file_names[5]}')
```

#### Commercial Sector


```python
# Consumption data for the Commercial Sector in Colorado

commercial_data_list = []
consumption_id = list(commercial_series_id['series_id'])
for i in range(len(consumption_id)):
    try:
        commercial_consumption_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={consumption_id[i]}').json()
        commercial_consumption_df = pd.DataFrame(commercial_consumption_json['series'][0]['data'], columns = ["year","value"])
        commercial_consumption_df['series_id'] = pd.Series([commercial_consumption_json['series'][0]['series_id'] for x in range(len(commercial_consumption_df.index))])
        commercial_consumption_df['units'] = pd.Series([commercial_consumption_json['series'][0]['units'] for x in range(len(commercial_consumption_df.index))])
        commercial_data_list.append(commercial_consumption_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(consumption_id[i]))
print('Done')    
all_commercial_consumption = pd.concat(commercial_data_list)    
```

    An error happened: 'series'
    series_id: nan
    Done
    


```python
# Price data for the Commercial Sector in Colorado
commercial_data_list = []
price_id = list(commercial_series_id['series_id_price'])
for i in range(len(price_id)):
    try:
        commercial_price_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={price_id[i]}').json()
        commercial_price_df = pd.DataFrame(commercial_price_json['series'][0]['data'], columns = ["year","value"])
        commercial_price_df['series_id'] = pd.Series([commercial_price_json['series'][0]['series_id'] for x in range(len(commercial_price_df.index))])
        commercial_price_df['units'] = pd.Series([commercial_price_json['series'][0]['units'] for x in range(len(commercial_price_df.index))])
        commercial_data_list.append(commercial_price_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(price_id[i]))
print('Done')    
all_commercial_prices = pd.concat(commercial_data_list)    
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    


```python
# Expenditures data for the Commercial Sector in Colorado

commercial_data_list = []
expenditure_id = list(commercial_series_id['series_id_expenditures'])
for i in range(len(expenditure_id)):
    try:
        commercial_exp_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={expenditure_id[i]}').json()
        commercial_exp_df = pd.DataFrame(commercial_exp_json['series'][0]['data'], columns = ["year","value"])
        commercial_exp_df['series_id'] = pd.Series([commercial_exp_json['series'][0]['series_id'] for x in range(len(commercial_exp_df.index))])
        commercial_exp_df['units'] = pd.Series([commercial_exp_json['series'][0]['units'] for x in range(len(commercial_exp_df.index))])
        commercial_data_list.append(commercial_exp_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(expenditure_id[i]))
print('Done')    
all_commercial_expenditures = pd.concat(commercial_data_list)   
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    

#### Electric Power Sector


```python
# Consumption data for the Electric Power Sector in Colorado

electric_power_data_list = []
consumption_id = list(electric_power_series_id['series_id'])
for i in range(len(consumption_id)):
    try:
        electric_power_consumption_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={consumption_id[i]}').json()
        electric_power_consumption_df = pd.DataFrame(electric_power_consumption_json['series'][0]['data'], columns = ["year","value"])
        electric_power_consumption_df['series_id'] = pd.Series([electric_power_consumption_json['series'][0]['series_id'] for x in range(len(electric_power_consumption_df.index))])
        electric_power_consumption_df['units'] = pd.Series([electric_power_consumption_json['series'][0]['units'] for x in range(len(electric_power_consumption_df.index))])
        electric_power_data_list.append(electric_power_consumption_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(consumption_id[i]))
print('Done')    
all_electric_power_consumption = pd.concat(electric_power_data_list)  
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    


```python
# Price data for the Electric Power Sector in Colorado

electric_power_list = []
price_id = list(electric_power_series_id['series_id_price'])
for i in range(len(price_id)):
    try:
        electric_power_price_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={price_id[i]}').json()
        electric_power_price_df = pd.DataFrame(electric_power_price_json['series'][0]['data'], columns = ["year","value"])
        electric_power_price_df['series_id'] = pd.Series([electric_power_price_json['series'][0]['series_id'] for x in range(len(electric_power_price_df.index))])
        electric_power_price_df['units'] = pd.Series([electric_power_price_json['series'][0]['units'] for x in range(len(electric_power_price_df.index))])
        electric_power_data_list.append(electric_power_price_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(price_id[i]))
print('Done')    
all_electric_power_prices = pd.concat(electric_power_data_list)   
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    


```python
# Expenditures data for the Electric Power Sector in Colorado

electric_power_data_list = []
expenditure_id = list(electric_power_series_id['series_id_expenditures'])
for i in range(len(expenditure_id)):
    try:
        electric_power_exp_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={expenditure_id[i]}').json()
        electric_power_exp_df = pd.DataFrame(electric_power_exp_json['series'][0]['data'], columns = ["year","value"])
        electric_power_exp_df['series_id'] = pd.Series([electric_power_exp_json['series'][0]['series_id'] for x in range(len(electric_power_exp_df.index))])
        electric_power_exp_df['units'] = pd.Series([electric_power_exp_json['series'][0]['units'] for x in range(len(electric_power_exp_df.index))])
        electric_power_data_list.append(electric_power_exp_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(expenditure_id[i]))
print('Done')    
all_electric_power_expenditures = pd.concat(electric_power_data_list)  
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    

#### Industrial Sector


```python
# Consumption data for the Industrial Sector in Colorado

industrial_data_list = []
consumption_id = list(industrial_series_id['series_id'])
for i in range(len(consumption_id)):
    try:
        industrial_consumption_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={consumption_id[i]}').json()
        industrial_consumption_df = pd.DataFrame(industrial_consumption_json['series'][0]['data'], columns = ["year","value"])
        industrial_consumption_df['series_id'] = pd.Series([industrial_consumption_json['series'][0]['series_id'] for x in range(len(industrial_consumption_df.index))])
        industrial_consumption_df['units'] = pd.Series([industrial_consumption_json['series'][0]['units'] for x in range(len(industrial_consumption_df.index))])
        industrial_data_list.append(industrial_consumption_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(consumption_id[i]))
print('Done')    
all_industrial_consumption = pd.concat(industrial_data_list)  
```

    An error happened: 'series'
    series_id: nan
    Done
    


```python
# Price data for the Industrial Sector in Colorado

industrial_list = []
price_id = list(industrial_series_id['series_id_price'])
for i in range(len(price_id)):
    try:
        industrial_price_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={price_id[i]}').json()
        industrial_price_df = pd.DataFrame(industrial_price_json['series'][0]['data'], columns = ["year","value"])
        industrial_price_df['series_id'] = pd.Series([industrial_price_json['series'][0]['series_id'] for x in range(len(industrial_price_df.index))])
        industrial_price_df['units'] = pd.Series([industrial_price_json['series'][0]['units'] for x in range(len(industrial_price_df.index))])
        industrial_data_list.append(industrial_price_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(price_id[i]))
print('Done')    
all_industrial_prices = pd.concat(industrial_data_list)   
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    


```python
# Expenditures data for the Industrial Sector in Colorado

industrial_data_list = []
expenditure_id = list(industrial_series_id['series_id_expenditures'])
for i in range(len(expenditure_id)):
    try:
        industrial_exp_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={expenditure_id[i]}').json()
        industrial_exp_df = pd.DataFrame(industrial_exp_json['series'][0]['data'], columns = ["year","value"])
        industrial_exp_df['series_id'] = pd.Series([commercial_exp_json['series'][0]['series_id'] for x in range(len(industrial_exp_df.index))])
        industrial_exp_df['units'] = pd.Series([industrial_exp_json['series'][0]['units'] for x in range(len(industrial_exp_df.index))])
        industrial_data_list.append(industrial_exp_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(expenditure_id[i]))
print('Done')    
all_industrial_expenditures = pd.concat(industrial_data_list)  
```

    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    An error happened: 'series'
    series_id: nan
    Done
    

#### Energy Production


```python
nonrenewable_series_id = pd.read_csv(f'series_id_reference/{ref_file_names[2]}')
renewable_series_id = pd.read_csv(f'series_id_reference/{ref_file_names[3]}')
```


```python
nonrenewable_series_id['type'] = pd.Series('nonrenewable' for x in range(len(nonrenewable_series_id.index)))
```


```python
renewable_series_id['type'] = pd.Series('renewable' for x in range(len(renewable_series_id.index)))
```


```python
production_series_id = pd.concat([nonrenewable_series_id,renewable_series_id])
```


```python
production_series_id

# Save as a new reference table for energy production
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>category</th>
      <th>series_id</th>
      <th>type</th>
      <th>notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Coal</td>
      <td>SEDS.CLPRB.CO.A</td>
      <td>nonrenewable</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Crude Oil including Lease Condensate</td>
      <td>SEDS.PAPRB.CO.A</td>
      <td>nonrenewable</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Nuclear Power</td>
      <td>SEDS.NUETB.CO.A</td>
      <td>nonrenewable</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Natural Gas Marketed</td>
      <td>SEDS.NGMPB.CO.A</td>
      <td>nonrenewable</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Biodiesel</td>
      <td>SEDS.BDPRP.CO.A</td>
      <td>renewable</td>
      <td>no longer produced in CO</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Biofuels</td>
      <td>SEDS.BFPRP.CO.A</td>
      <td>renewable</td>
      <td>thousand barrels</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Biomass inputs to the Production of Biodiesel</td>
      <td>SEDS.BDFDB.CO.A</td>
      <td>renewable</td>
      <td>BBTU</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Biomass inputs to the Production of Biofuels</td>
      <td>SEDS.BFFDB.CO.A</td>
      <td>renewable</td>
      <td>BBTU</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Biomass inputs to the Production of Fuel Ethanol</td>
      <td>SEDS.EMFDB.CO.A</td>
      <td>renewable</td>
      <td>BBTU</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Fuel Ethanol including Denaturant</td>
      <td>SEDS.ENPRP.CO.A</td>
      <td>renewable</td>
      <td>thousand barrels</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Noncombustible Renewable Energy</td>
      <td>SEDS.NCPRB.CO.A</td>
      <td>renewable</td>
      <td>BBTU</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Wood and Waste Energy</td>
      <td>SEDS.WWPRB.CO.A</td>
      <td>renewable</td>
      <td>BBTU</td>
    </tr>
    <tr>
      <th>8</th>
      <td>All</td>
      <td>SEDS.REPRB.CO.A</td>
      <td>renewable</td>
      <td>BBTU - most produced</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Production data for Colorado

prod_data_list = []
prod_id = list(production_series_id['series_id'])
for i in range(len(prod_id)):
    try:
        prod_json = re.get(f'https://api.eia.gov/series/?api_key={eia_api_key}&series_id={prod_id[i]}').json()
        prod_df = pd.DataFrame(prod_json['series'][0]['data'], columns = ["year","value"])
        prod_df['series_id'] = pd.Series([prod_json['series'][0]['series_id'] for x in range(len(prod_df.index))])
        prod_df['units'] = pd.Series([prod_json['series'][0]['units'] for x in range(len(prod_df.index))])
        prod_data_list.append(prod_df)
        time.sleep(5)
    except Exception as err:
        print('An error happened: ' + str(err))
        print('series_id: ' + str(prod_id[i]))
print('Done')    
all_production = pd.concat(prod_data_list)  
```

    Done
    

### Merging all consumption data


```python
all_industrial_consumption['sector'] =  pd.Series('Industrial' for x in range(len(all_industrial_consumption.index)))
all_residential_consumption['sector'] =  pd.Series('Residential' for x in range(len(all_residential_consumption.index)))
all_commercial_consumption['sector'] =  pd.Series('Commercial' for x in range(len(all_commercial_consumption.index)))
all_electric_power_consumption['sector'] =  pd.Series('Electric Power' for x in range(len(all_electric_power_consumption.index)))
```


```python
all_consumption = pd.concat([all_industrial_consumption,all_residential_consumption,all_commercial_consumption,all_electric_power_consumption]) 
```


```python
all_consumption.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 6201 entries, 0 to 60
    Data columns (total 5 columns):
     #   Column     Non-Null Count  Dtype  
    ---  ------     --------------  -----  
     0   year       6201 non-null   object 
     1   value      6201 non-null   float64
     2   series_id  6201 non-null   object 
     3   units      6201 non-null   object 
     4   sector     6201 non-null   object 
    dtypes: float64(1), object(4)
    memory usage: 290.7+ KB
    


```python
all_consumption['sector'].value_counts()
```




    Industrial        2844
    Commercial        1353
    Electric Power    1139
    Residential        865
    Name: sector, dtype: int64




```python
all_consumption.reset_index(inplace=True, drop=True)
```


```python
all_consumption
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>value</th>
      <th>series_id</th>
      <th>units</th>
      <th>sector</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2020</td>
      <td>66010.0</td>
      <td>SEDS.PAICB.CO.A</td>
      <td>Billion Btu</td>
      <td>Industrial</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2019</td>
      <td>74172.0</td>
      <td>SEDS.PAICB.CO.A</td>
      <td>Billion Btu</td>
      <td>Industrial</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2018</td>
      <td>72867.0</td>
      <td>SEDS.PAICB.CO.A</td>
      <td>Billion Btu</td>
      <td>Industrial</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2017</td>
      <td>62026.0</td>
      <td>SEDS.PAICB.CO.A</td>
      <td>Billion Btu</td>
      <td>Industrial</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016</td>
      <td>60477.0</td>
      <td>SEDS.PAICB.CO.A</td>
      <td>Billion Btu</td>
      <td>Industrial</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>6196</th>
      <td>1964</td>
      <td>0.0</td>
      <td>SEDS.WWEIB.CO.A</td>
      <td>Billion Btu</td>
      <td>Electric Power</td>
    </tr>
    <tr>
      <th>6197</th>
      <td>1963</td>
      <td>0.0</td>
      <td>SEDS.WWEIB.CO.A</td>
      <td>Billion Btu</td>
      <td>Electric Power</td>
    </tr>
    <tr>
      <th>6198</th>
      <td>1962</td>
      <td>0.0</td>
      <td>SEDS.WWEIB.CO.A</td>
      <td>Billion Btu</td>
      <td>Electric Power</td>
    </tr>
    <tr>
      <th>6199</th>
      <td>1961</td>
      <td>0.0</td>
      <td>SEDS.WWEIB.CO.A</td>
      <td>Billion Btu</td>
      <td>Electric Power</td>
    </tr>
    <tr>
      <th>6200</th>
      <td>1960</td>
      <td>0.0</td>
      <td>SEDS.WWEIB.CO.A</td>
      <td>Billion Btu</td>
      <td>Electric Power</td>
    </tr>
  </tbody>
</table>
<p>6201 rows × 5 columns</p>
</div>



### Merging all price data


```python
all_industrial_prices['sector'] =  pd.Series('Industrial' for x in range(len(all_industrial_prices.index)))
all_residential_prices['sector'] =  pd.Series('Residential' for x in range(len(all_residential_prices.index)))
all_commercial_prices['sector'] =  pd.Series('Commercial' for x in range(len(all_commercial_prices.index)))
all_electric_power_prices['sector'] =  pd.Series('Electric Power' for x in range(len(all_electric_power_prices.index)))
```


```python
all_prices = pd.concat([all_industrial_prices,all_residential_prices,all_commercial_prices,all_electric_power_prices]) 
```


```python
all_prices.reset_index(inplace=True, drop=True)
```


```python
all_prices.rename(columns = {'value':'price'},inplace=True)
```


```python
all_prices.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 8577 entries, 0 to 8576
    Data columns (total 5 columns):
     #   Column     Non-Null Count  Dtype  
    ---  ------     --------------  -----  
     0   year       8577 non-null   object 
     1   price      8577 non-null   float64
     2   series_id  8577 non-null   object 
     3   units      8577 non-null   object 
     4   sector     8577 non-null   object 
    dtypes: float64(1), object(4)
    memory usage: 335.2+ KB
    

### Merging all expenditures data


```python
all_industrial_expenditures['sector'] =  pd.Series('Industrial' for x in range(len(all_industrial_expenditures.index)))
all_residential_expenditures['sector'] =  pd.Series('Residential' for x in range(len(all_residential_expenditures.index)))
all_commercial_expenditures['sector'] =  pd.Series('Commercial' for x in range(len(all_commercial_expenditures.index)))
all_electric_power_expenditures['sector'] =  pd.Series('Electric Power' for x in range(len(all_electric_power_expenditures.index)))
```


```python
all_expenditures = pd.concat([all_industrial_expenditures,all_residential_expenditures,all_commercial_expenditures,all_electric_power_expenditures]) 
```


```python
all_expenditures.rename(columns = {'value':'expenditures'},inplace=True)
```


```python
all_expenditures.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 2991 entries, 0 to 50
    Data columns (total 5 columns):
     #   Column        Non-Null Count  Dtype  
    ---  ------        --------------  -----  
     0   year          2991 non-null   object 
     1   expenditures  2991 non-null   float64
     2   series_id     2991 non-null   object 
     3   units         2991 non-null   object 
     4   sector        2991 non-null   object 
    dtypes: float64(1), object(4)
    memory usage: 140.2+ KB
    

#### Monthly Net Generation in Colorado by fuel type


```python
os.chdir('set working directory here')
```


```python
net_gen_co = pd.read_csv(f'Datasets/Colorado_eia_data/Net_generation_Colorado_monthly.csv', skiprows = 4)
```


```python
net_gen_co.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 255 entries, 0 to 254
    Columns: 141 entries, Month to small-scale solar photovoltaic residential thousand megawatthours
    dtypes: float64(140), object(1)
    memory usage: 281.0+ KB
    


```python
net_gen_co['Month'] = pd.to_datetime(net_gen_co['Month'])
```


```python
net_gen_co
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Month</th>
      <th>all fuels (utility-scale) all sectors thousand megawatthours</th>
      <th>coal all sectors thousand megawatthours</th>
      <th>petroleum liquids all sectors thousand megawatthours</th>
      <th>petroleum coke all sectors thousand megawatthours</th>
      <th>natural gas all sectors thousand megawatthours</th>
      <th>other gases all sectors thousand megawatthours</th>
      <th>nuclear all sectors thousand megawatthours</th>
      <th>conventional hydroelectric all sectors thousand megawatthours</th>
      <th>other renewables all sectors thousand megawatthours</th>
      <th>...</th>
      <th>all utility-scale solar residential thousand megawatthours</th>
      <th>utility-scale photovoltaic residential thousand megawatthours</th>
      <th>utility-scale thermal residential thousand megawatthours</th>
      <th>geothermal residential thousand megawatthours</th>
      <th>biomass residential thousand megawatthours</th>
      <th>wood and wood-derived fuels residential thousand megawatthours</th>
      <th>other biomass residential thousand megawatthours</th>
      <th>hydro-electric pumped storage residential thousand megawatthours</th>
      <th>all solar residential thousand megawatthours</th>
      <th>small-scale solar photovoltaic residential thousand megawatthours</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2022-03-01</td>
      <td>4646.07929</td>
      <td>1576.19646</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1105.96774</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>161.76471</td>
      <td>1784.70780</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>81.47904</td>
      <td>81.47904</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2022-02-01</td>
      <td>4399.13319</td>
      <td>1612.65234</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1140.92791</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>152.50619</td>
      <td>1487.51087</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>60.72194</td>
      <td>60.72194</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2022-01-01</td>
      <td>4885.98685</td>
      <td>1992.68550</td>
      <td>1.59244</td>
      <td>NaN</td>
      <td>1151.54503</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>175.74589</td>
      <td>1567.07355</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>58.17301</td>
      <td>58.17301</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2021-12-01</td>
      <td>4907.08425</td>
      <td>1985.03236</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>971.34828</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>155.67654</td>
      <td>1796.64469</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>55.54230</td>
      <td>55.54230</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2021-11-01</td>
      <td>4271.07080</td>
      <td>1675.88665</td>
      <td>1.58557</td>
      <td>NaN</td>
      <td>970.81549</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>110.86623</td>
      <td>1505.34636</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>59.85652</td>
      <td>59.85652</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>250</th>
      <td>2001-05-01</td>
      <td>3975.39600</td>
      <td>3152.66100</td>
      <td>26.57400</td>
      <td>NaN</td>
      <td>640.38100</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>151.59200</td>
      <td>8.37800</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>251</th>
      <td>2001-04-01</td>
      <td>3692.81200</td>
      <td>2689.54300</td>
      <td>31.21300</td>
      <td>NaN</td>
      <td>873.97100</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>95.42500</td>
      <td>7.80800</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>252</th>
      <td>2001-03-01</td>
      <td>3841.54000</td>
      <td>2843.83600</td>
      <td>27.53800</td>
      <td>NaN</td>
      <td>896.10000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>98.21200</td>
      <td>8.10700</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>253</th>
      <td>2001-02-01</td>
      <td>3777.26600</td>
      <td>2881.71600</td>
      <td>23.43000</td>
      <td>NaN</td>
      <td>798.30300</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>86.63000</td>
      <td>7.73200</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>254</th>
      <td>2001-01-01</td>
      <td>4163.45300</td>
      <td>3245.93900</td>
      <td>20.51000</td>
      <td>NaN</td>
      <td>785.00000</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>111.34600</td>
      <td>9.31800</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>255 rows × 141 columns</p>
</div>



#### Loading reference tables for EIA data to be able to join data later on.


```python
ref_tables_file_names = os.listdir()
ref_tables_file_names 
```




    ['consumption_reference_table.csv',
     'eia_all_reference_table.xlsx',
     'expenditures_reference_table.csv',
     'Net_generation_Colorado_monthly.csv',
     'prices_reference_table.csv',
     'series_id_reference']




```python
# use indexes 0 = consumption, 2 = expenditures, 4 = prices

con_ref_df = pd.read_csv(ref_tables_file_names[0])
exp_ref_df = pd.read_csv(ref_tables_file_names[2])
price_ref_df = pd.read_csv(ref_tables_file_names[4])
```


```python
con_ref_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 111 entries, 0 to 110
    Data columns (total 3 columns):
     #   Column        Non-Null Count  Dtype 
    ---  ------        --------------  ----- 
     0   series_id     111 non-null    object
     1   category      111 non-null    object
     2   fuel_type_id  111 non-null    object
    dtypes: object(3)
    memory usage: 2.7+ KB
    


```python
exp_ref_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 61 entries, 0 to 60
    Data columns (total 3 columns):
     #   Column                  Non-Null Count  Dtype 
    ---  ------                  --------------  ----- 
     0   series_id_expenditures  61 non-null     object
     1   category                61 non-null     object
     2   fuel_type_id            61 non-null     object
    dtypes: object(3)
    memory usage: 1.6+ KB
    


```python
price_ref_df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 61 entries, 0 to 60
    Data columns (total 3 columns):
     #   Column           Non-Null Count  Dtype 
    ---  ------           --------------  ----- 
     0   series_id_price  61 non-null     object
     1   category         61 non-null     object
     2   fuel_type_id     61 non-null     object
    dtypes: object(3)
    memory usage: 1.6+ KB
    

### Creating a PostgreSQL Database for the Energy Data


```python
pip install psycopg2
```

    Collecting psycopg2
      Downloading psycopg2-2.9.3-cp39-cp39-win_amd64.whl (1.2 MB)
    Installing collected packages: psycopg2
    Successfully installed psycopg2-2.9.3
    Note: you may need to restart the kernel to use updated packages.
    


```python
import psycopg2
```


```python
pip install sqlalchemy
```

    Requirement already satisfied: sqlalchemy in c:\users\angie\anaconda3\lib\site-packages (1.4.32)
    Requirement already satisfied: greenlet!=0.4.17 in c:\users\angie\anaconda3\lib\site-packages (from sqlalchemy) (1.1.1)
    Note: you may need to restart the kernel to use updated packages.
    


```python
from sqlalchemy import create_engine
```


```python
engine = create_engine('postgresql://<<username>>:<<password>>@localhost:5432/colorado_energy_data')
```


```python
all_consumption.to_sql("all_consumption", engine)
```




    201




```python
all_prices.to_sql("all_prices", engine)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Input In [181], in <cell line: 2>()
          1 engine = create_engine('postgresql://postgres:Rosario$24@localhost:5432/colorado_energy_data')
    ----> 2 all_prices.to_sql("all_prices", engine)
    

    File ~\anaconda3\lib\site-packages\pandas\core\generic.py:2951, in NDFrame.to_sql(self, name, con, schema, if_exists, index, index_label, chunksize, dtype, method)
       2794 """
       2795 Write records stored in a DataFrame to a SQL database.
       2796 
       (...)
       2947 [(1,), (None,), (2,)]
       2948 """  # noqa:E501
       2949 from pandas.io import sql
    -> 2951 return sql.to_sql(
       2952     self,
       2953     name,
       2954     con,
       2955     schema=schema,
       2956     if_exists=if_exists,
       2957     index=index,
       2958     index_label=index_label,
       2959     chunksize=chunksize,
       2960     dtype=dtype,
       2961     method=method,
       2962 )
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:697, in to_sql(frame, name, con, schema, if_exists, index, index_label, chunksize, dtype, method, engine, **engine_kwargs)
        692 elif not isinstance(frame, DataFrame):
        693     raise NotImplementedError(
        694         "'frame' argument should be either a Series or a DataFrame"
        695     )
    --> 697 return pandas_sql.to_sql(
        698     frame,
        699     name,
        700     if_exists=if_exists,
        701     index=index,
        702     index_label=index_label,
        703     schema=schema,
        704     chunksize=chunksize,
        705     dtype=dtype,
        706     method=method,
        707     engine=engine,
        708     **engine_kwargs,
        709 )
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:1729, in SQLDatabase.to_sql(self, frame, name, if_exists, index, index_label, schema, chunksize, dtype, method, engine, **engine_kwargs)
       1679 """
       1680 Write records stored in a DataFrame to a SQL database.
       1681 
       (...)
       1725     Any additional kwargs are passed to the engine.
       1726 """
       1727 sql_engine = get_engine(engine)
    -> 1729 table = self.prep_table(
       1730     frame=frame,
       1731     name=name,
       1732     if_exists=if_exists,
       1733     index=index,
       1734     index_label=index_label,
       1735     schema=schema,
       1736     dtype=dtype,
       1737 )
       1739 total_inserted = sql_engine.insert_records(
       1740     table=table,
       1741     con=self.connectable,
       (...)
       1748     **engine_kwargs,
       1749 )
       1751 self.check_case_sensitive(name=name, schema=schema)
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:1628, in SQLDatabase.prep_table(self, frame, name, if_exists, index, index_label, schema, dtype)
       1616             raise ValueError(f"The type of {col} is not a SQLAlchemy type")
       1618 table = SQLTable(
       1619     name,
       1620     self,
       (...)
       1626     dtype=dtype,
       1627 )
    -> 1628 table.create()
       1629 return table
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:833, in SQLTable.create(self)
        831 if self.exists():
        832     if self.if_exists == "fail":
    --> 833         raise ValueError(f"Table '{self.name}' already exists.")
        834     elif self.if_exists == "replace":
        835         self.pd_sql.drop_table(self.name, self.schema)
    

    ValueError: Table 'all_prices' already exists.



```python
all_expenditures.to_sql("all_expenditures", engine)
```




    991




```python
all_production.to_sql("all_production", engine)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Input In [183], in <cell line: 1>()
    ----> 1 all_production.to_sql("all_production", engine)
    

    File ~\anaconda3\lib\site-packages\pandas\core\generic.py:2951, in NDFrame.to_sql(self, name, con, schema, if_exists, index, index_label, chunksize, dtype, method)
       2794 """
       2795 Write records stored in a DataFrame to a SQL database.
       2796 
       (...)
       2947 [(1,), (None,), (2,)]
       2948 """  # noqa:E501
       2949 from pandas.io import sql
    -> 2951 return sql.to_sql(
       2952     self,
       2953     name,
       2954     con,
       2955     schema=schema,
       2956     if_exists=if_exists,
       2957     index=index,
       2958     index_label=index_label,
       2959     chunksize=chunksize,
       2960     dtype=dtype,
       2961     method=method,
       2962 )
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:697, in to_sql(frame, name, con, schema, if_exists, index, index_label, chunksize, dtype, method, engine, **engine_kwargs)
        692 elif not isinstance(frame, DataFrame):
        693     raise NotImplementedError(
        694         "'frame' argument should be either a Series or a DataFrame"
        695     )
    --> 697 return pandas_sql.to_sql(
        698     frame,
        699     name,
        700     if_exists=if_exists,
        701     index=index,
        702     index_label=index_label,
        703     schema=schema,
        704     chunksize=chunksize,
        705     dtype=dtype,
        706     method=method,
        707     engine=engine,
        708     **engine_kwargs,
        709 )
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:1729, in SQLDatabase.to_sql(self, frame, name, if_exists, index, index_label, schema, chunksize, dtype, method, engine, **engine_kwargs)
       1679 """
       1680 Write records stored in a DataFrame to a SQL database.
       1681 
       (...)
       1725     Any additional kwargs are passed to the engine.
       1726 """
       1727 sql_engine = get_engine(engine)
    -> 1729 table = self.prep_table(
       1730     frame=frame,
       1731     name=name,
       1732     if_exists=if_exists,
       1733     index=index,
       1734     index_label=index_label,
       1735     schema=schema,
       1736     dtype=dtype,
       1737 )
       1739 total_inserted = sql_engine.insert_records(
       1740     table=table,
       1741     con=self.connectable,
       (...)
       1748     **engine_kwargs,
       1749 )
       1751 self.check_case_sensitive(name=name, schema=schema)
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:1628, in SQLDatabase.prep_table(self, frame, name, if_exists, index, index_label, schema, dtype)
       1616             raise ValueError(f"The type of {col} is not a SQLAlchemy type")
       1618 table = SQLTable(
       1619     name,
       1620     self,
       (...)
       1626     dtype=dtype,
       1627 )
    -> 1628 table.create()
       1629 return table
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:833, in SQLTable.create(self)
        831 if self.exists():
        832     if self.if_exists == "fail":
    --> 833         raise ValueError(f"Table '{self.name}' already exists.")
        834     elif self.if_exists == "replace":
        835         self.pd_sql.drop_table(self.name, self.schema)
    

    ValueError: Table 'all_production' already exists.



```python
production_series_id.to_sql("production_reference_table", engine)
```


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    Input In [184], in <cell line: 1>()
    ----> 1 production_series_id.to_sql("production_reference_table", engine)
    

    File ~\anaconda3\lib\site-packages\pandas\core\generic.py:2951, in NDFrame.to_sql(self, name, con, schema, if_exists, index, index_label, chunksize, dtype, method)
       2794 """
       2795 Write records stored in a DataFrame to a SQL database.
       2796 
       (...)
       2947 [(1,), (None,), (2,)]
       2948 """  # noqa:E501
       2949 from pandas.io import sql
    -> 2951 return sql.to_sql(
       2952     self,
       2953     name,
       2954     con,
       2955     schema=schema,
       2956     if_exists=if_exists,
       2957     index=index,
       2958     index_label=index_label,
       2959     chunksize=chunksize,
       2960     dtype=dtype,
       2961     method=method,
       2962 )
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:697, in to_sql(frame, name, con, schema, if_exists, index, index_label, chunksize, dtype, method, engine, **engine_kwargs)
        692 elif not isinstance(frame, DataFrame):
        693     raise NotImplementedError(
        694         "'frame' argument should be either a Series or a DataFrame"
        695     )
    --> 697 return pandas_sql.to_sql(
        698     frame,
        699     name,
        700     if_exists=if_exists,
        701     index=index,
        702     index_label=index_label,
        703     schema=schema,
        704     chunksize=chunksize,
        705     dtype=dtype,
        706     method=method,
        707     engine=engine,
        708     **engine_kwargs,
        709 )
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:1729, in SQLDatabase.to_sql(self, frame, name, if_exists, index, index_label, schema, chunksize, dtype, method, engine, **engine_kwargs)
       1679 """
       1680 Write records stored in a DataFrame to a SQL database.
       1681 
       (...)
       1725     Any additional kwargs are passed to the engine.
       1726 """
       1727 sql_engine = get_engine(engine)
    -> 1729 table = self.prep_table(
       1730     frame=frame,
       1731     name=name,
       1732     if_exists=if_exists,
       1733     index=index,
       1734     index_label=index_label,
       1735     schema=schema,
       1736     dtype=dtype,
       1737 )
       1739 total_inserted = sql_engine.insert_records(
       1740     table=table,
       1741     con=self.connectable,
       (...)
       1748     **engine_kwargs,
       1749 )
       1751 self.check_case_sensitive(name=name, schema=schema)
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:1628, in SQLDatabase.prep_table(self, frame, name, if_exists, index, index_label, schema, dtype)
       1616             raise ValueError(f"The type of {col} is not a SQLAlchemy type")
       1618 table = SQLTable(
       1619     name,
       1620     self,
       (...)
       1626     dtype=dtype,
       1627 )
    -> 1628 table.create()
       1629 return table
    

    File ~\anaconda3\lib\site-packages\pandas\io\sql.py:833, in SQLTable.create(self)
        831 if self.exists():
        832     if self.if_exists == "fail":
    --> 833         raise ValueError(f"Table '{self.name}' already exists.")
        834     elif self.if_exists == "replace":
        835         self.pd_sql.drop_table(self.name, self.schema)
    

    ValueError: Table 'production_reference_table' already exists.



```python
ATBe_2020_scenarios = pd.read_csv('D:/Capstone_Project/Datasets/ATBe.csv')
```


```python
ATBe_2020_scenarios.to_sql("ATBe_2020_scenarios", engine)
```




    604




```python
# Number of plants for Colorado, all sectors from EIA database
plants_co = pd.read_csv(f'{os.getcwd()}/Datasets/List_of_plants_for_Colorado_all_sectors.csv', skiprows = 4)
```


```python
plants_co.to_sql("power_plants_co", engine)
```




    197




```python
net_gen_co.to_sql("net_generation_co", engine)
```




    255




```python
con_ref_df.to_sql("consumption_reference_table", engine)
```




    111




```python
exp_ref_df.to_sql("expenditures_reference_table", engine)
```




    61




```python
price_ref_df.to_sql("price_reference_table", engine)
```




    61



### Census Data for the state of Colorado


```python
os.chdir('set working directory here')
```


```python
census_file_names = os.listdir('Census_data_CO/')
```


```python
print(census_file_names)
len(census_file_names)
```

    ['base-analysis-county.csv', 'components-change-county.csv', 'county-muni-timeseries.csv', 'historical-census.csv', 'household-county.csv', 'jobs-by-sector.csv', 'jobs-county.csv', 'labor-force-county.csv', 'muni-pop-housing.csv', 'profiles-county.csv', 'race-estimates-county.csv', 'race-forecast-county.csv', 'sya-county.csv']
    




    13




```python
jobs_by_county = pd.read_csv(f'Census_data_CO/{census_file_names[6]}')
```


```python
jobs_by_county.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>countyfips</th>
      <th>population_year</th>
      <th>totaljobs</th>
      <th>datatype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>1990</td>
      <td>111337</td>
      <td>ESTIMATE</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>3</td>
      <td>1990</td>
      <td>6385</td>
      <td>ESTIMATE</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>5</td>
      <td>1990</td>
      <td>204957</td>
      <td>ESTIMATE</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>7</td>
      <td>1990</td>
      <td>2371</td>
      <td>ESTIMATE</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>9</td>
      <td>1990</td>
      <td>1929</td>
      <td>ESTIMATE</td>
    </tr>
  </tbody>
</table>
</div>




```python
jobs_by_county.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 3366 entries, 0 to 3365
    Data columns (total 5 columns):
     #   Column           Non-Null Count  Dtype 
    ---  ------           --------------  ----- 
     0   id               3366 non-null   int64 
     1   countyfips       3366 non-null   int64 
     2   population_year  3366 non-null   int64 
     3   totaljobs        3366 non-null   int64 
     4   datatype         3366 non-null   object
    dtypes: int64(4), object(1)
    memory usage: 131.6+ KB
    


```python
jobs_by_county.to_sql("census_jobs_by_county_co", engine)
```




    366




```python
race_estimates = pd.read_csv(f'Census_data_CO/{census_file_names[-3]}')
```


```python
race_estimates.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>county_fips</th>
      <th>race</th>
      <th>ethnicity</th>
      <th>sex</th>
      <th>age</th>
      <th>year</th>
      <th>count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>White</td>
      <td>Not of Hispanic Origin</td>
      <td>M</td>
      <td>0</td>
      <td>2010</td>
      <td>1596.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>White</td>
      <td>Not of Hispanic Origin</td>
      <td>M</td>
      <td>1</td>
      <td>2010</td>
      <td>1570.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>White</td>
      <td>Not of Hispanic Origin</td>
      <td>M</td>
      <td>2</td>
      <td>2010</td>
      <td>1630.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>White</td>
      <td>Not of Hispanic Origin</td>
      <td>M</td>
      <td>3</td>
      <td>2010</td>
      <td>1639.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>1</td>
      <td>White</td>
      <td>Not of Hispanic Origin</td>
      <td>M</td>
      <td>4</td>
      <td>2010</td>
      <td>1620.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
race_estimates.to_sql("census_race_estimates_co", engine)
```




    704




```python
municipality_population = pd.read_csv(f'Census_data_CO/{census_file_names[2]}')
```


```python
municipality_population.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>countyfips</th>
      <th>placefips</th>
      <th>municipalityname</th>
      <th>year</th>
      <th>totalpopulation</th>
      <th>countyplace</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>COLORADO STATE</td>
      <td>1980</td>
      <td>2889735.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>COLORADO STATE</td>
      <td>1981</td>
      <td>2980340.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0</td>
      <td>0</td>
      <td>COLORADO STATE</td>
      <td>1982</td>
      <td>3064868.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0</td>
      <td>0</td>
      <td>COLORADO STATE</td>
      <td>1983</td>
      <td>3137511.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>0</td>
      <td>COLORADO STATE</td>
      <td>1984</td>
      <td>3174844.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
municipality_population['municipalityname'].value_counts()
```




    Unincorp. Area               682
    Broomfield (part)            100
    Littleton (part)              90
    Aurora (part)                 90
    Lochbuie (part)               60
                                ... 
    Mount Crested Butte/G         11
    Manassa                       11
    City of Castle Pines          11
    Windsor (Total)               11
    Broomfield Unincorp. Area     10
    Name: municipalityname, Length: 452, dtype: int64




```python
municipality_population.to_sql("census_municipality_population_co", engine)
```




    604




```python
household = pd.read_csv(f'Census_data_CO/{census_file_names[4]}')
```


```python
household
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>area_code</th>
      <th>year</th>
      <th>household_type_id</th>
      <th>household_type_description</th>
      <th>age_group_id</th>
      <th>age_group_description</th>
      <th>total_households</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>2010</td>
      <td>0</td>
      <td>All Households</td>
      <td>0</td>
      <td>Total</td>
      <td>1.981381e+06</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>0</td>
      <td>2010</td>
      <td>0</td>
      <td>All Households</td>
      <td>1</td>
      <td>18-24</td>
      <td>1.127560e+05</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>0</td>
      <td>2010</td>
      <td>0</td>
      <td>All Households</td>
      <td>2</td>
      <td>25-44</td>
      <td>7.245210e+05</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>0</td>
      <td>2010</td>
      <td>0</td>
      <td>All Households</td>
      <td>3</td>
      <td>45-64</td>
      <td>7.856270e+05</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>2010</td>
      <td>0</td>
      <td>All Households</td>
      <td>4</td>
      <td>65 &amp; Over</td>
      <td>3.584770e+05</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>66620</th>
      <td>66621</td>
      <td>125</td>
      <td>2050</td>
      <td>4</td>
      <td>More than one adult with children</td>
      <td>0</td>
      <td>Total</td>
      <td>8.073906e+02</td>
    </tr>
    <tr>
      <th>66621</th>
      <td>66622</td>
      <td>125</td>
      <td>2050</td>
      <td>4</td>
      <td>More than one adult with children</td>
      <td>1</td>
      <td>18-24</td>
      <td>2.825775e+01</td>
    </tr>
    <tr>
      <th>66622</th>
      <td>66623</td>
      <td>125</td>
      <td>2050</td>
      <td>4</td>
      <td>More than one adult with children</td>
      <td>2</td>
      <td>25-44</td>
      <td>5.194198e+02</td>
    </tr>
    <tr>
      <th>66623</th>
      <td>66624</td>
      <td>125</td>
      <td>2050</td>
      <td>4</td>
      <td>More than one adult with children</td>
      <td>3</td>
      <td>45-64</td>
      <td>2.251926e+02</td>
    </tr>
    <tr>
      <th>66624</th>
      <td>66625</td>
      <td>125</td>
      <td>2050</td>
      <td>4</td>
      <td>More than one adult with children</td>
      <td>4</td>
      <td>65 &amp; Over</td>
      <td>3.452052e+01</td>
    </tr>
  </tbody>
</table>
<p>66625 rows × 8 columns</p>
</div>




```python
household.to_sql("census_household_co", engine)
```




    625




```python
sya = pd.read_csv(f'Census_data_CO/{census_file_names[-1]}')
```


```python
sya
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>id</th>
      <th>countyfips</th>
      <th>year</th>
      <th>age</th>
      <th>county</th>
      <th>malepopulation</th>
      <th>femalepopulation</th>
      <th>totalpopulation</th>
      <th>datatype</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>1</td>
      <td>1990</td>
      <td>0</td>
      <td>Adams</td>
      <td>2354</td>
      <td>2404</td>
      <td>4758</td>
      <td>Estimate</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1990</td>
      <td>1</td>
      <td>Adams</td>
      <td>2345</td>
      <td>2375</td>
      <td>4720</td>
      <td>Estimate</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>1990</td>
      <td>2</td>
      <td>Adams</td>
      <td>2413</td>
      <td>2219</td>
      <td>4632</td>
      <td>Estimate</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1990</td>
      <td>3</td>
      <td>Adams</td>
      <td>2321</td>
      <td>2261</td>
      <td>4582</td>
      <td>Estimate</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>1</td>
      <td>1990</td>
      <td>4</td>
      <td>Adams</td>
      <td>2433</td>
      <td>2302</td>
      <td>4735</td>
      <td>Estimate</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>381499</th>
      <td>668150</td>
      <td>125</td>
      <td>2050</td>
      <td>96</td>
      <td>Yuma</td>
      <td>3</td>
      <td>6</td>
      <td>8</td>
      <td>Forecast</td>
    </tr>
    <tr>
      <th>381500</th>
      <td>668151</td>
      <td>125</td>
      <td>2050</td>
      <td>97</td>
      <td>Yuma</td>
      <td>2</td>
      <td>5</td>
      <td>7</td>
      <td>Forecast</td>
    </tr>
    <tr>
      <th>381501</th>
      <td>668152</td>
      <td>125</td>
      <td>2050</td>
      <td>98</td>
      <td>Yuma</td>
      <td>2</td>
      <td>4</td>
      <td>6</td>
      <td>Forecast</td>
    </tr>
    <tr>
      <th>381502</th>
      <td>668153</td>
      <td>125</td>
      <td>2050</td>
      <td>99</td>
      <td>Yuma</td>
      <td>1</td>
      <td>3</td>
      <td>4</td>
      <td>Forecast</td>
    </tr>
    <tr>
      <th>381503</th>
      <td>668154</td>
      <td>125</td>
      <td>2050</td>
      <td>100</td>
      <td>Yuma</td>
      <td>2</td>
      <td>5</td>
      <td>7</td>
      <td>Forecast</td>
    </tr>
  </tbody>
</table>
<p>381504 rows × 9 columns</p>
</div>




```python
sya.to_sql('census_single_yr_age_co', engine)
```




    504



### Census Data - Poverty and Median Income Estimates - Counties. 

Source: U.S. Census Bureau, Small Area Estimates Branch  


```python
os.chdir('set working directory here')
```


```python
income_file_names = os.listdir('Census_data_Income_US/')
```


```python
income_file_names
```




    ['2003-estimate-layout.txt',
     '2020-estimate-layout.txt',
     'est03all.xls',
     'est04all.xls',
     'est05all.xls',
     'est06all.xls',
     'est07all.xls',
     'est08all.xls',
     'est09all.xls',
     'est10all.xls',
     'est11all.xls',
     'est12all.xls',
     'est13all.xls',
     'est14all.xls',
     'est15all.xls',
     'est16all.xls',
     'est17all.xls',
     'est18all.xls',
     'est19all.xls',
     'est20all.xls']




```python
# Use this from 2003 to 2012
poverty2003_df = pd.read_excel('Census_data_Income_US/est03all.xls', index_col=None, header= 0, usecols = [0,1,2,3,4,7,22]) 
```


```python
poverty2003_df.columns
```




    Index(['State FIPS', 'County FIPS', 'Postal Code', 'Name',
           'Poverty Estimate All Ages', 'Poverty Percent All Ages',
           'Median Household Income'],
          dtype='object')




```python
# Use this from 2013 to 2020
poverty2020_df = pd.read_excel('Census_data_Income_US/est20all.xls', index_col=None, header= 0, skiprows = 3, usecols = [0,1,2,3,4,7,22]) 
```


```python
poverty2020_df.columns
```




    Index(['State FIPS Code', 'County FIPS Code', 'Postal Code', 'Name',
           'Poverty Estimate, All Ages', 'Poverty Percent, All Ages',
           'Median Household Income'],
          dtype='object')



#### Column names are consistent throughout the years


```python
col_names_income = pd.DataFrame([poverty2003_df.columns,poverty2020_df.columns])
```


```python
col_names_income
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>State FIPS</td>
      <td>County FIPS</td>
      <td>Postal Code</td>
      <td>Name</td>
      <td>Poverty Estimate All Ages</td>
      <td>Poverty Percent All Ages</td>
      <td>Median Household Income</td>
    </tr>
    <tr>
      <th>1</th>
      <td>State FIPS Code</td>
      <td>County FIPS Code</td>
      <td>Postal Code</td>
      <td>Name</td>
      <td>Poverty Estimate, All Ages</td>
      <td>Poverty Percent, All Ages</td>
      <td>Median Household Income</td>
    </tr>
  </tbody>
</table>
</div>



#### Read all files from 2003 to 2012


```python
income_data_list = []
years = [0,0,2003,2004,2005,2006,2007,2008,2009,2010,2011,2012]

for i in range(2, 12):
    income_df = pd.read_excel(f'Census_data_Income_US/{income_file_names[i]}', index_col=None, header= 0, usecols = [0,1,2,3,4,7,22]) 
    # Rename the columns so that they are uniform before appending to list
    income_df.columns = poverty2020_df.columns
    income_df['Year'] = pd.Series([years[i] for x in range(len(income_df.index))])
    income_data_list.append(income_df)
    
all_income_2003_2012 = pd.concat(income_data_list)  
    
```


```python
all_income_2003_2012.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 31960 entries, 0 to 3194
    Data columns (total 8 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   State FIPS Code             31953 non-null  object 
     1   County FIPS Code            31939 non-null  float64
     2   Postal Code                 31939 non-null  object 
     3   Name                        31939 non-null  object 
     4   Poverty Estimate, All Ages  31936 non-null  object 
     5   Poverty Percent, All Ages   31936 non-null  object 
     6   Median Household Income     31936 non-null  object 
     7   Year                        31960 non-null  int64  
    dtypes: float64(1), int64(1), object(6)
    memory usage: 2.2+ MB
    


```python
income_data_list = []
years = [2013,2014,2015,2016,2017,2018,2019,2020]

for i in range(-1,-9, -1):
    income_df = pd.read_excel(f'Census_data_Income_US/{income_file_names[i]}', index_col=None, header= 0, skiprows = 3, usecols = [0,1,2,3,4,7,22]) 
    # Rename the columns so that they are uniform before appending to list
    income_df.columns = poverty2020_df.columns
    income_df['Year'] = pd.Series([years[i] for x in range(len(income_df.index))])
    income_data_list.append(income_df)
    
all_income_2013_2020 = pd.concat(income_data_list)  
    
```


```python
all_income_2013_2020.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 25554 entries, 0 to 3194
    Data columns (total 8 columns):
     #   Column                      Non-Null Count  Dtype 
    ---  ------                      --------------  ----- 
     0   State FIPS Code             25554 non-null  int64 
     1   County FIPS Code            25554 non-null  int64 
     2   Postal Code                 25554 non-null  object
     3   Name                        25554 non-null  object
     4   Poverty Estimate, All Ages  25554 non-null  object
     5   Poverty Percent, All Ages   25554 non-null  object
     6   Median Household Income     25554 non-null  object
     7   Year                        25554 non-null  int64 
    dtypes: int64(3), object(5)
    memory usage: 1.8+ MB
    


```python
all_income_2013_2020
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>State FIPS Code</th>
      <th>County FIPS Code</th>
      <th>Postal Code</th>
      <th>Name</th>
      <th>Poverty Estimate, All Ages</th>
      <th>Poverty Percent, All Ages</th>
      <th>Median Household Income</th>
      <th>Year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>0</td>
      <td>US</td>
      <td>United States</td>
      <td>38371394</td>
      <td>11.9</td>
      <td>67340</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>0</td>
      <td>AL</td>
      <td>Alabama</td>
      <td>714568</td>
      <td>14.9</td>
      <td>53958</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>1</td>
      <td>AL</td>
      <td>Autauga County</td>
      <td>6242</td>
      <td>11.2</td>
      <td>67565</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>3</td>
      <td>AL</td>
      <td>Baldwin County</td>
      <td>20189</td>
      <td>8.9</td>
      <td>71135</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>5</td>
      <td>AL</td>
      <td>Barbour County</td>
      <td>5548</td>
      <td>25.5</td>
      <td>38866</td>
      <td>2020</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>3190</th>
      <td>56</td>
      <td>37</td>
      <td>WY</td>
      <td>Sweetwater County</td>
      <td>3850</td>
      <td>8.7</td>
      <td>72899</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>3191</th>
      <td>56</td>
      <td>39</td>
      <td>WY</td>
      <td>Teton County</td>
      <td>1700</td>
      <td>7.7</td>
      <td>70201</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>3192</th>
      <td>56</td>
      <td>41</td>
      <td>WY</td>
      <td>Uinta County</td>
      <td>2515</td>
      <td>12</td>
      <td>60953</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>3193</th>
      <td>56</td>
      <td>43</td>
      <td>WY</td>
      <td>Washakie County</td>
      <td>941</td>
      <td>11.3</td>
      <td>50740</td>
      <td>2013</td>
    </tr>
    <tr>
      <th>3194</th>
      <td>56</td>
      <td>45</td>
      <td>WY</td>
      <td>Weston County</td>
      <td>672</td>
      <td>9.9</td>
      <td>59314</td>
      <td>2013</td>
    </tr>
  </tbody>
</table>
<p>25554 rows × 8 columns</p>
</div>




```python
all_income_2013_2020.sort_values(by = ['Year', 'State FIPS Code', 'County FIPS Code'], inplace = True)
```


```python
all_income = pd.concat([all_income_2003_2012, all_income_2013_2020])
```


```python
all_income.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 57514 entries, 0 to 3194
    Data columns (total 8 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   State FIPS Code             57507 non-null  object 
     1   County FIPS Code            57493 non-null  float64
     2   Postal Code                 57493 non-null  object 
     3   Name                        57493 non-null  object 
     4   Poverty Estimate, All Ages  57490 non-null  object 
     5   Poverty Percent, All Ages   57490 non-null  object 
     6   Median Household Income     57490 non-null  object 
     7   Year                        57514 non-null  int64  
    dtypes: float64(1), int64(1), object(6)
    memory usage: 3.9+ MB
    


```python
all_income.columns = all_income.columns.str.replace(' ','_')
```


```python
index = all_income[all_income['Name'] == 'Kalawao County'].index

all_income.drop(index, axis=0, inplace=True)
```


```python
all_income['Poverty_Estimate,_All_Ages'] = pd.to_numeric(all_income['Poverty_Estimate,_All_Ages'])
```


```python
all_income['Poverty_Percent,_All_Ages'] = pd.to_numeric(all_income['Poverty_Percent,_All_Ages'])
```


```python
all_income['Median_Household_Income'] = pd.to_numeric(all_income['Median_Household_Income'])
```


```python
all_income.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 57442 entries, 0 to 3194
    Data columns (total 8 columns):
     #   Column                      Non-Null Count  Dtype  
    ---  ------                      --------------  -----  
     0   State_FIPS_Code             57435 non-null  object 
     1   County_FIPS_Code            57421 non-null  float64
     2   Postal_Code                 57421 non-null  object 
     3   Name                        57421 non-null  object 
     4   Poverty_Estimate,_All_Ages  57421 non-null  float64
     5   Poverty_Percent,_All_Ages   57421 non-null  float64
     6   Median_Household_Income     57421 non-null  float64
     7   Year                        57442 non-null  int64  
    dtypes: float64(4), int64(1), object(3)
    memory usage: 3.9+ MB
    


```python
all_income.to_sql("all_income_census_us", engine)
```




    442


