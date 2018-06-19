
- There is direct correlation between city latitude and the max temperature in that city
- As you move farther from the equator, the city humidity begins to decrease
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

    <zip object at 0x00000239D8EE4308>
    




    678




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

    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=klaksvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kaitangata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tabuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ushuaia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=weihe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shenjiamen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mataura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=acapulco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lavrentiya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jamestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kapaa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=taolanaro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=barentsburg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cape%20town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hofn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bourg-les-valence
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=thompson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=alofi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shache
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lebu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=illoqqortoormiut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=atuona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=carnarvon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mar%20del%20plata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=belushya%20guba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=toliary
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kudahuvadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vallenar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=punta%20arenas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=butaritari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=katsuura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20alfred
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tiksi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=barcelos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=busselton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bethel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kavieng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=albany
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rikitea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hamada
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dikson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=meyungs
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=souris
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=east%20london
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saleaula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=puerto%20madryn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=puerto%20ayora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kostomuksha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vaini
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bonavista
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=faanui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bengkulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=georgetown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint-philippe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hermanus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=esperance
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=leningradskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chokurdakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=razgrad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=broome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=borger
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hithadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kaeo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hobart
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=marcona
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fairbanks
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ahipara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=coquimbo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kijang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cherskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=veinticinco%20de%20mayo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=eureka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=broken%20hill
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hilo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yellowknife
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hushitai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mahebourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kahului
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bismarck
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gamba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=blytheville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tuatapere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tasiilaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nizhneyansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bambous%20virieux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sesvete
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pangnirtung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=babanusah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kalos%20agros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=richards%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fortuna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=victoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yaan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vardo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=constitucion
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=libertador%20general%20san%20martin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saldanha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=barrow
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=berlevag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bredasdorp
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=micomeseng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=avarua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sitka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cambridge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bandarbeyla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=umba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bloemfontein
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=batsfjord
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kuche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pisco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nikolskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nanortalik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kruisfontein
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ust-nera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=doha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bluff
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=muros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20blair
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=levski
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lander
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=utinga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sikasso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=roma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=itarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cururupu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=crixas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=macusani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=isla%20mujeres
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=alexandria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kangaatsiaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tirlyanskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mecca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fevralsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ilulissat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tamandare
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zambezi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kavaratti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=paracuru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ribeira%20grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shieli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tsienyane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sao%20joao%20da%20barra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=isangel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=norman%20wells
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sambava
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=maine-soroa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=upernavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sampit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=narsaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mayo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=krasnoselkup
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=villarrica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=torbay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lorut
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kodiak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nizhnevartovsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=luancheng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=iwaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=amderma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nanzhou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shiyan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=khonuu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=las%20matas%20de%20farfan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=santo%20tomas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=impfondo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=new%20norfolk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=aasiaat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=geraldton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yuci
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kapit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=suntar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lingao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=araguacu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gurupa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cerinza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hobyo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=castro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20andres
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hebertville
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bhola
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=qaanaaq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cidreira
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tsihombe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20juan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=flin%20flon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=malwan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mamakan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zhigansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=harper
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=matagami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=los%20llanos%20de%20aridane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=airai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=turukhansk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=boende
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lasa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tomatlan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20patricio
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=souillac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=severo-kurilsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=quelimane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=meulaboh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pouebo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20hedland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=husavik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mogadishu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jalu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=khatanga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=maracacume
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cockburn%20town
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=suez
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=qeshm
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tigil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ambilobe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=semey
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=castelo%20branco
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jibuti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=malanje
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wadi%20musa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=iqaluit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=roald
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pochutla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chegdomyn
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mount%20isa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=balabac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bonthe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kupang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=takoradi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=galle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ostrovnoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=magdagachi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=arraial%20do%20cabo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ovalle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jasper
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cabo%20san%20lucas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint%20george
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=douglas
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wulanhaote
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wukari
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yulara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=uren
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sawakin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=anadyr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pizhanka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=amapa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=havoysund
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ratnagiri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=palmer
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=miraflores
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=acarau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mutum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ngaoundere
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ayan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lhuntshi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=poum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zyryanka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=falealupo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=koumac
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=avera
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mys%20shmidta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tuktoyaktuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sokoto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ivdel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hasaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=huaidian
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=half%20moon%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=price
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=guangyuan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tessalit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=xuddur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint-augustin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=totness
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bubaque
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=barabinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saurimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jackson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20keats
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tual
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lahaina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=linfen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=iquitos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shakawe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sao%20filipe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=longyan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tateyama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=guerrero%20negro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=khor
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bambanglipuro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shakiso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=thurso
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=grand%20centre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tsarychanka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=clyde%20river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dingle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rosarito
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=namatanai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=anchorage
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hualmay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=guangshui
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=salalah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tazovskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=puerto%20escondido
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=luderitz
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=conde
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kyra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fukue
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=olafsvik
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=henties%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=valea%20ciorii
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=maneadero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=havre-saint-pierre
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mago
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=okha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=buala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mandurah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nsanje
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tonj
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ayabe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=catuday
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=beyneu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=buraydah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bartica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=baykit
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ballina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=trairi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ikalamavony
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chakwal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20cristobal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=palabuhanratu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=asau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=thinadhoo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=raudeberg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tuam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chernenko
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tuy%20hoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kununurra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=laguna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=la%20ronge
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tukrah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mayumba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kimbe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oksfjord
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fort%20nelson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=codrington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=muisne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=matamoros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mitsamiouli
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ruteng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yar-sale
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=provost
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gisborne
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gravenhurst
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ponta%20do%20sol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=samarai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=altus
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=loiza
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint-joseph
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20vicente
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=margate
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20elizabeth
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bereda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=skalistyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=fare
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=charlestown
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saquarema
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=boyolangu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=camacha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=honningsvag
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=longyearbyen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pimentel
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=imeni%20poliny%20osipenko
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lorengau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chuy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pemba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20moresby
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=assiniboia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nguru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=korla
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=adrar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vaitupu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kanye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lolua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chepareria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nuuk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bure
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mountain%20home
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lalmohan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=santos%20dumont
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kaniama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kibala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=brokopondo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lagoa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tumannyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=carolina
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=luebo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ojinaga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ngunguru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mount%20gambier
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=timizart
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kazalinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vostok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=olinda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=faya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rio%20grande
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=araouane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wejherowo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ketchikan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hambantota
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tabiauea
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nadym
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ust-maya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pavilosta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=turka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20lincoln
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=crotone
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=thano%20bula%20khan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=svetlogorsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bababe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kutum
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pevek
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wenatchee
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=grand-lahou
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=keetmanshoop
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shingu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kazachinskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=marhaura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=riyadh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=flinders
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bokspits
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ziyang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=terrace%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mandalgovi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=asfi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zhezkazgan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sergiyevsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bristol
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port-gentil
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kutahya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=macheng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hamilton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=beidao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kungurtug
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kamenskoye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=karratha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wakkanai
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sorland
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lompoc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=seabra
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vanimo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=banmo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vagur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rawson
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=awjilah
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=coahuayana
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=alta%20floresta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lingdong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=venado%20tuerto
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oxford
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=brightwater
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20policarpo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bystrice%20nad%20pernstejnem
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bridlington
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=waingapu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kropotkin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=te%20anau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shebunino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=martapura
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wichian%20buri
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tongliao
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=plataresti
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nemuro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rawannawi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ginda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=north%20bend
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ljubovija
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chekhov
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=andalucia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=linhares
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=praia
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=manjacaze
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mineral%20wells
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=humpolec
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=trani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bairiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=novyy%20urengoy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=taoudenni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=qena
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ust-kamchatsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=samusu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dunedin
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vila%20franca%20do%20campo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=alyangula
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vestmanna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chagda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=solwezi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tahoua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=santa%20cruz%20das%20palmeiras
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=attawapiskat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vestmannaeyjar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=walvis%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lata
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nishihara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=provideniya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20macquarie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dunhua
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=atar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=inhambane
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=diplo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=vigrestad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=neftcala
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=batticaloa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=burica
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rheinberg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=konevo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=palm%20city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=niksic
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=burnie
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rafaela
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=haibowan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=labutta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=rabat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tilichiki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=urubicha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bilma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yiyang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=srednekolymsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=petropavlovsk-kamchatskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=aporawan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tiarei
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saskylakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=soller
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=verkhoshizhemye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=praxedis%20guerrero
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gumrak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kieta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=betare%20oya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kyaikkami
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=khuldabad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mackay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=boguchar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=manggar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=stonewall
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=poronaysk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dzhusaly
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=baruun-urt
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mayya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mareeba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kiama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=aberlour
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=louisbourg
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=oussouye
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chicama
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=santa%20isabel%20do%20rio%20negro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tsiroanomandidy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=port%20augusta
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=yuanping
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kagoro
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gizo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mattoon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=touros
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=piterka
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ngukurr
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=la%20palma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=peniche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sabha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kaduna
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mentok
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=one%20hundred%20mile%20house
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nome
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kisangani
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=san%20carlos%20de%20bariloche
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gonaives
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=egvekinot
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=paysandu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=grand%20gaube
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bolitoc
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=houlung
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=samalaeulu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=praia%20da%20vitoria
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=matara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dzhebariki-khaya
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=namibe
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=evensk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=abadiania
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=chernyshevskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=zhelnino
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=celestun
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hirara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=katobu
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=antalaha
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=santa%20rosa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kulhudhuffushi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=talnakh
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=craig
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=alotau
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pemberton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=derzhavinsk
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hampton
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=komsomolskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kawambwa
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=porto%20belo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sur
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ilinskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sentyabrskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=paciran
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=maniitsoq
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nantucket
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tyrma
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=trinidad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=agadez
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ewa%20beach
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=batemans%20bay
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sabirabad
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hovd
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pasighat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pemangkat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=slave%20lake
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=cap%20malheureux
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mazatlan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=porto%20novo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=robertsport
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=sao%20paulo%20de%20olivenca
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=makakilo%20city
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=quatre%20cocos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tres%20arroyos
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=jauja
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=hearst
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tirumullaivasal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=solnechnyy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=solginskiy
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pasni
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=labuhan
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=puerto%20rondon
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ulaangom
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=campbell%20river
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=halalo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=wenling
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pindwara
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=dornoch
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=natal
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=mezen
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ipora
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tambacounda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=bathsheba
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=christchurch
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nang%20rong
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=saint-georges
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=amga
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=iguape
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=umm%20durman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nenjiang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=daru
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=blackwater
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=opuwo
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=padang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=williston
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=goundam
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=soeng%20sang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=tianpeng
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=maumelle
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ransang
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=methven
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=shimoda
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=nakhon%20si%20thammarat
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=lima
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=pouembout
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=ishigaki
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=biak
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=soure
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=itoman
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=gaoual
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=kalmar
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=maragogi
    http://api.openweathermap.org/data/2.5/weather?units=Imperial&APPID=85225f802373e5d9cb5253efb6fdeda8&q=swan%20river
    


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




    City          600
    Cloudiness    600
    Country       600
    Date          600
    Humidity      600
    Latitude      600
    Longitude     600
    Max Temp      600
    Wind Speed    600
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
      <td>klaksvik</td>
      <td>88</td>
      <td>FO</td>
      <td>1529367600</td>
      <td>87</td>
      <td>62.23</td>
      <td>-6.59</td>
      <td>48.20</td>
      <td>27.51</td>
    </tr>
    <tr>
      <th>1</th>
      <td>kaitangata</td>
      <td>32</td>
      <td>NZ</td>
      <td>1529369992</td>
      <td>83</td>
      <td>-46.28</td>
      <td>169.85</td>
      <td>43.40</td>
      <td>13.80</td>
    </tr>
    <tr>
      <th>2</th>
      <td>tabuk</td>
      <td>44</td>
      <td>PH</td>
      <td>1529369993</td>
      <td>89</td>
      <td>17.41</td>
      <td>121.44</td>
      <td>74.72</td>
      <td>2.28</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ushuaia</td>
      <td>40</td>
      <td>AR</td>
      <td>1529366400</td>
      <td>69</td>
      <td>-54.81</td>
      <td>-68.31</td>
      <td>37.40</td>
      <td>5.82</td>
    </tr>
    <tr>
      <th>4</th>
      <td>weihe</td>
      <td>12</td>
      <td>CN</td>
      <td>1529369993</td>
      <td>71</td>
      <td>32.99</td>
      <td>105.33</td>
      <td>68.33</td>
      <td>2.84</td>
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


![png](output_7_0.png)



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

plt.savefig("City Latitude vs Speed.png")

plt.show()


```


![png](output_9_0.png)

