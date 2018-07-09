
# WeatherPy

## Analysis
- Maximum temperatures of cities increase as the location goes closer to the equator (0 degrees latitude).
- Wind speed increases for cities located further away from the equator. The highest wind speeds are seen closer to the poles.
- Most cities between 20-40 degrees below and 20-60 degrees above the equator have low cloudiness. 


```python
#call dependencies 
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

import requests
import json
from config import api_key
from citipy import citipy
```


```python
#generate cities list 
#set ranges for latitude and longitude 
lat = (-90, 90)
long = (-180, 180)

#generate random coordinate points
lat = np.random.uniform(low=-90, high=90, size=1500)
long = np.random.uniform(low=-180, high=180, size=1500)

#combine/zip the latitude and longitude list 
lat_long_list = list(zip(lat, long))
#print(lat_long_list)
```

## Generate Cities List


```python
#find corresponding cities to coordinate points 
cities = []

#for loop and append to list 
for point in lat_long_list:
    x = citipy.nearest_city(point[0], point[1]).city_name
    if x not in cities:
        cities.append(x)

#print(cities)
#print(len(cities))
```

## Perform API Calls


```python
url = "http://api.openweathermap.org/data/2.5/weather?units=Imperial&"

#counter 
row_count = 0 
set_count = 1
for city in cities:
    row_count += 1
    if row_count > 50: #create new set for each 50 rows (cities)
        set_count += 1 
        row_count = 1 
    query_url = url + "appid=" + api_key + "&q=" + city
    query_url = query_url.replace(" ", "+")
    print("Processing Record " + str(row_count) + " of Set " + str(set_count) + " | " + city)
    print(query_url)
    
    #create csv output file
    process_str = "Processing Record " + str(row_count) + " of Set " + str(set_count) + " | " + city
    process_url = query_url
    print(process_str + "\n" + process_url, file=open("output.csv", "a"))

```
    EXAMPLE OF PRINT (about 500-600 actual records)
    
    Processing Record 1 of Set 1 | mount gambier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mount+gambier

    
```python
#create lists to hold info
city_name = []
cloudiness = []
country = []
date = []
humidity = []
lat = []
long = []
max_temp = []
wind_speed = []


for city in cities:
    #loop through list to create query url, replace spaces to create working links
    query_url = url + "appid=" + api_key + "&q=" + city
    query_url = query_url.replace(" ", "+")

    #create json file
    response = requests.get(query_url).json()
    #print(json.dumps(weather_json, indent=4, sort_keys=True))

    #append info into lists - will take a few mins to run
    if response["cod"] == 200:
        city_name.append(response["name"])
        cloudiness.append(response["clouds"]["all"])
        country.append(response["sys"]["country"])
        date.append(response["dt"])
        humidity.append(response["main"]["humidity"])
        lat.append(response["coord"]["lat"])
        long.append(response["coord"]["lon"])
        max_temp.append(response["main"]["temp_max"])
        wind_speed.append(response["wind"]["speed"])
    
```


```python
#create dataframe
weather_df = pd.DataFrame({"City": city_name,
                "Cloudiness": cloudiness,
                "Country": country,
                "Date": date,
                "Humidity": humidity,
                "Lat": lat,
                "Lng": long,
                "Max Temp": max_temp,
                "Wind Speed": wind_speed})

weather_df.count()
```




    City          543
    Cloudiness    543
    Country       543
    Date          543
    Humidity      543
    Lat           543
    Lng           543
    Max Temp      543
    Wind Speed    543
    dtype: int64




