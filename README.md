# Understat Data Scrape
Scrape Shot location data from understat.com

![](https://github.com/cooperh01/understat_scrape/blob/main/FornalsSDScrap.ipynb)

```
import requests
from bs4 import BeautifulSoup
import json
import pandas as pd
```
```
base_url = 'https://understat.com/player/'
player = str(input('Please enter player id:'))
url = base_url + player
```
Please enter player id: 2335

```
url
```
'https://understat.com/player/2335'
```
res = requests.get(url)
soup = BeautifulSoup(res.content,'lxml')
scripts = soup.find_all('script')
```
```
strings = scripts[3].string
```
```
# strip unnecessary symbols and get only JSON data 
ind_start = strings.index("('")+2 
ind_end = strings.index("')") 
json_data = strings[ind_start:ind_end] 
json_data = json_data.encode('utf8').decode('unicode_escape')

#convert string to json format
data = json.loads(json_data)
```
```
x = []
y = []
xG = []
season = []
result = []


for index in range(len(data)):
    for key in data[index]:
        if key == 'X':
            x.append(data[index][key])
        if key == 'Y':
            y.append(data[index][key])
        if key == 'xG':
            xG.append(data[index][key])
        if key == 'season':
            season.append(data[index][key])
        if key == 'result':
            result.append(data[index][key])
```
```
col_names = ['x','y','xG','season','result']
df = pd.DataFrame([x,y,xG,season,result],index=col_names)
df = df.T
```
```
df
```
```
df.to_csv('FornalsShotData.csv')
```
