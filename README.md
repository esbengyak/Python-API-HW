
- There is direct correlation between city latitude and the max temperature in that city
- There is no correlation between city latitude and cloudiness
- There is no correlation between city latitude and wind speed


```python
from citipy import citipy
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import requests
import os
import seaborn as sns
import random
from random import uniform
import urllib
import time



output_file = "weather_cities.csv"

```


```python
lat_longs = []
cities = []
lats_generate = np.random.uniform(low=-90.000, high=90.000, size=1800)
longs_generate = np.random.uniform(low=-180.000, high=180.000, size=1800)
lat_longs = zip(lats_generate, longs_generate)
print(lat_longs)

for lat_lng in lat_longs:
    city = citipy.nearest_city(lat_lng[0], lat_lng[1]).city_name
    if city not in cities:
        cities.append(city)
len(cities)

```

    <zip object at 0x0000020A12E44D08>
    




    690




```python
weather_api = "85225f802373e5d9cb5253efb6fdeda8"
url = "http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=" + weather_api
city_info = []
city_count = 1
info_count = 1
for x, city in enumerate(cities):
    city_url = url + "&q=" + urllib.request.pathname2url(city)
    print(city_url)
    city_count += 1
    try:
        city_response = requests.get(city_url).json()
        latitude_data = city_response["coord"]["lat"]
        longitude_data = city_response["coord"]["lon"]
        max_temp = city_response["main"]["temp_max"]
        humid = city_response["main"]["humidity"]
        clouds = city_response["clouds"]["all"]
        wind = city_response["wind"]["speed"]
        country = city_response["sys"]["country"]
        date = city_response["dt"]
        
        city_info.append({"City": city, 
                          "Latitude": latitude_data, 
                          "Longitude": longitude_data, 
                          "Max Temp": max_temp,
                          "Humidity": humid,
                          "Cloudiness": clouds,
                          "Wind Speed": wind,
                          "Country": country,
                          "Date": date})    
    except:
        pass

```

    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chunskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tiksi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=taoudenni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=narsaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=faanui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yellowknife
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=puerto%20escondido
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nuuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ushuaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=luchegorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pinega
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bereda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cape%20town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=havoysund
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cidreira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=busselton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sitia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lebu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=skibbereen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=witu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bilibino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=guerrero%20negro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20elizabeth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nikolskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=torbay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=esperance
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=soyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tiznit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mataura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hermanus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bluff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=broome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=daru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=atuona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saldanha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nyagan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zemio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=belmonte
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=coihaique
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=barrow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20alfred
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=touros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=amderma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vaini
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=punta%20arenas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint-philippe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=robstown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=la%20montanita
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mys%20shmidta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=taltal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bredasdorp
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kapaa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oudtshoorn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mayya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kamloops
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=qaanaaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=taolanaro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=norman%20wells
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jamestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bernay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rikitea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shebunino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ponta%20do%20sol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dikson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=egvekinot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=palmer
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jackson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gizo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tornio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=upernavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=marsa%20matruh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tuatapere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=leningradskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20hardy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rodrigues%20alves
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kaitangata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=burnie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tumannyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=new%20norfolk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=puerto%20ayora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cabo%20san%20lucas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bengkulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=istok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mazamari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hays
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=geraldton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kodiak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=belaya%20gora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=terra%20santa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tautira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sorvag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=los%20llanos%20de%20aridane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mahebourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=illoqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=muzhi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cheuskiny
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nizhneyansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=barcelos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=butaritari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=solnechnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=poya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=den%20helder
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=waitati
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rio%20gallegos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kannauj
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chokurdakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=middle%20island
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bahia%20blanca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dawson%20creek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=namibe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hobart
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hofn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=plettenberg%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=georgetown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kokoda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sterling
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tsihombe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bethel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=forestville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=arraial%20do%20cabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=santiago
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kavieng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=carnarvon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bambous%20virieux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=amurzet
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=samusu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lardos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lompoc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mergui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20quintin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lavrentiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=khatanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=palabuhanratu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=belushya%20guba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=faratsiho
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20patricio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=albany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=christchurch
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fortuna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=najran
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ocho%20rios
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=margate
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sambava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=necochea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=salalah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=atar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mar%20del%20plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=khao%20yoi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=brive-la-gaillarde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bad%20sachsa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sentyabrskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ordu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mount%20gambier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=charagua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=olafsvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kant
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vallenar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=antofagasta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hay%20river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=klyuchi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saurimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nago
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saskylakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=padang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kruisfontein
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nemuro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=calvinia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=aleksandrovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mlalo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=makakilo%20city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rocha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kirakira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ponta%20delgada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=akdepe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=laiagam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=petauke
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=souillac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=katobu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nyrob
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ahipara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=manavalakurichi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kampong%20thum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=huayang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sept-iles
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=uk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=iqaluit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ouadda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=henties%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=basna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tabou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=formosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bahia%20honda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=evensk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kochubey
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nouadhibou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sechura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=itarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=filingue
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=knysna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lorengau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=santiago%20del%20estero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20pirie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kytlym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=avarua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hunza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=turukhansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hithadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hibbing
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vostok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=burns%20lake
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint-joseph
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sambhar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20macquarie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=westport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hope%20mills
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cayenne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=aklavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=talnakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=manta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bargal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=praya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pemberton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=longyearbyen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=general%20roca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=buchanan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hasaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fort%20nelson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=inhambane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pouebo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bilma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=urdzhar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ondorhaan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=birao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=comodoro%20rivadavia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=broken%20hill
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ayan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tasiilaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ayios%20matthaios
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=severo-yeniseyskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=marienburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=beringovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pandan%20niog
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=laguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=valleyview
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vaitupu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=williamsport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mishkino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint%20george
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hoa%20binh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chahal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=grand%20river%20south%20east
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mackay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=husavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=airai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ancud
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=talcahuano
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sao%20sebastiao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=alofi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=eatonton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=high%20rock
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=katsuura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=muros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tsumeb
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=east%20london
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=maturin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=beloha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oranjestad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=barentsburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kahului
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gjellerup%20kirkeby
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ulagan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dondo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=samarai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=clyde%20river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ilulissat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oktyabrskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=monrovia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=garanhuns
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=weyburn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=weihai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20moresby
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=waipawa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=morgantown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nikolaevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=finschhafen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=acapulco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pevek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nguiu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tateyama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vanimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=koppa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yerbogachen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pangnirtung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lolua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cherskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=grand%20gaube
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=klaksvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ramet
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=veshkayma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=adrar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hamilton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=turtkul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ambon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cartaya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zilair
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=palu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=santa%20maria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=areosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=acari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=princeton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hvolsvollur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=karia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gohpur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=victoria%20point
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nabire
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint%20anthony
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sungaipenuh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=teya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sinnamary
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=manhattan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=solvychegodsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mae%20ramat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vila%20franca%20do%20campo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zile
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=brownsville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ratnagiri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lubango
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tawzar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bakel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nanortalik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=buin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=auxerre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20hedland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=esna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nishihara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=galiwinku
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=libenge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wuxi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=romny
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=andevoranto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=abu%20zabad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ilkeston
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bonham
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=luderitz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20blair
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dourbali
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=banjar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=antalaha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kawalu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=guilin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=seymchan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kudahuvadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=killybegs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=halalo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=thalassery
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=severobaykalsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=havelock
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=skalistyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=petropavlovka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gberia%20fotombu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=takoradi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=riverton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tartus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=morro%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kieta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sao%20miguel%20do%20araguaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jaguaruana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=verkhoyansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bage
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=luwuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ambilobe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sao%20jose%20da%20coroa%20grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hambantota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ruatoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fairmont
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=thompson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kizilskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=matagami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fairbanks
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ibra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bay%20roberts
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=araouane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=karasjok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=umzimvubu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=iquitos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sile
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lazo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20cristobal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=victor%20harbor
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=leeton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=richards%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lusaka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=trat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oktyabrskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=orlik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=outjo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=antsohihy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kerman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ilhabela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nanchong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=palmas%20de%20monte%20alto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=loandjili
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=provideniya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=laje
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=codrington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=moerai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=altay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=corinto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=murgab
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=akita
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wahran
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=qaqortoq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=axim
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=itapirapua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=concepcion%20del%20oro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=paamiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=naze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yar-sale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vanderhoof
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=labuhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kangaatsiaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tres%20picos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=abu%20samrah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20policarpo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=amahai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=imeni%20stepana%20razina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=linxia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=toktogul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yazman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=constitucion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=phu%20khieo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=destin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bell%20ville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kavaratti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=boshnyakovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rungata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=banda%20aceh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=half%20moon%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kloulklubed
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sao%20filipe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=isabela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mathbaria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=inyonga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ippy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=khani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dingle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=agadez
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=idil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vila%20velha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=the%20valley
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port-cartier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=guayaramerin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=aldan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=russellville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=trairi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sayat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=college
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ribeira%20grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=itamaraca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=poronaysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=carutapera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dunedin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ust-kulom
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ostersund
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=susanville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=felipe%20carrillo%20puerto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pokhara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=roald
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=waddan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=isiro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bumba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=moses%20lake
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yenagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tazovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kayes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=emmen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pelotas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=las%20navas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=boueni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nhulunbuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lakki%20marwat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=babahoyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=abha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tucumcari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mangrol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nizwa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tatawin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gravdal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=okhotsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dwarka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=smiltene
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hirara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jiwani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ibicarai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dongsheng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=voka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mananara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kisangani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=attawapiskat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=beyneu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=conakry
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=miraflores
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=circleville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=macau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saleaula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nelson%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kamenskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=edson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=venice
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cabra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mount%20hagen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tamandare
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=macduff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=brae
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=haradok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20salvo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=innisfail
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sol-iletsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kurumkan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=czechowice-dziedzice
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=anadyr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=liyang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=batticaloa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=camana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kashi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zhezkazgan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=uglich
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint-augustin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pacific%20grove
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sitka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fevralsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dovolnoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mrirt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mozarlandia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jumla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sakakah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tilichiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=benguela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20luis
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=umm%20jarr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sulina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kulhudhuffushi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=firozpur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=portland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mitsamiouli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chute-aux-outardes
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zelenoborskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oshikango
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=porto%20recanati
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=firminy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=itoman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kabwe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gigmoto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tejupilco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=agutaya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chengde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=walvis%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ust-tsilma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=urumqi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kraslava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=umm%20kaddadah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=solano
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=muisne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sajanan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=coquimbo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dukat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=la%20ronge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gafanha%20da%20encarnacao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=skiros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lakewood
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oyama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cap-aux-meules
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ketchikan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=morehead
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=berlevag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lantawan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=louisbourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dicabisagan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=linkou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=qingyuan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wanlaweyn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mandera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=thinadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mogadishu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zaragoza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kapoeta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ca%20mau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=haverfordwest
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=abalak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kristianstad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=madang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=verkhnevilyuysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bairiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tucuman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=coos%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=muvattupula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tondano
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=marcona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=melfi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=montepuez
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ares
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kamenka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=petropavlovsk-kamchatskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rapallo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sigli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=coruripe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=borogontsy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pleshanovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bathsheba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hobbs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kendrapara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=temaraia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yashkul
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=puerto%20el%20triunfo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lydenburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=doka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pathalgaon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=inta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sosnovo-ozerskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mogadouro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kamaishi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sheltozero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=awbari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lembang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=maceio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sarahan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pizarro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mullaitivu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=baglung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=miri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=viedma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=isangel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bocaranga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rambha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=havre-saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=skagastrond
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mareeba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=abnub
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tougan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bolshaya%20glushitsa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mocuba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=grindavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hereford
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mehamn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hervey%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=melnikovo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=winsum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=malanje
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sembe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lancaster
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=genthin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chipiona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=galgani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=te%20anau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=katherine
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tabiauea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=matamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=juneau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=glodeni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ryotsu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=manaure
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yalvac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=northam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wilmington%20island
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sao%20felix%20do%20xingu
    


