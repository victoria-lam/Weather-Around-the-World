
# WeatherPy

## Analysis
- Cities that are located closer to the equator (0 degrees latitude) have higher maximum temperatures than those further away.
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

    Processing Record 1 of Set 1 | mount gambier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mount+gambier
    Processing Record 2 of Set 1 | hithadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hithadhoo
    Processing Record 3 of Set 1 | qaanaaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=qaanaaq
    Processing Record 4 of Set 1 | saint-philippe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-philippe
    Processing Record 5 of Set 1 | pevek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pevek
    Processing Record 6 of Set 1 | rikitea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rikitea
    Processing Record 7 of Set 1 | taolanaro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taolanaro
    Processing Record 8 of Set 1 | provideniya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=provideniya
    Processing Record 9 of Set 1 | georgetown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=georgetown
    Processing Record 10 of Set 1 | hilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hilo
    Processing Record 11 of Set 1 | hobart
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hobart
    Processing Record 12 of Set 1 | new norfolk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=new+norfolk
    Processing Record 13 of Set 1 | punta arenas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=punta+arenas
    Processing Record 14 of Set 1 | hurghada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hurghada
    Processing Record 15 of Set 1 | cabo san lucas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cabo+san+lucas
    Processing Record 16 of Set 1 | ilulissat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ilulissat
    Processing Record 17 of Set 1 | albany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=albany
    Processing Record 18 of Set 1 | iralaya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=iralaya
    Processing Record 19 of Set 1 | busselton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=busselton
    Processing Record 20 of Set 1 | sorland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sorland
    Processing Record 21 of Set 1 | bredasdorp
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bredasdorp
    Processing Record 22 of Set 1 | monsenhor gil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=monsenhor+gil
    Processing Record 23 of Set 1 | las rosas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=las+rosas
    Processing Record 24 of Set 1 | vila franca do campo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vila+franca+do+campo
    Processing Record 25 of Set 1 | iqaluit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=iqaluit
    Processing Record 26 of Set 1 | mataura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mataura
    Processing Record 27 of Set 1 | port alfred
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+alfred
    Processing Record 28 of Set 1 | matamoros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=matamoros
    Processing Record 29 of Set 1 | cape town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cape+town
    Processing Record 30 of Set 1 | kapaa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kapaa
    Processing Record 31 of Set 1 | victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=victoria
    Processing Record 32 of Set 1 | vaini
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vaini
    Processing Record 33 of Set 1 | komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=komsomolskiy
    Processing Record 34 of Set 1 | illoqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=illoqqortoormiut
    Processing Record 35 of Set 1 | yatou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yatou
    Processing Record 36 of Set 1 | mandurah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mandurah
    Processing Record 37 of Set 1 | fairbanks
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fairbanks
    Processing Record 38 of Set 1 | yellowknife
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yellowknife
    Processing Record 39 of Set 1 | arauco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=arauco
    Processing Record 40 of Set 1 | maniitsoq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=maniitsoq
    Processing Record 41 of Set 1 | tsihombe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tsihombe
    Processing Record 42 of Set 1 | reconquista
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=reconquista
    Processing Record 43 of Set 1 | kamenskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kamenskoye
    Processing Record 44 of Set 1 | talnakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=talnakh
    Processing Record 45 of Set 1 | pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pisco
    Processing Record 46 of Set 1 | bluff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bluff
    Processing Record 47 of Set 1 | avarua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=avarua
    Processing Record 48 of Set 1 | east london
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=east+london
    Processing Record 49 of Set 1 | ludvika
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ludvika
    Processing Record 50 of Set 1 | bethel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bethel
    Processing Record 1 of Set 2 | panaba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=panaba
    Processing Record 2 of Set 2 | te anau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=te+anau
    Processing Record 3 of Set 2 | gimli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gimli
    Processing Record 4 of Set 2 | san patricio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+patricio
    Processing Record 5 of Set 2 | achacachi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=achacachi
    Processing Record 6 of Set 2 | dikson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dikson
    Processing Record 7 of Set 2 | khash
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khash
    Processing Record 8 of Set 2 | palora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=palora
    Processing Record 9 of Set 2 | baisha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=baisha
    Processing Record 10 of Set 2 | grand river south east
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=grand+river+south+east
    Processing Record 11 of Set 2 | airai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=airai
    Processing Record 12 of Set 2 | lorengau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lorengau
    Processing Record 13 of Set 2 | sao felix do xingu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sao+felix+do+xingu
    Processing Record 14 of Set 2 | barrow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=barrow
    Processing Record 15 of Set 2 | saint-joseph
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-joseph
    Processing Record 16 of Set 2 | attawapiskat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=attawapiskat
    Processing Record 17 of Set 2 | jamestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jamestown
    Processing Record 18 of Set 2 | wulanhaote
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=wulanhaote
    Processing Record 19 of Set 2 | hommersak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hommersak
    Processing Record 20 of Set 2 | hermanus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hermanus
    Processing Record 21 of Set 2 | cayenne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cayenne
    Processing Record 22 of Set 2 | itarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=itarema
    Processing Record 23 of Set 2 | celestun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=celestun
    Processing Record 24 of Set 2 | qaqortoq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=qaqortoq
    Processing Record 25 of Set 2 | tupik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tupik
    Processing Record 26 of Set 2 | leningradskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=leningradskiy
    Processing Record 27 of Set 2 | la asuncion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=la+asuncion
    Processing Record 28 of Set 2 | khatanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khatanga
    Processing Record 29 of Set 2 | bolshaya chernigovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bolshaya+chernigovka
    Processing Record 30 of Set 2 | wufeng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=wufeng
    Processing Record 31 of Set 2 | salinas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=salinas
    Processing Record 32 of Set 2 | san rafael
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+rafael
    Processing Record 33 of Set 2 | severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=severo-kurilsk
    Processing Record 34 of Set 2 | kaeo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kaeo
    Processing Record 35 of Set 2 | santo antonio do sudoeste
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=santo+antonio+do+sudoeste
    Processing Record 36 of Set 2 | tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tuktoyaktuk
    Processing Record 37 of Set 2 | duldurga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=duldurga
    Processing Record 38 of Set 2 | anbu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=anbu
    Processing Record 39 of Set 2 | clyde river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=clyde+river
    Processing Record 40 of Set 2 | abu kamal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=abu+kamal
    Processing Record 41 of Set 2 | ribeira grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ribeira+grande
    Processing Record 42 of Set 2 | tahoua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tahoua
    Processing Record 43 of Set 2 | san joaquin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+joaquin
    Processing Record 44 of Set 2 | jalu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jalu
    Processing Record 45 of Set 2 | nanyamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nanyamba
    Processing Record 46 of Set 2 | bahia blanca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bahia+blanca
    Processing Record 47 of Set 2 | laguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=laguna
    Processing Record 48 of Set 2 | longyearbyen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=longyearbyen
    Processing Record 49 of Set 2 | pangoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pangoa
    Processing Record 50 of Set 2 | puerto ayora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=puerto+ayora
    Processing Record 1 of Set 3 | alyangula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=alyangula
    Processing Record 2 of Set 3 | sentyabrskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sentyabrskiy
    Processing Record 3 of Set 3 | chuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chuy
    Processing Record 4 of Set 3 | douentza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=douentza
    Processing Record 5 of Set 3 | nazarovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nazarovo
    Processing Record 6 of Set 3 | mahebourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mahebourg
    Processing Record 7 of Set 3 | chokurdakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chokurdakh
    Processing Record 8 of Set 3 | chastoozerye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chastoozerye
    Processing Record 9 of Set 3 | benghazi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=benghazi
    Processing Record 10 of Set 3 | carnarvon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=carnarvon
    Processing Record 11 of Set 3 | the valley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=the+valley
    Processing Record 12 of Set 3 | barentsburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=barentsburg
    Processing Record 13 of Set 3 | bowen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bowen
    Processing Record 14 of Set 3 | ushuaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ushuaia
    Processing Record 15 of Set 3 | toila
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=toila
    Processing Record 16 of Set 3 | mikhaylovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mikhaylovka
    Processing Record 17 of Set 3 | mar del plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mar+del+plata
    Processing Record 18 of Set 3 | fort nelson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fort+nelson
    Processing Record 19 of Set 3 | tautira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tautira
    Processing Record 20 of Set 3 | porto novo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=porto+novo
    Processing Record 21 of Set 3 | ossora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ossora
    Processing Record 22 of Set 3 | tasiilaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tasiilaq
    Processing Record 23 of Set 3 | lima duarte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lima+duarte
    Processing Record 24 of Set 3 | kampene
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kampene
    Processing Record 25 of Set 3 | kirksville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kirksville
    Processing Record 26 of Set 3 | esperance
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=esperance
    Processing Record 27 of Set 3 | labuhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=labuhan
    Processing Record 28 of Set 3 | port elizabeth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+elizabeth
    Processing Record 29 of Set 3 | atuona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atuona
    Processing Record 30 of Set 3 | owando
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=owando
    Processing Record 31 of Set 3 | grindavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=grindavik
    Processing Record 32 of Set 3 | saldanha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saldanha
    Processing Record 33 of Set 3 | banfora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=banfora
    Processing Record 34 of Set 3 | castleisland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=castleisland
    Processing Record 35 of Set 3 | bambous virieux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bambous+virieux
    Processing Record 36 of Set 3 | vredendal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vredendal
    Processing Record 37 of Set 3 | ahipara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ahipara
    Processing Record 38 of Set 3 | tiksi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tiksi
    Processing Record 39 of Set 3 | samusu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=samusu
    Processing Record 40 of Set 3 | saint-augustin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-augustin
    Processing Record 41 of Set 3 | thompson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=thompson
    Processing Record 42 of Set 3 | mecca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mecca
    Processing Record 43 of Set 3 | taitung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taitung
    Processing Record 44 of Set 3 | broome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=broome
    Processing Record 45 of Set 3 | belushya guba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=belushya+guba
    Processing Record 46 of Set 3 | fortuna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fortuna
    Processing Record 47 of Set 3 | margate
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=margate
    Processing Record 48 of Set 3 | agogo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=agogo
    Processing Record 49 of Set 3 | kvam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kvam
    Processing Record 50 of Set 3 | souillac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=souillac
    Processing Record 1 of Set 4 | kuche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kuche
    Processing Record 2 of Set 4 | namibe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=namibe
    Processing Record 3 of Set 4 | waling
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=waling
    Processing Record 4 of Set 4 | gejiu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gejiu
    Processing Record 5 of Set 4 | saskylakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saskylakh
    Processing Record 6 of Set 4 | huarmey
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=huarmey
    Processing Record 7 of Set 4 | atakpame
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atakpame
    Processing Record 8 of Set 4 | arraial do cabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=arraial+do+cabo
    Processing Record 9 of Set 4 | okhotsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=okhotsk
    Processing Record 10 of Set 4 | cairns
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cairns
    Processing Record 11 of Set 4 | bolungarvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bolungarvik
    Processing Record 12 of Set 4 | bathsheba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bathsheba
    Processing Record 13 of Set 4 | alofi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=alofi
    Processing Record 14 of Set 4 | kolda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kolda
    Processing Record 15 of Set 4 | mitu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mitu
    Processing Record 16 of Set 4 | sinnamary
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sinnamary
    Processing Record 17 of Set 4 | constitucion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=constitucion
    Processing Record 18 of Set 4 | butaritari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=butaritari
    Processing Record 19 of Set 4 | sechura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sechura
    Processing Record 20 of Set 4 | kampot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kampot
    Processing Record 21 of Set 4 | littleton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=littleton
    Processing Record 22 of Set 4 | codrington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=codrington
    Processing Record 23 of Set 4 | nome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nome
    Processing Record 24 of Set 4 | lebu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lebu
    Processing Record 25 of Set 4 | katsuura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=katsuura
    Processing Record 26 of Set 4 | saint george
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint+george
    Processing Record 27 of Set 4 | tombouctou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tombouctou
    Processing Record 28 of Set 4 | nemuro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nemuro
    Processing Record 29 of Set 4 | jaisinghnagar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jaisinghnagar
    Processing Record 30 of Set 4 | strathaven
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=strathaven
    Processing Record 31 of Set 4 | biak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=biak
    Processing Record 32 of Set 4 | ambon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ambon
    Processing Record 33 of Set 4 | zonguldak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zonguldak
    Processing Record 34 of Set 4 | faya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=faya
    Processing Record 35 of Set 4 | thisted
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=thisted
    Processing Record 36 of Set 4 | batemans bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=batemans+bay
    Processing Record 37 of Set 4 | vardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vardo
    Processing Record 38 of Set 4 | virginia beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=virginia+beach
    Processing Record 39 of Set 4 | palmer
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=palmer
    Processing Record 40 of Set 4 | auki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=auki
    Processing Record 41 of Set 4 | dickinson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dickinson
    Processing Record 42 of Set 4 | lasa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lasa
    Processing Record 43 of Set 4 | carsamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=carsamba
    Processing Record 44 of Set 4 | port moresby
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+moresby
    Processing Record 45 of Set 4 | upernavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=upernavik
    Processing Record 46 of Set 4 | lata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lata
    Processing Record 47 of Set 4 | campbell river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=campbell+river
    Processing Record 48 of Set 4 | mao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mao
    Processing Record 49 of Set 4 | springdale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=springdale
    Processing Record 50 of Set 4 | do gonbadan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=do+gonbadan
    Processing Record 1 of Set 5 | vaitupu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vaitupu
    Processing Record 2 of Set 5 | plettenberg bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=plettenberg+bay
    Processing Record 3 of Set 5 | torbay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=torbay
    Processing Record 4 of Set 5 | kodiak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kodiak
    Processing Record 5 of Set 5 | santa rosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=santa+rosa
    Processing Record 6 of Set 5 | hualmay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hualmay
    Processing Record 7 of Set 5 | mehamn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mehamn
    Processing Record 8 of Set 5 | nantucket
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nantucket
    Processing Record 9 of Set 5 | cidreira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cidreira
    Processing Record 10 of Set 5 | almazar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=almazar
    Processing Record 11 of Set 5 | padang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=padang
    Processing Record 12 of Set 5 | maues
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=maues
    Processing Record 13 of Set 5 | kavaratti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kavaratti
    Processing Record 14 of Set 5 | marsala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marsala
    Processing Record 15 of Set 5 | hare bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hare+bay
    Processing Record 16 of Set 5 | whitehorse
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=whitehorse
    Processing Record 17 of Set 5 | srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=srednekolymsk
    Processing Record 18 of Set 5 | norman wells
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=norman+wells
    Processing Record 19 of Set 5 | tevaitoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tevaitoa
    Processing Record 20 of Set 5 | kommunar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kommunar
    Processing Record 21 of Set 5 | aksarka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=aksarka
    Processing Record 22 of Set 5 | sorong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sorong
    Processing Record 23 of Set 5 | boueni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=boueni
    Processing Record 24 of Set 5 | khandela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khandela
    Processing Record 25 of Set 5 | vieste
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vieste
    Processing Record 26 of Set 5 | kavieng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kavieng
    Processing Record 27 of Set 5 | zapolyarnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zapolyarnyy
    Processing Record 28 of Set 5 | novobirilyussy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=novobirilyussy
    Processing Record 29 of Set 5 | quelimane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=quelimane
    Processing Record 30 of Set 5 | ajdabiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ajdabiya
    Processing Record 31 of Set 5 | naze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=naze
    Processing Record 32 of Set 5 | dianopolis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dianopolis
    Processing Record 33 of Set 5 | goderich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=goderich
    Processing Record 34 of Set 5 | touros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=touros
    Processing Record 35 of Set 5 | brae
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=brae
    Processing Record 36 of Set 5 | chimbote
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chimbote
    Processing Record 37 of Set 5 | petropavlovsk-kamchatskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=petropavlovsk-kamchatskiy
    Processing Record 38 of Set 5 | mareeba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mareeba
    Processing Record 39 of Set 5 | praia da vitoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=praia+da+vitoria
    Processing Record 40 of Set 5 | gisborne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gisborne
    Processing Record 41 of Set 5 | tacoronte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tacoronte
    Processing Record 42 of Set 5 | jumla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jumla
    Processing Record 43 of Set 5 | aksay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=aksay
    Processing Record 44 of Set 5 | princeton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=princeton
    Processing Record 45 of Set 5 | socorro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=socorro
    Processing Record 46 of Set 5 | faanui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=faanui
    Processing Record 47 of Set 5 | cherskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cherskiy
    Processing Record 48 of Set 5 | veraval
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=veraval
    Processing Record 49 of Set 5 | makakilo city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=makakilo+city
    Processing Record 50 of Set 5 | limbang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=limbang
    Processing Record 1 of Set 6 | mazyr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mazyr
    Processing Record 2 of Set 6 | anadyr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=anadyr
    Processing Record 3 of Set 6 | pandan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pandan
    Processing Record 4 of Set 6 | merauke
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=merauke
    Processing Record 5 of Set 6 | santa cruz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=santa+cruz
    Processing Record 6 of Set 6 | arkhangelskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=arkhangelskoye
    Processing Record 7 of Set 6 | mehriz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mehriz
    Processing Record 8 of Set 6 | chik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chik
    Processing Record 9 of Set 6 | hambantota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hambantota
    Processing Record 10 of Set 6 | ponta do sol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ponta+do+sol
    Processing Record 11 of Set 6 | duluth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=duluth
    Processing Record 12 of Set 6 | haines junction
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=haines+junction
    Processing Record 13 of Set 6 | tabou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tabou
    Processing Record 14 of Set 6 | utiroa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=utiroa
    Processing Record 15 of Set 6 | burns lake
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=burns+lake
    Processing Record 16 of Set 6 | roura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=roura
    Processing Record 17 of Set 6 | tateyama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tateyama
    Processing Record 18 of Set 6 | comodoro rivadavia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=comodoro+rivadavia
    Processing Record 19 of Set 6 | kasongo-lunda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kasongo-lunda
    Processing Record 20 of Set 6 | grand centre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=grand+centre
    Processing Record 21 of Set 6 | rapid valley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rapid+valley
    Processing Record 22 of Set 6 | silvania
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=silvania
    Processing Record 23 of Set 6 | geraldton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=geraldton
    Processing Record 24 of Set 6 | la libertad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=la+libertad
    Processing Record 25 of Set 6 | hofn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hofn
    Processing Record 26 of Set 6 | san quintin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+quintin
    Processing Record 27 of Set 6 | port lincoln
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+lincoln
    Processing Record 28 of Set 6 | taoudenni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taoudenni
    Processing Record 29 of Set 6 | kaitangata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kaitangata
    Processing Record 30 of Set 6 | shache
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=shache
    Processing Record 31 of Set 6 | buala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=buala
    Processing Record 32 of Set 6 | garmsar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=garmsar
    Processing Record 33 of Set 6 | san antonio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+antonio
    Processing Record 34 of Set 6 | lagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lagoa
    Processing Record 35 of Set 6 | castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=castro
    Processing Record 36 of Set 6 | hokitika
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hokitika
    Processing Record 37 of Set 6 | taft
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taft
    Processing Record 38 of Set 6 | solsvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=solsvik
    Processing Record 39 of Set 6 | hamilton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hamilton
    Processing Record 40 of Set 6 | rocha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rocha
    Processing Record 41 of Set 6 | chapais
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chapais
    Processing Record 42 of Set 6 | buraydah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=buraydah
    Processing Record 43 of Set 6 | guarapari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=guarapari
    Processing Record 44 of Set 6 | acarau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=acarau
    Processing Record 45 of Set 6 | amel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=amel
    Processing Record 46 of Set 6 | hasaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hasaki
    Processing Record 47 of Set 6 | aris
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=aris
    Processing Record 48 of Set 6 | teya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=teya
    Processing Record 49 of Set 6 | walvis bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=walvis+bay
    Processing Record 50 of Set 6 | kota bahru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kota+bahru
    Processing Record 1 of Set 7 | coracora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=coracora
    Processing Record 2 of Set 7 | luderitz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=luderitz
    Processing Record 3 of Set 7 | atambua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atambua
    Processing Record 4 of Set 7 | solnechnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=solnechnyy
    Processing Record 5 of Set 7 | doctor pedro p. pena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=doctor+pedro+p.+pena
    Processing Record 6 of Set 7 | awbari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=awbari
    Processing Record 7 of Set 7 | lompoc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lompoc
    Processing Record 8 of Set 7 | bereznik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bereznik
    Processing Record 9 of Set 7 | dalvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dalvik
    Processing Record 10 of Set 7 | bairiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bairiki
    Processing Record 11 of Set 7 | pangnirtung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pangnirtung
    Processing Record 12 of Set 7 | zhigansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zhigansk
    Processing Record 13 of Set 7 | la paz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=la+paz
    Processing Record 14 of Set 7 | paracuru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=paracuru
    Processing Record 15 of Set 7 | karratha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=karratha
    Processing Record 16 of Set 7 | mayo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mayo
    Processing Record 17 of Set 7 | asosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=asosa
    Processing Record 18 of Set 7 | kahului
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kahului
    Processing Record 19 of Set 7 | kato mazarakion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kato+mazarakion
    Processing Record 20 of Set 7 | klaksvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=klaksvik
    Processing Record 21 of Set 7 | mikun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mikun
    Processing Record 22 of Set 7 | ambunti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ambunti
    Processing Record 23 of Set 7 | emba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=emba
    Processing Record 24 of Set 7 | saint-francois
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-francois
    Processing Record 25 of Set 7 | mildura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mildura
    Processing Record 26 of Set 7 | quesnel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=quesnel
    Processing Record 27 of Set 7 | yulara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yulara
    Processing Record 28 of Set 7 | haibowan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=haibowan
    Processing Record 29 of Set 7 | kirakira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kirakira
    Processing Record 30 of Set 7 | verkhnevilyuysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=verkhnevilyuysk
    Processing Record 31 of Set 7 | salalah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=salalah
    Processing Record 32 of Set 7 | lengshuijiang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lengshuijiang
    Processing Record 33 of Set 7 | ebeltoft
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ebeltoft
    Processing Record 34 of Set 7 | waingapu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=waingapu
    Processing Record 35 of Set 7 | innisfail
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=innisfail
    Processing Record 36 of Set 7 | taungdwingyi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=taungdwingyi
    Processing Record 37 of Set 7 | gravdal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gravdal
    Processing Record 38 of Set 7 | zatyshshya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zatyshshya
    Processing Record 39 of Set 7 | tumannyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tumannyy
    Processing Record 40 of Set 7 | kathmandu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kathmandu
    Processing Record 41 of Set 7 | alekseyevsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=alekseyevsk
    Processing Record 42 of Set 7 | sao filipe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sao+filipe
    Processing Record 43 of Set 7 | paita
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=paita
    Processing Record 44 of Set 7 | nelson bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nelson+bay
    Processing Record 45 of Set 7 | makinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=makinsk
    Processing Record 46 of Set 7 | pimentel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pimentel
    Processing Record 47 of Set 7 | ust-kuyga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ust-kuyga
    Processing Record 48 of Set 7 | dzhusaly
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dzhusaly
    Processing Record 49 of Set 7 | zhanakorgan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zhanakorgan
    Processing Record 50 of Set 7 | namatanai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=namatanai
    Processing Record 1 of Set 8 | mackay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mackay
    Processing Record 2 of Set 8 | saint-leu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-leu
    Processing Record 3 of Set 8 | aras
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=aras
    Processing Record 4 of Set 8 | safwah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=safwah
    Processing Record 5 of Set 8 | nanga eboko
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nanga+eboko
    Processing Record 6 of Set 8 | maumere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=maumere
    Processing Record 7 of Set 8 | lolua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lolua
    Processing Record 8 of Set 8 | inderborskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=inderborskiy
    Processing Record 9 of Set 8 | ancud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ancud
    Processing Record 10 of Set 8 | kazerun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kazerun
    Processing Record 11 of Set 8 | cabedelo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cabedelo
    Processing Record 12 of Set 8 | amderma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=amderma
    Processing Record 13 of Set 8 | ingham
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ingham
    Processing Record 14 of Set 8 | praxedis guerrero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=praxedis+guerrero
    Processing Record 15 of Set 8 | gazli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gazli
    Processing Record 16 of Set 8 | umea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=umea
    Processing Record 17 of Set 8 | port hardy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+hardy
    Processing Record 18 of Set 8 | camacupa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=camacupa
    Processing Record 19 of Set 8 | gamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gamba
    Processing Record 20 of Set 8 | amazar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=amazar
    Processing Record 21 of Set 8 | guanica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=guanica
    Processing Record 22 of Set 8 | vanimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vanimo
    Processing Record 23 of Set 8 | bonavista
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bonavista
    Processing Record 24 of Set 8 | eskasem
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=eskasem
    Processing Record 25 of Set 8 | healdsburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=healdsburg
    Processing Record 26 of Set 8 | pirot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pirot
    Processing Record 27 of Set 8 | conde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=conde
    Processing Record 28 of Set 8 | orotukan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=orotukan
    Processing Record 29 of Set 8 | saleaula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saleaula
    Processing Record 30 of Set 8 | ulladulla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ulladulla
    Processing Record 31 of Set 8 | tuatapere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tuatapere
    Processing Record 32 of Set 8 | asau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=asau
    Processing Record 33 of Set 8 | narsaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=narsaq
    Processing Record 34 of Set 8 | sitka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sitka
    Processing Record 35 of Set 8 | muridke
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=muridke
    Processing Record 36 of Set 8 | avera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=avera
    Processing Record 37 of Set 8 | ashtabula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ashtabula
    Processing Record 38 of Set 8 | batagay-alyta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=batagay-alyta
    Processing Record 39 of Set 8 | lai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lai
    Processing Record 40 of Set 8 | vila
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vila
    Processing Record 41 of Set 8 | teluknaga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=teluknaga
    Processing Record 42 of Set 8 | nizhneyansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nizhneyansk
    Processing Record 43 of Set 8 | coihaique
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=coihaique
    Processing Record 44 of Set 8 | los llanos de aridane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=los+llanos+de+aridane
    Processing Record 45 of Set 8 | inirida
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=inirida
    Processing Record 46 of Set 8 | ranot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ranot
    Processing Record 47 of Set 8 | vila velha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vila+velha
    Processing Record 48 of Set 8 | fomboni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fomboni
    Processing Record 49 of Set 8 | inta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=inta
    Processing Record 50 of Set 8 | linda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=linda
    Processing Record 1 of Set 9 | praia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=praia
    Processing Record 2 of Set 9 | kirya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kirya
    Processing Record 3 of Set 9 | katherine
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=katherine
    Processing Record 4 of Set 9 | mwinilunga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mwinilunga
    Processing Record 5 of Set 9 | flagstaff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=flagstaff
    Processing Record 6 of Set 9 | tulsipur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tulsipur
    Processing Record 7 of Set 9 | koutiala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=koutiala
    Processing Record 8 of Set 9 | port-gentil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port-gentil
    Processing Record 9 of Set 9 | isabela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=isabela
    Processing Record 10 of Set 9 | sfantu gheorghe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sfantu+gheorghe
    Processing Record 11 of Set 9 | north bend
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=north+bend
    Processing Record 12 of Set 9 | fuzhou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fuzhou
    Processing Record 13 of Set 9 | cockburn town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cockburn+town
    Processing Record 14 of Set 9 | la ronge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=la+ronge
    Processing Record 15 of Set 9 | karkaralinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=karkaralinsk
    Processing Record 16 of Set 9 | mogadishu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mogadishu
    Processing Record 17 of Set 9 | port blair
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+blair
    Processing Record 18 of Set 9 | mys shmidta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mys+shmidta
    Processing Record 19 of Set 9 | cape canaveral
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cape+canaveral
    Processing Record 20 of Set 9 | gabi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gabi
    Processing Record 21 of Set 9 | guasdualito
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=guasdualito
    Processing Record 22 of Set 9 | disa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=disa
    Processing Record 23 of Set 9 | rio grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rio+grande
    Processing Record 24 of Set 9 | henzada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=henzada
    Processing Record 25 of Set 9 | longlac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=longlac
    Processing Record 26 of Set 9 | abu dhabi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=abu+dhabi
    Processing Record 27 of Set 9 | arivonimamo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=arivonimamo
    Processing Record 28 of Set 9 | road town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=road+town
    Processing Record 29 of Set 9 | dutlwe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dutlwe
    Processing Record 30 of Set 9 | loukhi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=loukhi
    Processing Record 31 of Set 9 | minna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=minna
    Processing Record 32 of Set 9 | meulaboh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=meulaboh
    Processing Record 33 of Set 9 | antofagasta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=antofagasta
    Processing Record 34 of Set 9 | barao de melgaco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=barao+de+melgaco
    Processing Record 35 of Set 9 | bargal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bargal
    Processing Record 36 of Set 9 | lieksa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lieksa
    Processing Record 37 of Set 9 | zambezi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zambezi
    Processing Record 38 of Set 9 | ranipur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ranipur
    Processing Record 39 of Set 9 | svetlogorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=svetlogorsk
    Processing Record 40 of Set 9 | chavantes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chavantes
    Processing Record 41 of Set 9 | nikolskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nikolskoye
    Processing Record 42 of Set 9 | agutaya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=agutaya
    Processing Record 43 of Set 9 | rungata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rungata
    Processing Record 44 of Set 9 | severo-yeniseyskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=severo-yeniseyskiy
    Processing Record 45 of Set 9 | roebourne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=roebourne
    Processing Record 46 of Set 9 | karamay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=karamay
    Processing Record 47 of Set 9 | lehututu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lehututu
    Processing Record 48 of Set 9 | tigil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tigil
    Processing Record 49 of Set 9 | alta floresta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=alta+floresta
    Processing Record 50 of Set 9 | urulga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=urulga
    Processing Record 1 of Set 10 | saint anthony
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint+anthony
    Processing Record 2 of Set 10 | yirol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yirol
    Processing Record 3 of Set 10 | kindu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kindu
    Processing Record 4 of Set 10 | thohoyandou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=thohoyandou
    Processing Record 5 of Set 10 | marsa matruh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marsa+matruh
    Processing Record 6 of Set 10 | vedaranniyam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vedaranniyam
    Processing Record 7 of Set 10 | svetlyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=svetlyy
    Processing Record 8 of Set 10 | cascais
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cascais
    Processing Record 9 of Set 10 | boende
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=boende
    Processing Record 10 of Set 10 | ensley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ensley
    Processing Record 11 of Set 10 | horni jiretin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=horni+jiretin
    Processing Record 12 of Set 10 | lavrentiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lavrentiya
    Processing Record 13 of Set 10 | urumqi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=urumqi
    Processing Record 14 of Set 10 | ust-kut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ust-kut
    Processing Record 15 of Set 10 | saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-pierre
    Processing Record 16 of Set 10 | vao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vao
    Processing Record 17 of Set 10 | ayan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ayan
    Processing Record 18 of Set 10 | akdepe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=akdepe
    Processing Record 19 of Set 10 | kurumkan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kurumkan
    Processing Record 20 of Set 10 | mosquera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mosquera
    Processing Record 21 of Set 10 | tambopata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tambopata
    Processing Record 22 of Set 10 | cravo norte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cravo+norte
    Processing Record 23 of Set 10 | saquarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saquarema
    Processing Record 24 of Set 10 | olovyannaya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=olovyannaya
    Processing Record 25 of Set 10 | saint-georges
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=saint-georges
    Processing Record 26 of Set 10 | bikin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bikin
    Processing Record 27 of Set 10 | yumen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yumen
    Processing Record 28 of Set 10 | jabiru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jabiru
    Processing Record 29 of Set 10 | yibin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=yibin
    Processing Record 30 of Set 10 | havelock
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=havelock
    Processing Record 31 of Set 10 | rundu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=rundu
    Processing Record 32 of Set 10 | poya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=poya
    Processing Record 33 of Set 10 | sisimiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sisimiut
    Processing Record 34 of Set 10 | bengkulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bengkulu
    Processing Record 35 of Set 10 | beringovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=beringovskiy
    Processing Record 36 of Set 10 | doha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=doha
    Processing Record 37 of Set 10 | luoyang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=luoyang
    Processing Record 38 of Set 10 | boa vista
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=boa+vista
    Processing Record 39 of Set 10 | vung tau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vung+tau
    Processing Record 40 of Set 10 | nhulunbuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nhulunbuy
    Processing Record 41 of Set 10 | placido de castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=placido+de+castro
    Processing Record 42 of Set 10 | laranjeiras do sul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=laranjeiras+do+sul
    Processing Record 43 of Set 10 | turukhansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=turukhansk
    Processing Record 44 of Set 10 | pontianak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pontianak
    Processing Record 45 of Set 10 | khonuu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khonuu
    Processing Record 46 of Set 10 | eureka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=eureka
    Processing Record 47 of Set 10 | vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vestmannaeyjar
    Processing Record 48 of Set 10 | camacha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=camacha
    Processing Record 49 of Set 10 | takoradi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=takoradi
    Processing Record 50 of Set 10 | eyl
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=eyl
    Processing Record 1 of Set 11 | tolaga bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tolaga+bay
    Processing Record 2 of Set 11 | ksenyevka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ksenyevka
    Processing Record 3 of Set 11 | kadykchan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kadykchan
    Processing Record 4 of Set 11 | maroantsetra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=maroantsetra
    Processing Record 5 of Set 11 | zarinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zarinsk
    Processing Record 6 of Set 11 | meadville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=meadville
    Processing Record 7 of Set 11 | nuuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nuuk
    Processing Record 8 of Set 11 | snezhnogorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=snezhnogorsk
    Processing Record 9 of Set 11 | berbera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=berbera
    Processing Record 10 of Set 11 | baraboo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=baraboo
    Processing Record 11 of Set 11 | boguchany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=boguchany
    Processing Record 12 of Set 11 | sirjan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sirjan
    Processing Record 13 of Set 11 | talawdi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=talawdi
    Processing Record 14 of Set 11 | gat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gat
    Processing Record 15 of Set 11 | balaipungut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=balaipungut
    Processing Record 16 of Set 11 | omboue
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=omboue
    Processing Record 17 of Set 11 | zyryanka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zyryanka
    Processing Record 18 of Set 11 | pacific grove
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pacific+grove
    Processing Record 19 of Set 11 | sakakah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sakakah
    Processing Record 20 of Set 11 | arlit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=arlit
    Processing Record 21 of Set 11 | charters towers
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=charters+towers
    Processing Record 22 of Set 11 | ayer itam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ayer+itam
    Processing Record 23 of Set 11 | san juan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=san+juan
    Processing Record 24 of Set 11 | manzil salim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=manzil+salim
    Processing Record 25 of Set 11 | palabuhanratu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=palabuhanratu
    Processing Record 26 of Set 11 | batsfjord
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=batsfjord
    Processing Record 27 of Set 11 | corner brook
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=corner+brook
    Processing Record 28 of Set 11 | shima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=shima
    Processing Record 29 of Set 11 | elliot lake
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=elliot+lake
    Processing Record 30 of Set 11 | bud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bud
    Processing Record 31 of Set 11 | neryungri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=neryungri
    Processing Record 32 of Set 11 | odweyne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=odweyne
    Processing Record 33 of Set 11 | paamiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=paamiut
    Processing Record 34 of Set 11 | caravelas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=caravelas
    Processing Record 35 of Set 11 | soyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=soyo
    Processing Record 36 of Set 11 | port hawkesbury
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+hawkesbury
    Processing Record 37 of Set 11 | kerchevskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kerchevskiy
    Processing Record 38 of Set 11 | marystown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marystown
    Processing Record 39 of Set 11 | kingaroy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kingaroy
    Processing Record 40 of Set 11 | kimbe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kimbe
    Processing Record 41 of Set 11 | andenes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=andenes
    Processing Record 42 of Set 11 | porbandar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=porbandar
    Processing Record 43 of Set 11 | gautier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=gautier
    Processing Record 44 of Set 11 | salinopolis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=salinopolis
    Processing Record 45 of Set 11 | porosozero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=porosozero
    Processing Record 46 of Set 11 | half moon bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=half+moon+bay
    Processing Record 47 of Set 11 | fernley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=fernley
    Processing Record 48 of Set 11 | wolbrom
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=wolbrom
    Processing Record 49 of Set 11 | davila
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=davila
    Processing Record 50 of Set 11 | dicabisagan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=dicabisagan
    Processing Record 1 of Set 12 | hvide sande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hvide+sande
    Processing Record 2 of Set 12 | kharovsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kharovsk
    Processing Record 3 of Set 12 | port hedland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=port+hedland
    Processing Record 4 of Set 12 | deputatskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=deputatskiy
    Processing Record 5 of Set 12 | guaraciaba do norte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=guaraciaba+do+norte
    Processing Record 6 of Set 12 | newport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=newport
    Processing Record 7 of Set 12 | laiyang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=laiyang
    Processing Record 8 of Set 12 | ozieri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ozieri
    Processing Record 9 of Set 12 | zaysan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=zaysan
    Processing Record 10 of Set 12 | riyadh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=riyadh
    Processing Record 11 of Set 12 | urusha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=urusha
    Processing Record 12 of Set 12 | tortoli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tortoli
    Processing Record 13 of Set 12 | nalgonda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=nalgonda
    Processing Record 14 of Set 12 | waipawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=waipawa
    Processing Record 15 of Set 12 | guanambi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=guanambi
    Processing Record 16 of Set 12 | chernyshevskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=chernyshevskiy
    Processing Record 17 of Set 12 | emilio carranza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=emilio+carranza
    Processing Record 18 of Set 12 | kanniyakumari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kanniyakumari
    Processing Record 19 of Set 12 | kytlym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kytlym
    Processing Record 20 of Set 12 | caucaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=caucaia
    Processing Record 21 of Set 12 | green river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=green+river
    Processing Record 22 of Set 12 | atagay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=atagay
    Processing Record 23 of Set 12 | leninsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=leninsk
    Processing Record 24 of Set 12 | kieta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kieta
    Processing Record 25 of Set 12 | plakhtiyivka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=plakhtiyivka
    Processing Record 26 of Set 12 | kenai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kenai
    Processing Record 27 of Set 12 | tete
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tete
    Processing Record 28 of Set 12 | pinawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pinawa
    Processing Record 29 of Set 12 | belyy yar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=belyy+yar
    Processing Record 30 of Set 12 | kargat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kargat
    Processing Record 31 of Set 12 | portland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=portland
    Processing Record 32 of Set 12 | emmett
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=emmett
    Processing Record 33 of Set 12 | waitati
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=waitati
    Processing Record 34 of Set 12 | poum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=poum
    Processing Record 35 of Set 12 | sao joao da barra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sao+joao+da+barra
    Processing Record 36 of Set 12 | bannu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=bannu
    Processing Record 37 of Set 12 | kabwe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=kabwe
    Processing Record 38 of Set 12 | tessalit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tessalit
    Processing Record 39 of Set 12 | burica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=burica
    Processing Record 40 of Set 12 | cermik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=cermik
    Processing Record 41 of Set 12 | svetlyy yar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=svetlyy+yar
    Processing Record 42 of Set 12 | jiddah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=jiddah
    Processing Record 43 of Set 12 | puerto escondido
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=puerto+escondido
    Processing Record 44 of Set 12 | tatarsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tatarsk
    Processing Record 45 of Set 12 | khandagayty
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=khandagayty
    Processing Record 46 of Set 12 | umzimvubu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=umzimvubu
    Processing Record 47 of Set 12 | ewa beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=ewa+beach
    Processing Record 48 of Set 12 | oakville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=oakville
    Processing Record 49 of Set 12 | marcona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=marcona
    Processing Record 50 of Set 12 | lisakovsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=lisakovsk
    Processing Record 1 of Set 13 | darnah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=darnah
    Processing Record 2 of Set 13 | vitre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=vitre
    Processing Record 3 of Set 13 | aitape
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=aitape
    Processing Record 4 of Set 13 | isla mujeres
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=isla+mujeres
    Processing Record 5 of Set 13 | moron
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=moron
    Processing Record 6 of Set 13 | tucumcari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tucumcari
    Processing Record 7 of Set 13 | pires do rio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=pires+do+rio
    Processing Record 8 of Set 13 | mardin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=mardin
    Processing Record 9 of Set 13 | sola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=sola
    Processing Record 10 of Set 13 | tura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=tura
    Processing Record 11 of Set 13 | hovd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&appid=f69e8609b24ababd74a0428bbcc559f2&q=hovd
    


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


![png](output_12_0.png)


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


![png](output_14_0.png)


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


![png](output_16_0.png)


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


![png](output_18_0.png)

