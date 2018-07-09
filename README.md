
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

    Processing Record 1 of Set 1 | pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pisco
    Processing Record 2 of Set 1 | ushuaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ushuaia
    Processing Record 3 of Set 1 | avarua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=avarua
    Processing Record 4 of Set 1 | punta arenas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=punta+arenas
    Processing Record 5 of Set 1 | chokurdakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chokurdakh
    Processing Record 6 of Set 1 | sharjah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sharjah
    Processing Record 7 of Set 1 | rikitea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rikitea
    Processing Record 8 of Set 1 | mataura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mataura
    Processing Record 9 of Set 1 | uni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=uni
    Processing Record 10 of Set 1 | saint-augustin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-augustin
    Processing Record 11 of Set 1 | lingdong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lingdong
    Processing Record 12 of Set 1 | marawi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marawi
    Processing Record 13 of Set 1 | kahului
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kahului
    Processing Record 14 of Set 1 | san ramon de la nueva oran
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+ramon+de+la+nueva+oran
    Processing Record 15 of Set 1 | new norfolk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=new+norfolk
    Processing Record 16 of Set 1 | sinnamary
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sinnamary
    Processing Record 17 of Set 1 | hermanus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hermanus
    Processing Record 18 of Set 1 | illoqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=illoqqortoormiut
    Processing Record 19 of Set 1 | cape town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cape+town
    Processing Record 20 of Set 1 | tasiilaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tasiilaq
    Processing Record 21 of Set 1 | albany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=albany
    Processing Record 22 of Set 1 | japura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=japura
    Processing Record 23 of Set 1 | quimper
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=quimper
    Processing Record 24 of Set 1 | coquimbo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=coquimbo
    Processing Record 25 of Set 1 | grand centre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=grand+centre
    Processing Record 26 of Set 1 | mahebourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mahebourg
    Processing Record 27 of Set 1 | jabiru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jabiru
    Processing Record 28 of Set 1 | dikson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dikson
    Processing Record 29 of Set 1 | nyrob
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nyrob
    Processing Record 30 of Set 1 | sao filipe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sao+filipe
    Processing Record 31 of Set 1 | qaanaaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=qaanaaq
    Processing Record 32 of Set 1 | rurrenabaque
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rurrenabaque
    Processing Record 33 of Set 1 | meulaboh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=meulaboh
    Processing Record 34 of Set 1 | alofi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=alofi
    Processing Record 35 of Set 1 | namibe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=namibe
    Processing Record 36 of Set 1 | monte carmelo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=monte+carmelo
    Processing Record 37 of Set 1 | nikolskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nikolskoye
    Processing Record 38 of Set 1 | saint-francois
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-francois
    Processing Record 39 of Set 1 | vardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vardo
    Processing Record 40 of Set 1 | yellowknife
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yellowknife
    Processing Record 41 of Set 1 | bathsheba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bathsheba
    Processing Record 42 of Set 1 | atuona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atuona
    Processing Record 43 of Set 1 | marsh harbour
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marsh+harbour
    Processing Record 44 of Set 1 | arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=arraial+do+cabo
    Processing Record 45 of Set 1 | caravelas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=caravelas
    Processing Record 46 of Set 1 | bilibino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bilibino
    Processing Record 47 of Set 1 | presidencia roque saenz pena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=presidencia+roque+saenz+pena
    Processing Record 48 of Set 1 | corner brook
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=corner+brook
    Processing Record 49 of Set 1 | manokwari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=manokwari
    Processing Record 50 of Set 1 | nishihara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nishihara
    Processing Record 1 of Set 2 | isiro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=isiro
    Processing Record 2 of Set 2 | rio grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rio+grande
    Processing Record 3 of Set 2 | mount isa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mount+isa
    Processing Record 4 of Set 2 | grand-santi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=grand-santi
    Processing Record 5 of Set 2 | kapaa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kapaa
    Processing Record 6 of Set 2 | provideniya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=provideniya
    Processing Record 7 of Set 2 | eydhafushi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=eydhafushi
    Processing Record 8 of Set 2 | geraldton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=geraldton
    Processing Record 9 of Set 2 | bairiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bairiki
    Processing Record 10 of Set 2 | norman wells
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=norman+wells
    Processing Record 11 of Set 2 | los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=los+llanos+de+aridane
    Processing Record 12 of Set 2 | williams lake
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=williams+lake
    Processing Record 13 of Set 2 | nabire
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nabire
    Processing Record 14 of Set 2 | laguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=laguna
    Processing Record 15 of Set 2 | bambous virieux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bambous+virieux
    Processing Record 16 of Set 2 | hambantota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hambantota
    Processing Record 17 of Set 2 | kodiak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kodiak
    Processing Record 18 of Set 2 | santa cruz de la palma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=santa+cruz+de+la+palma
    Processing Record 19 of Set 2 | phan rang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=phan+rang
    Processing Record 20 of Set 2 | kashi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kashi
    Processing Record 21 of Set 2 | busselton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=busselton
    Processing Record 22 of Set 2 | katherine
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=katherine
    Processing Record 23 of Set 2 | klaksvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=klaksvik
    Processing Record 24 of Set 2 | sitka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sitka
    Processing Record 25 of Set 2 | saskylakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saskylakh
    Processing Record 26 of Set 2 | hobart
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hobart
    Processing Record 27 of Set 2 | gazimurskiy zavod
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gazimurskiy+zavod
    Processing Record 28 of Set 2 | boyolangu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=boyolangu
    Processing Record 29 of Set 2 | matara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=matara
    Processing Record 30 of Set 2 | souillac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=souillac
    Processing Record 31 of Set 2 | asau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=asau
    Processing Record 32 of Set 2 | upernavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=upernavik
    Processing Record 33 of Set 2 | fortuna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fortuna
    Processing Record 34 of Set 2 | korla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=korla
    Processing Record 35 of Set 2 | flinders
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=flinders
    Processing Record 36 of Set 2 | kruisfontein
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kruisfontein
    Processing Record 37 of Set 2 | broken hill
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=broken+hill
    Processing Record 38 of Set 2 | mayo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mayo
    Processing Record 39 of Set 2 | sobolevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sobolevo
    Processing Record 40 of Set 2 | axim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=axim
    Processing Record 41 of Set 2 | tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tuktoyaktuk
    Processing Record 42 of Set 2 | brae
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=brae
    Processing Record 43 of Set 2 | bridlington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bridlington
    Processing Record 44 of Set 2 | bilma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bilma
    Processing Record 45 of Set 2 | vizimyary
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vizimyary
    Processing Record 46 of Set 2 | skala fourkas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=skala+fourkas
    Processing Record 47 of Set 2 | anadyr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=anadyr
    Processing Record 48 of Set 2 | fomboni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fomboni
    Processing Record 49 of Set 2 | tual
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tual
    Processing Record 50 of Set 2 | barentsburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=barentsburg
    Processing Record 1 of Set 3 | amderma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=amderma
    Processing Record 2 of Set 3 | butaritari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=butaritari
    Processing Record 3 of Set 3 | saleaula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saleaula
    Processing Record 4 of Set 3 | boca do acre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=boca+do+acre
    Processing Record 5 of Set 3 | sept-iles
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sept-iles
    Processing Record 6 of Set 3 | lompoc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lompoc
    Processing Record 7 of Set 3 | salalah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=salalah
    Processing Record 8 of Set 3 | warmbad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=warmbad
    Processing Record 9 of Set 3 | yibin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yibin
    Processing Record 10 of Set 3 | oktyabrskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=oktyabrskoye
    Processing Record 11 of Set 3 | aklavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=aklavik
    Processing Record 12 of Set 3 | thompson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=thompson
    Processing Record 13 of Set 3 | aykhal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=aykhal
    Processing Record 14 of Set 3 | santiago del estero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=santiago+del+estero
    Processing Record 15 of Set 3 | rabo de peixe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rabo+de+peixe
    Processing Record 16 of Set 3 | vaini
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vaini
    Processing Record 17 of Set 3 | atasu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atasu
    Processing Record 18 of Set 3 | neepawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=neepawa
    Processing Record 19 of Set 3 | bagdarin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bagdarin
    Processing Record 20 of Set 3 | debre tabor
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=debre+tabor
    Processing Record 21 of Set 3 | bluff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bluff
    Processing Record 22 of Set 3 | correntina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=correntina
    Processing Record 23 of Set 3 | salinopolis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=salinopolis
    Processing Record 24 of Set 3 | cartagena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cartagena
    Processing Record 25 of Set 3 | linxia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=linxia
    Processing Record 26 of Set 3 | khatanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khatanga
    Processing Record 27 of Set 3 | beringovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=beringovskiy
    Processing Record 28 of Set 3 | perevoz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=perevoz
    Processing Record 29 of Set 3 | sao felix do xingu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sao+felix+do+xingu
    Processing Record 30 of Set 3 | labutta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=labutta
    Processing Record 31 of Set 3 | severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=severo-kurilsk
    Processing Record 32 of Set 3 | les cayes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=les+cayes
    Processing Record 33 of Set 3 | grand river south east
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=grand+river+south+east
    Processing Record 34 of Set 3 | puerto baquerizo moreno
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=puerto+baquerizo+moreno
    Processing Record 35 of Set 3 | katsuura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=katsuura
    Processing Record 36 of Set 3 | bredasdorp
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bredasdorp
    Processing Record 37 of Set 3 | eureka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=eureka
    Processing Record 38 of Set 3 | necochea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=necochea
    Processing Record 39 of Set 3 | skeldon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=skeldon
    Processing Record 40 of Set 3 | saint-joseph
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-joseph
    Processing Record 41 of Set 3 | illela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=illela
    Processing Record 42 of Set 3 | usak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=usak
    Processing Record 43 of Set 3 | puerto ayora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=puerto+ayora
    Processing Record 44 of Set 3 | rosarito
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rosarito
    Processing Record 45 of Set 3 | hami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hami
    Processing Record 46 of Set 3 | kokopo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kokopo
    Processing Record 47 of Set 3 | bacolod
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bacolod
    Processing Record 48 of Set 3 | port alfred
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+alfred
    Processing Record 49 of Set 3 | saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-pierre
    Processing Record 50 of Set 3 | maloshuyka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=maloshuyka
    Processing Record 1 of Set 4 | palmer
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=palmer
    Processing Record 2 of Set 4 | barrow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=barrow
    Processing Record 3 of Set 4 | mys shmidta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mys+shmidta
    Processing Record 4 of Set 4 | zhigansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zhigansk
    Processing Record 5 of Set 4 | chilia veche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chilia+veche
    Processing Record 6 of Set 4 | labuhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=labuhan
    Processing Record 7 of Set 4 | sabang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sabang
    Processing Record 8 of Set 4 | hilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hilo
    Processing Record 9 of Set 4 | honiara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=honiara
    Processing Record 10 of Set 4 | qaqortoq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=qaqortoq
    Processing Record 11 of Set 4 | san patricio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+patricio
    Processing Record 12 of Set 4 | saint-leu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-leu
    Processing Record 13 of Set 4 | zeya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zeya
    Processing Record 14 of Set 4 | muravlenko
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=muravlenko
    Processing Record 15 of Set 4 | rocha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rocha
    Processing Record 16 of Set 4 | taltal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taltal
    Processing Record 17 of Set 4 | lufilufi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lufilufi
    Processing Record 18 of Set 4 | lugovoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lugovoy
    Processing Record 19 of Set 4 | touros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=touros
    Processing Record 20 of Set 4 | makakilo city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=makakilo+city
    Processing Record 21 of Set 4 | esil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=esil
    Processing Record 22 of Set 4 | cap-chat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cap-chat
    Processing Record 23 of Set 4 | taolanaro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taolanaro
    Processing Record 24 of Set 4 | buzdyak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=buzdyak
    Processing Record 25 of Set 4 | nome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nome
    Processing Record 26 of Set 4 | muhos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=muhos
    Processing Record 27 of Set 4 | okandja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=okandja
    Processing Record 28 of Set 4 | aleksandrovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=aleksandrovka
    Processing Record 29 of Set 4 | atikokan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atikokan
    Processing Record 30 of Set 4 | jacksonville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jacksonville
    Processing Record 31 of Set 4 | kushiro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kushiro
    Processing Record 32 of Set 4 | marystown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marystown
    Processing Record 33 of Set 4 | sarankhola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sarankhola
    Processing Record 34 of Set 4 | palapye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=palapye
    Processing Record 35 of Set 4 | nouadhibou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nouadhibou
    Processing Record 36 of Set 4 | paamiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=paamiut
    Processing Record 37 of Set 4 | belmonte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=belmonte
    Processing Record 38 of Set 4 | victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=victoria
    Processing Record 39 of Set 4 | bukama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bukama
    Processing Record 40 of Set 4 | haimen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=haimen
    Processing Record 41 of Set 4 | pinotepa nacional
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pinotepa+nacional
    Processing Record 42 of Set 4 | auki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=auki
    Processing Record 43 of Set 4 | tucuman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tucuman
    Processing Record 44 of Set 4 | carnarvon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=carnarvon
    Processing Record 45 of Set 4 | hithadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hithadhoo
    Processing Record 46 of Set 4 | pevek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pevek
    Processing Record 47 of Set 4 | khonsa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khonsa
    Processing Record 48 of Set 4 | jamestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jamestown
    Processing Record 49 of Set 4 | riyadh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=riyadh
    Processing Record 50 of Set 4 | bengkulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bengkulu
    Processing Record 1 of Set 5 | reyes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=reyes
    Processing Record 2 of Set 5 | lebu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lebu
    Processing Record 3 of Set 5 | valparaiso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=valparaiso
    Processing Record 4 of Set 5 | airai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=airai
    Processing Record 5 of Set 5 | dolbeau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dolbeau
    Processing Record 6 of Set 5 | luderitz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=luderitz
    Processing Record 7 of Set 5 | zhuhai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zhuhai
    Processing Record 8 of Set 5 | hamilton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hamilton
    Processing Record 9 of Set 5 | tsihombe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tsihombe
    Processing Record 10 of Set 5 | cherskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cherskiy
    Processing Record 11 of Set 5 | esperance
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=esperance
    Processing Record 12 of Set 5 | carutapera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=carutapera
    Processing Record 13 of Set 5 | henties bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=henties+bay
    Processing Record 14 of Set 5 | san quintin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+quintin
    Processing Record 15 of Set 5 | skiros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=skiros
    Processing Record 16 of Set 5 | cidreira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cidreira
    Processing Record 17 of Set 5 | kaitangata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kaitangata
    Processing Record 18 of Set 5 | mar del plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mar+del+plata
    Processing Record 19 of Set 5 | bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bandarbeyla
    Processing Record 20 of Set 5 | college
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=college
    Processing Record 21 of Set 5 | kamenskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kamenskoye
    Processing Record 22 of Set 5 | sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sao+joao+da+barra
    Processing Record 23 of Set 5 | snezhnogorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=snezhnogorsk
    Processing Record 24 of Set 5 | dunedin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dunedin
    Processing Record 25 of Set 5 | rioja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rioja
    Processing Record 26 of Set 5 | georgetown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=georgetown
    Processing Record 27 of Set 5 | talnakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=talnakh
    Processing Record 28 of Set 5 | attawapiskat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=attawapiskat
    Processing Record 29 of Set 5 | igarka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=igarka
    Processing Record 30 of Set 5 | mawlaik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mawlaik
    Processing Record 31 of Set 5 | opuwo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=opuwo
    Processing Record 32 of Set 5 | udachnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=udachnyy
    Processing Record 33 of Set 5 | puro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=puro
    Processing Record 34 of Set 5 | creston
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=creston
    Processing Record 35 of Set 5 | clyde river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=clyde+river
    Processing Record 36 of Set 5 | wahpeton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=wahpeton
    Processing Record 37 of Set 5 | pacific grove
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pacific+grove
    Processing Record 38 of Set 5 | jagdalpur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jagdalpur
    Processing Record 39 of Set 5 | luwero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=luwero
    Processing Record 40 of Set 5 | kloulklubed
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kloulklubed
    Processing Record 41 of Set 5 | constitucion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=constitucion
    Processing Record 42 of Set 5 | kuching
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kuching
    Processing Record 43 of Set 5 | ambanja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ambanja
    Processing Record 44 of Set 5 | katha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=katha
    Processing Record 45 of Set 5 | conde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=conde
    Processing Record 46 of Set 5 | rafraf
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rafraf
    Processing Record 47 of Set 5 | malbork
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=malbork
    Processing Record 48 of Set 5 | sorland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sorland
    Processing Record 49 of Set 5 | porbandar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=porbandar
    Processing Record 50 of Set 5 | ketchikan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ketchikan
    Processing Record 1 of Set 6 | veraval
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=veraval
    Processing Record 2 of Set 6 | port elizabeth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+elizabeth
    Processing Record 3 of Set 6 | kandi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kandi
    Processing Record 4 of Set 6 | ondjiva
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ondjiva
    Processing Record 5 of Set 6 | saldanha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saldanha
    Processing Record 6 of Set 6 | ponta do sol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ponta+do+sol
    Processing Record 7 of Set 6 | kayerkan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kayerkan
    Processing Record 8 of Set 6 | berlevag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=berlevag
    Processing Record 9 of Set 6 | padang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=padang
    Processing Record 10 of Set 6 | porto novo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=porto+novo
    Processing Record 11 of Set 6 | kyren
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kyren
    Processing Record 12 of Set 6 | bara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bara
    Processing Record 13 of Set 6 | palembang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=palembang
    Processing Record 14 of Set 6 | tubuala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tubuala
    Processing Record 15 of Set 6 | tumannyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tumannyy
    Processing Record 16 of Set 6 | northam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=northam
    Processing Record 17 of Set 6 | reconquista
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=reconquista
    Processing Record 18 of Set 6 | kirakira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kirakira
    Processing Record 19 of Set 6 | adrar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=adrar
    Processing Record 20 of Set 6 | ulladulla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ulladulla
    Processing Record 21 of Set 6 | portland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=portland
    Processing Record 22 of Set 6 | bacuit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bacuit
    Processing Record 23 of Set 6 | maragogi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=maragogi
    Processing Record 24 of Set 6 | anchorage
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=anchorage
    Processing Record 25 of Set 6 | rawah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rawah
    Processing Record 26 of Set 6 | dwarka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dwarka
    Processing Record 27 of Set 6 | gayny
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gayny
    Processing Record 28 of Set 6 | enshi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=enshi
    Processing Record 29 of Set 6 | carauari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=carauari
    Processing Record 30 of Set 6 | chuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chuy
    Processing Record 31 of Set 6 | torrington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=torrington
    Processing Record 32 of Set 6 | mahon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mahon
    Processing Record 33 of Set 6 | vila velha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vila+velha
    Processing Record 34 of Set 6 | verkhnyaya inta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=verkhnyaya+inta
    Processing Record 35 of Set 6 | nantucket
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nantucket
    Processing Record 36 of Set 6 | xirokambion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=xirokambion
    Processing Record 37 of Set 6 | mareeba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mareeba
    Processing Record 38 of Set 6 | illapel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=illapel
    Processing Record 39 of Set 6 | acarau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=acarau
    Processing Record 40 of Set 6 | guerrero negro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=guerrero+negro
    Processing Record 41 of Set 6 | palu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=palu
    Processing Record 42 of Set 6 | vao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vao
    Processing Record 43 of Set 6 | odienne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=odienne
    Processing Record 44 of Set 6 | prado
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=prado
    Processing Record 45 of Set 6 | ilulissat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ilulissat
    Processing Record 46 of Set 6 | kuche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kuche
    Processing Record 47 of Set 6 | morant bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=morant+bay
    Processing Record 48 of Set 6 | yambio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yambio
    Processing Record 49 of Set 6 | wamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=wamba
    Processing Record 50 of Set 6 | kambove
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kambove
    Processing Record 1 of Set 7 | ust-omchug
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ust-omchug
    Processing Record 2 of Set 7 | ksenyevka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ksenyevka
    Processing Record 3 of Set 7 | taoudenni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taoudenni
    Processing Record 4 of Set 7 | kilindoni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kilindoni
    Processing Record 5 of Set 7 | saint-philippe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-philippe
    Processing Record 6 of Set 7 | flin flon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=flin+flon
    Processing Record 7 of Set 7 | longlac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=longlac
    Processing Record 8 of Set 7 | sibolga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sibolga
    Processing Record 9 of Set 7 | zhezkazgan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zhezkazgan
    Processing Record 10 of Set 7 | marcona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marcona
    Processing Record 11 of Set 7 | moose factory
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=moose+factory
    Processing Record 12 of Set 7 | tessalit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tessalit
    Processing Record 13 of Set 7 | sakaiminato
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sakaiminato
    Processing Record 14 of Set 7 | bontang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bontang
    Processing Record 15 of Set 7 | vaitupu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vaitupu
    Processing Record 16 of Set 7 | tiksi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tiksi
    Processing Record 17 of Set 7 | marijampole
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marijampole
    Processing Record 18 of Set 7 | faanui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=faanui
    Processing Record 19 of Set 7 | frejus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=frejus
    Processing Record 20 of Set 7 | castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=castro
    Processing Record 21 of Set 7 | ambodifototra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ambodifototra
    Processing Record 22 of Set 7 | estevan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=estevan
    Processing Record 23 of Set 7 | mumford
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mumford
    Processing Record 24 of Set 7 | mangan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mangan
    Processing Record 25 of Set 7 | moanda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=moanda
    Processing Record 26 of Set 7 | stanghelle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=stanghelle
    Processing Record 27 of Set 7 | tecoanapa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tecoanapa
    Processing Record 28 of Set 7 | khakhea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khakhea
    Processing Record 29 of Set 7 | nguiu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nguiu
    Processing Record 30 of Set 7 | margate
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=margate
    Processing Record 31 of Set 7 | salisbury
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=salisbury
    Processing Record 32 of Set 7 | vila franca do campo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vila+franca+do+campo
    Processing Record 33 of Set 7 | gambela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gambela
    Processing Record 34 of Set 7 | catuday
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=catuday
    Processing Record 35 of Set 7 | port moresby
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+moresby
    Processing Record 36 of Set 7 | ribeira grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ribeira+grande
    Processing Record 37 of Set 7 | abilene
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=abilene
    Processing Record 38 of Set 7 | kieta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kieta
    Processing Record 39 of Set 7 | shenjiamen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=shenjiamen
    Processing Record 40 of Set 7 | luau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=luau
    Processing Record 41 of Set 7 | mackay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mackay
    Processing Record 42 of Set 7 | chernyshevskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chernyshevskiy
    Processing Record 43 of Set 7 | lorengau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lorengau
    Processing Record 44 of Set 7 | ginda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ginda
    Processing Record 45 of Set 7 | leningradskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=leningradskiy
    Processing Record 46 of Set 7 | manta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=manta
    Processing Record 47 of Set 7 | east london
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=east+london
    Processing Record 48 of Set 7 | opatija
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=opatija
    Processing Record 49 of Set 7 | imbituba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=imbituba
    Processing Record 50 of Set 7 | cam ranh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cam+ranh
    Processing Record 1 of Set 8 | sur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sur
    Processing Record 2 of Set 8 | sainte-marie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sainte-marie
    Processing Record 3 of Set 8 | vanimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vanimo
    Processing Record 4 of Set 8 | florianopolis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=florianopolis
    Processing Record 5 of Set 8 | chunoyar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chunoyar
    Processing Record 6 of Set 8 | itacoatiara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=itacoatiara
    Processing Record 7 of Set 8 | namatanai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=namatanai
    Processing Record 8 of Set 8 | le vauclin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=le+vauclin
    Processing Record 9 of Set 8 | chisinau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chisinau
    Processing Record 10 of Set 8 | kununurra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kununurra
    Processing Record 11 of Set 8 | inderborskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=inderborskiy
    Processing Record 12 of Set 8 | suluq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=suluq
    Processing Record 13 of Set 8 | bulaevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bulaevo
    Processing Record 14 of Set 8 | sakakah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sakakah
    Processing Record 15 of Set 8 | vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vestmannaeyjar
    Processing Record 16 of Set 8 | warqla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=warqla
    Processing Record 17 of Set 8 | sidi ali
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sidi+ali
    Processing Record 18 of Set 8 | abu samrah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=abu+samrah
    Processing Record 19 of Set 8 | placido de castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=placido+de+castro
    Processing Record 20 of Set 8 | port hardy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+hardy
    Processing Record 21 of Set 8 | catamarca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=catamarca
    Processing Record 22 of Set 8 | alice springs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=alice+springs
    Processing Record 23 of Set 8 | meadow lake
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=meadow+lake
    Processing Record 24 of Set 8 | macaboboni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=macaboboni
    Processing Record 25 of Set 8 | khormuj
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khormuj
    Processing Record 26 of Set 8 | pointe-noire
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pointe-noire
    Processing Record 27 of Set 8 | lasa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lasa
    Processing Record 28 of Set 8 | nouakchott
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nouakchott
    Processing Record 29 of Set 8 | mogadishu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mogadishu
    Processing Record 30 of Set 8 | fairbanks
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fairbanks
    Processing Record 31 of Set 8 | sistranda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sistranda
    Processing Record 32 of Set 8 | bell ville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bell+ville
    Processing Record 33 of Set 8 | morondava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=morondava
    Processing Record 34 of Set 8 | burica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=burica
    Processing Record 35 of Set 8 | teya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=teya
    Processing Record 36 of Set 8 | kokstad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kokstad
    Processing Record 37 of Set 8 | druzhba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=druzhba
    Processing Record 38 of Set 8 | kochevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kochevo
    Processing Record 39 of Set 8 | bend
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bend
    Processing Record 40 of Set 8 | along
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=along
    Processing Record 41 of Set 8 | gat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gat
    Processing Record 42 of Set 8 | teguise
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=teguise
    Processing Record 43 of Set 8 | vostok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vostok
    Processing Record 44 of Set 8 | ulaangom
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ulaangom
    Processing Record 45 of Set 8 | quelimane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=quelimane
    Processing Record 46 of Set 8 | port-cartier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port-cartier
    Processing Record 47 of Set 8 | krasnyy chikoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=krasnyy+chikoy
    Processing Record 48 of Set 8 | almaznyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=almaznyy
    Processing Record 49 of Set 8 | sioux lookout
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sioux+lookout
    Processing Record 50 of Set 8 | ajaccio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ajaccio
    Processing Record 1 of Set 9 | simbahan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=simbahan
    Processing Record 2 of Set 9 | te anau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=te+anau
    Processing Record 3 of Set 9 | longyearbyen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=longyearbyen
    Processing Record 4 of Set 9 | port lincoln
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+lincoln
    Processing Record 5 of Set 9 | hovd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hovd
    Processing Record 6 of Set 9 | pochutla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pochutla
    Processing Record 7 of Set 9 | kutum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kutum
    Processing Record 8 of Set 9 | bose
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bose
    Processing Record 9 of Set 9 | waipawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=waipawa
    Processing Record 10 of Set 9 | gushikawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gushikawa
    Processing Record 11 of Set 9 | kenai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kenai
    Processing Record 12 of Set 9 | agua verde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=agua+verde
    Processing Record 13 of Set 9 | verkhnetulomskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=verkhnetulomskiy
    Processing Record 14 of Set 9 | sao francisco de paula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sao+francisco+de+paula
    Processing Record 15 of Set 9 | hailar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hailar
    Processing Record 16 of Set 9 | bereda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bereda
    Processing Record 17 of Set 9 | outjo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=outjo
    Processing Record 18 of Set 9 | fukue
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fukue
    Processing Record 19 of Set 9 | ola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ola
    Processing Record 20 of Set 9 | boysun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=boysun
    Processing Record 21 of Set 9 | samusu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=samusu
    Processing Record 22 of Set 9 | kaniama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kaniama
    Processing Record 23 of Set 9 | san ignacio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+ignacio
    Processing Record 24 of Set 9 | narsaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=narsaq
    Processing Record 25 of Set 9 | walvis bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=walvis+bay
    Processing Record 26 of Set 9 | manikganj
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=manikganj
    Processing Record 27 of Set 9 | kamina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kamina
    Processing Record 28 of Set 9 | clones
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=clones
    Processing Record 29 of Set 9 | bocaranga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bocaranga
    Processing Record 30 of Set 9 | hunza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hunza
    Processing Record 31 of Set 9 | ust-maya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ust-maya
    Processing Record 32 of Set 9 | roma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=roma
    Processing Record 33 of Set 9 | naze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=naze
    Processing Record 34 of Set 9 | belushya guba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=belushya+guba
    Processing Record 35 of Set 9 | dapitan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dapitan
    Processing Record 36 of Set 9 | jardim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jardim
    Processing Record 37 of Set 9 | cayenne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cayenne
    Processing Record 38 of Set 9 | xuanhua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=xuanhua
    Processing Record 39 of Set 9 | guozhen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=guozhen
    Processing Record 40 of Set 9 | la orilla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=la+orilla
    Processing Record 41 of Set 9 | utiroa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=utiroa
    Processing Record 42 of Set 9 | ust-nera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ust-nera
    Processing Record 43 of Set 9 | yichun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yichun
    Processing Record 44 of Set 9 | vila do maio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vila+do+maio
    Processing Record 45 of Set 9 | ballina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ballina
    Processing Record 46 of Set 9 | husavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=husavik
    Processing Record 47 of Set 9 | kontagora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kontagora
    Processing Record 48 of Set 9 | khandbari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khandbari
    Processing Record 49 of Set 9 | huainan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=huainan
    Processing Record 50 of Set 9 | esqueda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=esqueda
    Processing Record 1 of Set 10 | sentyabrskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sentyabrskiy
    Processing Record 2 of Set 10 | andenes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=andenes
    Processing Record 3 of Set 10 | rawannawi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rawannawi
    Processing Record 4 of Set 10 | maceio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=maceio
    Processing Record 5 of Set 10 | suruc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=suruc
    Processing Record 6 of Set 10 | cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cabo+san+lucas
    Processing Record 7 of Set 10 | pangnirtung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pangnirtung
    Processing Record 8 of Set 10 | manyana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=manyana
    Processing Record 9 of Set 10 | bougouni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bougouni
    Processing Record 10 of Set 10 | oranjemund
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=oranjemund
    Processing Record 11 of Set 10 | sokoni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sokoni
    Processing Record 12 of Set 10 | port blair
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+blair
    Processing Record 13 of Set 10 | diego de almagro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=diego+de+almagro
    Processing Record 14 of Set 10 | myitkyina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=myitkyina
    Processing Record 15 of Set 10 | amarante do maranhao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=amarante+do+maranhao
    Processing Record 16 of Set 10 | iqaluit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=iqaluit
    Processing Record 17 of Set 10 | ayan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ayan
    Processing Record 18 of Set 10 | bonthe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bonthe
    Processing Record 19 of Set 10 | kensington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kensington
    Processing Record 20 of Set 10 | hokitika
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hokitika
    Processing Record 21 of Set 10 | otane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=otane
    Processing Record 22 of Set 10 | selikhino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=selikhino
    Processing Record 23 of Set 10 | olafsvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=olafsvik
    Processing Record 24 of Set 10 | jutai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jutai
    Processing Record 25 of Set 10 | monte cristi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=monte+cristi
    Processing Record 26 of Set 10 | santa cruz cabralia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=santa+cruz+cabralia
    Processing Record 27 of Set 10 | ahipara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ahipara
    Processing Record 28 of Set 10 | deputatskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=deputatskiy
    Processing Record 29 of Set 10 | hofn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hofn
    Processing Record 30 of Set 10 | pakruojis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pakruojis
    Processing Record 31 of Set 10 | gavrilovka vtoraya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gavrilovka+vtoraya
    Processing Record 32 of Set 10 | ortigueira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ortigueira
    Processing Record 33 of Set 10 | maxixe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=maxixe
    Processing Record 34 of Set 10 | bakchar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bakchar
    Processing Record 35 of Set 10 | moa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=moa
    Processing Record 36 of Set 10 | port augusta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+augusta
    Processing Record 37 of Set 10 | fenoarivo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fenoarivo
    Processing Record 38 of Set 10 | abu jubayhah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=abu+jubayhah
    Processing Record 39 of Set 10 | kailua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kailua
    Processing Record 40 of Set 10 | folldal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=folldal
    Processing Record 41 of Set 10 | vadso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vadso
    Processing Record 42 of Set 10 | brainerd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=brainerd
    Processing Record 43 of Set 10 | broome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=broome
    Processing Record 44 of Set 10 | tabiauea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tabiauea
    Processing Record 45 of Set 10 | yulara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yulara
    Processing Record 46 of Set 10 | san clemente
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+clemente
    Processing Record 47 of Set 10 | surt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=surt
    Processing Record 48 of Set 10 | kattivakkam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kattivakkam
    Processing Record 49 of Set 10 | muli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=muli
    Processing Record 50 of Set 10 | santa cruz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=santa+cruz
    Processing Record 1 of Set 11 | suntar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=suntar
    Processing Record 2 of Set 11 | bo phloi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bo+phloi
    Processing Record 3 of Set 11 | puerto madryn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=puerto+madryn
    Processing Record 4 of Set 11 | arkhangelsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=arkhangelsk
    Processing Record 5 of Set 11 | nanortalik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nanortalik
    Processing Record 6 of Set 11 | birao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=birao
    Processing Record 7 of Set 11 | farsund
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=farsund
    Processing Record 8 of Set 11 | tuatapere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tuatapere
    Processing Record 9 of Set 11 | coihaique
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=coihaique
    Processing Record 10 of Set 11 | verkhnevilyuysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=verkhnevilyuysk
    Processing Record 11 of Set 11 | bargal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bargal
    Processing Record 12 of Set 11 | suao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=suao
    Processing Record 13 of Set 11 | matagami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=matagami
    Processing Record 14 of Set 11 | altay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=altay
    Processing Record 15 of Set 11 | arlit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=arlit
    Processing Record 16 of Set 11 | hasaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hasaki
    Processing Record 17 of Set 11 | dormidontovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dormidontovka
    Processing Record 18 of Set 11 | whitianga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=whitianga
    Processing Record 19 of Set 11 | volchikha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=volchikha
    Processing Record 20 of Set 11 | kirensk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kirensk
    Processing Record 21 of Set 11 | miraflores
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=miraflores
    Processing Record 22 of Set 11 | summerville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=summerville
    Processing Record 23 of Set 11 | mumbwa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mumbwa
    Processing Record 24 of Set 11 | mavelikara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mavelikara
    Processing Record 25 of Set 11 | matay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=matay
    Processing Record 26 of Set 11 | manakara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=manakara
    Processing Record 27 of Set 11 | villa maria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=villa+maria
    Processing Record 28 of Set 11 | wajima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=wajima
    Processing Record 29 of Set 11 | grindavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=grindavik
    Processing Record 30 of Set 11 | emerald
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=emerald
    Processing Record 31 of Set 11 | garissa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=garissa
    Processing Record 32 of Set 11 | newport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=newport
    Processing Record 33 of Set 11 | san andres
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+andres
    Processing Record 34 of Set 11 | villamontes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=villamontes
    Processing Record 35 of Set 11 | fuzhou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fuzhou
    Processing Record 36 of Set 11 | carndonagh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=carndonagh
    Processing Record 37 of Set 11 | hagersville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hagersville
    Processing Record 38 of Set 11 | sambava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sambava
    Processing Record 39 of Set 11 | sorvag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sorvag
    Processing Record 40 of Set 11 | moree
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=moree
    Processing Record 41 of Set 11 | zhaotong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zhaotong
    Processing Record 42 of Set 11 | nisia floresta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nisia+floresta
    Processing Record 43 of Set 11 | sitges
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sitges
    Processing Record 44 of Set 11 | nizhneyansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nizhneyansk
    Processing Record 45 of Set 11 | synya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=synya
    Processing Record 46 of Set 11 | inuvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=inuvik
    Processing Record 47 of Set 11 | george
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=george
    Processing Record 48 of Set 11 | rawson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rawson
    Processing Record 49 of Set 11 | bam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bam
    Processing Record 50 of Set 11 | fuerte olimpo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fuerte+olimpo
    Processing Record 1 of Set 12 | dali
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dali
    Processing Record 2 of Set 12 | wanning
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=wanning
    Processing Record 3 of Set 12 | benoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=benoy
    Processing Record 4 of Set 12 | tournon-sur-rhone
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tournon-sur-rhone
    Processing Record 5 of Set 12 | fez
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fez
    Processing Record 6 of Set 12 | saint-jean-de-braye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-jean-de-braye
    Processing Record 7 of Set 12 | mao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mao
    Processing Record 8 of Set 12 | baruun-urt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=baruun-urt
    Processing Record 9 of Set 12 | nauta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nauta
    Processing Record 10 of Set 12 | ukiah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ukiah
    Processing Record 11 of Set 12 | abiy adi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=abiy+adi
    Processing Record 12 of Set 12 | pemangkat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pemangkat
    Processing Record 13 of Set 12 | havoysund
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=havoysund
    Processing Record 14 of Set 12 | buin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=buin
    Processing Record 15 of Set 12 | nove zamky
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nove+zamky
    Processing Record 16 of Set 12 | baoding
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=baoding
    Processing Record 17 of Set 12 | laurel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=laurel
    Processing Record 18 of Set 12 | louisbourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=louisbourg
    Processing Record 19 of Set 12 | palabuhanratu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=palabuhanratu
    Processing Record 20 of Set 12 | rio branco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rio+branco
    Processing Record 21 of Set 12 | metro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=metro
    Processing Record 22 of Set 12 | tondon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tondon
    Processing Record 23 of Set 12 | veydelevka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=veydelevka
    Processing Record 24 of Set 12 | mora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mora
    Processing Record 25 of Set 12 | samsun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=samsun
    Processing Record 26 of Set 12 | nemuro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nemuro
    Processing Record 27 of Set 12 | la asuncion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=la+asuncion
    Processing Record 28 of Set 12 | golden
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=golden
    Processing Record 29 of Set 12 | champerico
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=champerico
    Processing Record 30 of Set 12 | acapulco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=acapulco
    Processing Record 31 of Set 12 | nkan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nkan
    Processing Record 32 of Set 12 | pivka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pivka
    Processing Record 33 of Set 12 | hingatungan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hingatungan
    Processing Record 34 of Set 12 | jork
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jork
    Processing Record 35 of Set 12 | lavrentiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lavrentiya
    Processing Record 36 of Set 12 | voi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=voi
    Processing Record 37 of Set 12 | atambua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atambua
    Processing Record 38 of Set 12 | mangrol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mangrol
    Processing Record 39 of Set 12 | quatre cocos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=quatre+cocos
    Processing Record 40 of Set 12 | mrirt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mrirt
    Processing Record 41 of Set 12 | shieli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=shieli
    Processing Record 42 of Set 12 | yantal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yantal
    Processing Record 43 of Set 12 | torbay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=torbay
    Processing Record 44 of Set 12 | chilmari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chilmari
    Processing Record 45 of Set 12 | dingle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dingle
    Processing Record 46 of Set 12 | mehamn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mehamn
    Processing Record 47 of Set 12 | we
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=we
    Processing Record 48 of Set 12 | umzimvubu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=umzimvubu
    Processing Record 49 of Set 12 | dzhusaly
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dzhusaly
    Processing Record 50 of Set 12 | benguela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=benguela
    Processing Record 1 of Set 13 | banyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=banyo
    Processing Record 2 of Set 13 | ancud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ancud
    Processing Record 3 of Set 13 | cap malheureux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cap+malheureux
    Processing Record 4 of Set 13 | mahanoro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mahanoro
    Processing Record 5 of Set 13 | jinchang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jinchang
    Processing Record 6 of Set 13 | boundiali
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=boundiali
    Processing Record 7 of Set 13 | bethel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bethel
    Processing Record 8 of Set 13 | stepnyak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=stepnyak
    Processing Record 9 of Set 13 | puerto escondido
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=puerto+escondido
    Processing Record 10 of Set 13 | oussouye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=oussouye
    Processing Record 11 of Set 13 | sovetskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sovetskiy
    Processing Record 12 of Set 13 | tanete
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tanete
    Processing Record 13 of Set 13 | eresos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=eresos
    Processing Record 14 of Set 13 | srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=srednekolymsk
    Processing Record 15 of Set 13 | saint-georges
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-georges
    Processing Record 16 of Set 13 | togur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=togur
    Processing Record 17 of Set 13 | dondo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dondo
    Processing Record 18 of Set 13 | biala podlaska
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=biala+podlaska
    Processing Record 19 of Set 13 | kosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kosa
    Processing Record 20 of Set 13 | atar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atar
    Processing Record 21 of Set 13 | galesong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=galesong
    Processing Record 22 of Set 13 | bayir
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bayir
    Processing Record 23 of Set 13 | oriximina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=oriximina
    Processing Record 24 of Set 13 | nkwerre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nkwerre
    Processing Record 25 of Set 13 | taft
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taft
    Processing Record 26 of Set 13 | komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=komsomolskiy
    Processing Record 27 of Set 13 | atbasar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atbasar
    Processing Record 28 of Set 13 | benito juarez
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=benito+juarez
    Processing Record 29 of Set 13 | baykit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=baykit
    


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
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
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


![png](output_14_0.png)


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


![png](output_16_0.png)


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


![png](output_18_0.png)


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


![png](output_20_0.png)

