# Understat Data Scrape
Scrape Shot location data from understat.com


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
