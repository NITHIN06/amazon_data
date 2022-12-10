# Dataset Creation Using Web Scraping
This project will create a dataset by doing web scraping and store in a CSV file. 


## Installation

requirement.txt file contains all the required python packages

To install the requirements use the following cmd
```bash
pip install -r requirement.txt
```
or..

Use the package manager [pip](https://pip.pypa.io/en/stable/) to install all required packages.

```bash
pip install bs4 requests pandas numpy
```

## Usage
Here packages are bs4, requests, pandas, and numpy.
```python
from bs4 import BeautifulSoup
import numpy as np
import pandas as pd
import requests
```

### Requests package
The requests package is used to get the web page content. requests package has a get method. it takes the URL and headers as parameters and returns the web page's content. Here headers are unique for everyone you can get your header from [here](https://www.whatismybrowser.com/detect/what-is-my-user-agent/). Replace it with '---' in below code
```python
HEADERS = HEADERS = ({'User-Agent':'----', 'Accept-Language':'en-US, en;q=0.5'})
website = requests.get(url,headers=headers)
print(website.content)
```
### bs4 Package
bs4 package provides BeautifulSoup method it will help us to parse through previous output(website.content)
```python
soup = BeautifulSoup(webpage.content, 'html.parser')
```
Now we will extract all <a> tags from the web page using the method find_all with tag name and attrs as parameters. In attrs we mention the required attribute and value (as mentioned in inspect tab).
```python
links = soup.find_all("a", attrs={'class': 'a-link-normal s-underline-text s-underline-link-text s-link-style a-text-normal'})
```
Then collect all products <a> tag and extract href attribute values to extract the title, price, ratings, review count and store it in a dictionary

### Pandas Package
pandas package is used to store the dictionary in a DataFrame format and remove unnecessary rows. Finally, store it in a CSV file.
``` python
amazon_df = pd.DataFrame.from_dict(d)
amazon_df['title'].replace('', np.nan,inplace=True)
amazon_df = amazon_df.dropna(subset=['title'])
amazon_df.to_csv("amazon_data.csv", header=True, index=False)
```
## License

[MIT](https://choosealicense.com/licenses/mit/)