```python
city_data_df = pd.DataFrame(city_info)

latitude_info = city_data_df["Latitude"]
longitude_info = city_data_df["Longitude"]
max_temps_info = city_data_df["Max Temp"]
humidity_info = city_data_df["Humidity"]
cloudiness_info = city_data_df["Cloudiness"]
wind_info = city_data_df["Wind Speed"]

city_data_df.to_csv(output_file, index = "City_Info")

city_data_df.count()


```




    City          622
    Cloudiness    622
    Country       622
    Date          622
    Humidity      622
    Latitude      622
    Longitude     622
    Max Temp      622
    Wind Speed    622
    dtype: int64




```python
city_data_df.head()
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
      <th>City</th>
      <th>Cloudiness</th>
      <th>Country</th>
      <th>Date</th>
      <th>Humidity</th>
      <th>Latitude</th>
      <th>Longitude</th>
      <th>Max Temp</th>
      <th>Wind Speed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>chunskiy</td>
      <td>44</td>
      <td>RU</td>
      <td>1529364245</td>
      <td>63</td>
      <td>56.08</td>
      <td>99.63</td>
      <td>64.19</td>
      <td>7.65</td>
    </tr>
    <tr>
      <th>1</th>
      <td>chuy</td>
      <td>0</td>
      <td>UY</td>
      <td>1529364246</td>
      <td>90</td>
      <td>-33.69</td>
      <td>-53.46</td>
      <td>45.20</td>
      <td>8.10</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tiksi</td>
      <td>0</td>
      <td>RU</td>
      <td>1529364014</td>
      <td>79</td>
      <td>71.64</td>
      <td>128.87</td>
      <td>51.86</td>
      <td>3.96</td>
    </tr>
    <tr>
      <th>3</th>
      <td>taoudenni</td>
      <td>92</td>
      <td>ML</td>
      <td>1529364247</td>
      <td>12</td>
      <td>22.68</td>
      <td>-3.98</td>
      <td>99.65</td>
      <td>14.47</td>
    </tr>
    <tr>
      <th>4</th>
      <td>narsaq</td>
      <td>20</td>
      <td>GL</td>
      <td>1529362200</td>
      <td>65</td>
      <td>60.91</td>
      <td>-46.05</td>
      <td>46.40</td>
      <td>13.87</td>
    </tr>
  </tbody>
</table>
</div>




```python
plt.scatter(latitude_info,
            max_temps_info,
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Cities")

plt.title("City Latitude vs. Max Temperature (%s)" % time.strftime("%x"))
plt.ylabel("Max Temperature (F)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("Latitude vs Temp.png")

plt.show()

```


![png](output_6_0.png)



```python
plt.scatter(latitude_info,
            humidity_info,
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Cities")

plt.title("City Latitude vs. Humidity (%s)" % time.strftime("%x"))
plt.ylabel("Humidity (%)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("City Latitude vs Humidity.png")

plt.show()

```


```python
plt.scatter(latitude_info,
            cloudiness_info,
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Cities")

plt.title("City Latitude vs. Cloudiness (%s)" % time.strftime("%x"))
plt.ylabel("Cloudiness (%)")
plt.xlabel("Latitude")
plt.grid(True)

plt.savefig("City Latitude vs Cloudiness.png")

plt.show()

```


![png](output_8_0.png)



```python
plt.scatter(latitude_info,
            wind_info,
            edgecolor="black", linewidths=1, marker="o",
            alpha=0.8, label="Cities")

plt.title("City Latitude vs. Wind Speed (%s)" % time.strftime("%x"))
plt.ylabel("Wind Speed (mph)")
plt.xlabel("Latitude")
plt.grid(True)

# Save the figure
plt.savefig("City Latitude vs Speed.png")

# Show plot
plt.show()


```


![png](output_9_0.png)

