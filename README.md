
# WeatherPy

Python and the [OpenWeatherMap API](https://openweathermap.org/api) was used to generate random latitude and longitude points that correlate to cities around the world. The Matplotlib and Seaborn libraries were used to visualize the relationship between:
- Temperature (F) vs. Latitude
- Humidity (%) vs. Latitude
- Cloudiness (%) vs. Latitude
- Wind Speed (mph) vs. Latitude

## Analysis
- Maximum temperatures of cities increase as the location goes closer to the equator (0 degrees latitude). Overall, the temperature in the northern hemisphere is warmer at this time of year possibility due to the axis tilt at the time data was collected.
- While there is no obvious correlation between latitude and humidity, there is a visible band at 100% humidity.
- While there is no obvious correlation between latitude and wind speed, most cities at each have wind speeds <15 mph with more clusters located north of the equator.


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
    EXAMPLE OF PRINT STATEMENT (there are about 500-600 actual records)
    ------------------------------------------------------------------------------------------------------------
    Processing Record 1 of Set 1 | pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pisco

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




    City          558
    Cloudiness    558
    Country       558
    Date          558
    Humidity      558
    Lat           558
    Lng           558
    Max Temp      558
    Wind Speed    558
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
      <td>Pisco</td>
      <td>40</td>
      <td>PE</td>
      <td>1531159200</td>
      <td>72</td>
      <td>-13.71</td>
      <td>-76.20</td>
      <td>66.20</td>
      <td>9.17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Ushuaia</td>
      <td>40</td>
      <td>AR</td>
      <td>1531155600</td>
      <td>50</td>
      <td>-54.81</td>
      <td>-68.31</td>
      <td>53.60</td>
      <td>13.87</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Avarua</td>
      <td>75</td>
      <td>CK</td>
      <td>1531159200</td>
      <td>64</td>
      <td>-21.21</td>
      <td>-159.78</td>
      <td>69.80</td>
      <td>10.29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Punta Arenas</td>
      <td>20</td>
      <td>CL</td>
      <td>1531155600</td>
      <td>71</td>
      <td>-53.16</td>
      <td>-70.91</td>
      <td>50.00</td>
      <td>19.46</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Chokurdakh</td>
      <td>80</td>
      <td>RU</td>
      <td>1531160774</td>
      <td>87</td>
      <td>70.62</td>
      <td>147.90</td>
      <td>41.92</td>
      <td>8.97</td>
    </tr>
  </tbody>
</table>
</div>




```python
#save dataframe as csv
weather_df.to_csv("cities.csv")
```

## Temperature v. Latitude Plot


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
plt.title("Max Temperature v. City Latitude", fontsize=20)
plt.xlabel("Latitude", fontsize=16)
plt.ylabel("Max Temperature (F)", fontsize=16)

plt.savefig("TempvLat.png")
plt.show()
```


![Temp v. Lat](/Images/TempvLat.png)


## Humidity v. Latitude Plot


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
plt.title("Humidity v. City Latitude", fontsize=20)
plt.xlabel("Latitude", fontsize=16)
plt.ylabel("Humidity (%)", fontsize=16)

plt.savefig("HumvLat.png")
plt.show()
```


![Hum v. Lat](/Images/HumvLat.png)


## Cloudiness v. Latitude Plot


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
plt.title("Cloudiness v. City Latitude", fontsize=20)
plt.xlabel("Latitude", fontsize=16)
plt.ylabel("Cloudiness (%)", fontsize=16)

plt.savefig("LatvCloud.png")
plt.show()
```


![Cloud v. Lat](/Images/LatvCloud.png)


## Wind Speed v. Latitude Plot


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
plt.title("Wind Speed v. City Latitude", fontsize=20)
plt.xlabel("Latitude", fontsize=16)
plt.ylabel("Wind Speed (mph)", fontsize=16)

plt.savefig("LatvWind")
plt.show()
```


![Wind v. Lat](/Images/LatvWind.png)