```python
#print dataframe
weather_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity</th>
      <th>Lat</th>
      <th>Lng</th>
      <th>Max Temp</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Mount Gambier</td>
      <td>64</td>
      <td>AU</td>
      <td>1521482505</td>
      <td>68</td>
      <td>-37.83</td>
      <td>140.78</td>
      <td>57.98</td>
      <td>5.26</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Hithadhoo</td>
      <td>76</td>
      <td>MV</td>
      <td>1521482571</td>
      <td>98</td>
      <td>-0.60</td>
      <td>73.08</td>
      <td>85.43</td>
      <td>12.30</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Qaanaaq</td>
      <td>0</td>
      <td>GL</td>
      <td>1521482572</td>
      <td>86</td>
      <td>77.48</td>
      <td>-69.36</td>
      <td>-14.56</td>
      <td>8.95</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Saint-Philippe</td>
      <td>1</td>
      <td>CA</td>
      <td>1521479700</td>
      <td>44</td>
      <td>45.36</td>
      <td>-73.48</td>
      <td>21.20</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Pevek</td>
      <td>48</td>
      <td>RU</td>
      <td>1521482572</td>
      <td>99</td>
      <td>69.70</td>
      <td>170.27</td>
      <td>-16.72</td>
      <td>7.27</td>
    </tr>
  </tbody>
</table>
</div>



## Latitude vs Temperature Plot


```python
#assign data to x- and y-
city_lat = weather_df["Lat"]
city_temp = weather_df["Max Temp"] 

#charts aesthetics 
fig = plt.figure(figsize=(15,10))
ax = fig.add_subplot(1, 1, 1)

ax.grid(which="major", alpha=0.5)
sns.set_style("darkgrid")

#create scatter plot
plt.scatter(city_lat, city_temp, edgecolor="black", marker="o")

#add labels
plt.title("City Latitude v. Max Temperature", fontsize=20)
plt.xlabel("Latitude", fontsize=16)
plt.ylabel("Max Temperature (F)", fontsize=16)

plt.savefig("LatvTemp.png")
plt.show()
```


![Lat v. Temp](/Images/LatvTemp.png)


## Latitude vs. Humidity Plot


```python
city_hum = weather_df["Humidity"]

#charts aesthetics 
fig = plt.figure(figsize=(15,10))
ax = fig.add_subplot(1, 1, 1)

ax.grid(which="major", alpha=0.5)
sns.set_style("darkgrid")

#create scatter plot
plt.scatter(city_lat, city_hum, edgecolor="black", marker="o")

#add labels
plt.title("City Latitude v. Humidity", fontsize=20)
plt.xlabel("Latitude", fontsize=16)
plt.ylabel("Humidity (%)", fontsize=16)

plt.savefig("LatvHum.png")
plt.show()
```


![Lat v. Hum](/Images/LatvHum.png)


## Latitude vs. Cloudiness Plot


```python
city_cloud = weather_df["Cloudiness"]

#charts aesthetics 
fig = plt.figure(figsize=(15,10))
ax = fig.add_subplot(1, 1, 1)

ax.grid(which="major", alpha=0.5)
sns.set_style("darkgrid")

#create scatter plot
plt.scatter(city_lat, city_cloud, edgecolor="black", marker="o")

#add labels
plt.title("City Latitude v. Cloudiness", fontsize=20)
plt.xlabel("Latitude", fontsize=16)
plt.ylabel("Cloudiness (%)", fontsize=16)

plt.savefig("LatvCloud.png")
plt.show()
```


![Lat v. Cloud](LatvCloud.png)


## Latitude vs. Wind Speed Plot


```python
#latidude v windspeed
city_wind = weather_df["Wind Speed"]

#charts aesthetics 
fig = plt.figure(figsize=(15,10))
ax = fig.add_subplot(1, 1, 1)

ax.grid(which="major", alpha=0.5)
sns.set_style("darkgrid")

#create scatter plot
plt.scatter(city_lat, city_wind, edgecolor="black", marker="o")

#add labels
plt.title("City Latitude v. Wind Speed", fontsize=20)
plt.xlabel("Latitude", fontsize=16)
plt.ylabel("Wind Speed (mph)", fontsize=16)

plt.savefig("LatvWind")
plt.show()
```


![Lat v. Wind](LatvWind.png)

