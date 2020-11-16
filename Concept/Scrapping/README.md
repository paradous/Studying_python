# Scrapping

## Librairies
```Python
import requests
import lxml
from bs4 import BeautifulSoup
```

## XML scrapping
For this xml document:

```XML
<?xml version="1.0" encoding="UTF-8"?>
<users>
    <user data-id="101">
        <nom>Zorro</nom>
        <metier>Danseur</metier>
    </user>
    <user data-id="102">
        <nom>Hulk</nom>
        <metier>Footballeur</metier>
    </user>
    <user data-id="103">
        <nom>Zidane</nom>
        <metier>Star</metier>
    </user>
    <user data-id="104">
        <nom>Beans</nom>
        <metier>Epicier</metier>
    </user>
    <user data-id="105">
        <nom>Batman</nom>
        <metier>Veterinaire</metier>
    </user>
    <user data-id="106">
        <nom>Spiderman</nom>
        <metier>Veterinaire</metier>
    </user>
</users>
```

### 1. Get a list of all <name> data
```Python
from lxml import etree
tree = etree.parse("../path/to/my/document.xml")

# I retrieve all <user><nom> in <users>
for user in tree.xpath("/users/user/nom"):
    print(user.text)
```

Result:
```
Zorro
Hulk
Zidane
Beans
Batman
Spiderman
```

### 2. Get all attributes of a tag
We retrieve the *data-id* attribute from the *user* tag.
```Python
from lxml import etree
tree = etree.parse("../path/to/my/document.xml")

for user in tree.xpath("/users/user"):
    print(user.get("data-id"))
```

Result:
```
101
102
103
104
105
106
```

### 3. Get a list of all <name> data filtered by job
We retrieve all *user/name* who are *Veterinaire*.
```Python
from lxml import etree
tree = etree.parse("../path/to/my/document.xml")

for user in tree.xpath("/users/user[metier='Veterinaire']/nom"):
    print(user.text)
```

Result:
```
Batman
Spiderman
```

## HTML scrapping

### Get all H1 from an HTML document
```Python
from bs4 import BeautifulSoup
soup = BeautifulSoup(html_doc, "lxml") # "html_doc" is an HTML document

for p in soup.find_all('h1'):
    print (p.text) # We only retrieve the content => .text
```

## Web requests

### Get an html document from the web
```Python
from bs4 import BeautifulSoup
import requests

def get_webpage(url):
    res = requests.get(url)
    
    if res.status_code == 200:
        return BeautifulSoup(res.content,'lxml')

webpage = get_webpage("https://www.becode.org/about/")
```
