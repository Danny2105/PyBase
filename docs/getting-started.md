# Getting Started

This is a short introduction to PyBase that contains
installation and a sample code (you can also see it in GH).

> **Current PyBase version and status:** (**v0.1.0 - Beta**).

------

## Installing PyBase

> **Before starting, you have to know that PyBase doesn't
> have support for Python 2.7, only Python 3 onwards.**

PyBase can be installed through pip with the following command.
```sh
pip install pybase_db
```

## Creating our first db with pybase

With the example extracted from GH, we can do the following.
```py
#-------------- Importing PyBase Class ---------------------------------------
# Lets import PyBase Class from PyBase Package
from pybase_db import PyBase
#
#-------------- Initializing PyBase ------------------------------------------
# Lets define our database name and format (with default db_path).
# db_type isn't case sensitive. You can use JSON and json and it'll be valid.
db = PyBase("example", "JSON")  #=> ./example.json
#
#-------------- Using Insert Method ------------------------------------------
# Lets define and add some content to our database.
pybase_info = {"pybase": "awesomeness", "version": "0.1.0"}
# Lets insert the defined dict inside our database.
db.insert(pybase_info)  #=> {'pybase': 'awesomeness', 'version': '0.1.0'}
print(db.read())
#
#-------------- Using Delete Method ------------------------------------------
# Lets delete an object inside our database cuz it's useless.
db.delete('pybase')  #=> {'version': '0.1.0'}
print(db.read())
#
#-------------- Using Fetch Method -------------------------------------------
# Lets fetch an object inside our database and display its type.
# It's useful to debug and manipulate the data dynamically.
print(db.fetch('version'))
```
