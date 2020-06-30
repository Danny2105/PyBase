# PyBase Class

## Attributes

---

## Methods

- `delete(obj)`
    - Delete a object from the database established in PyBase init.
- `exists(database: str, db_type: str)`
    - Fetch if the given database exists.
- `fetch(obj: str, sub=None)`
    - Fetch an object and its sub_objects inside the database established in PyBase init.
- `insert(content: dict)`
    - Insert a dictionary content inside the given database file.
- `read()`
    - Read the database file established in PyBase init to to access its objects.

------

### `init(database: str, db_type: str, db_path: str = pathlib.Path().absolute())`

> Define the database to use and create it if it doesn't exist.

#### Parameters

- `database : str`
    - The name of the database without extension.
- `db_type : str`
    - The database type.
    - Available types: `JSON`, `YAML`, `SQLite`
- `db_path : str`
    - The path where the database is located (default is current working directory).
    - Example: `/home/bloodbath/Desktop/PyBase`

> Note: db_type **isn't** case sensitive, you can use lowercase or uppercase.

#### Raises
- `TypeError`
    - If database or db_type isn't a String.
- `ValueError`
    - If the given db_type isn't a valid type (`JSON`, `YAML`, `SQLite`).
- `FileNotFoundError`
    - If the given path wasn't found.

#### Example
```py
PyBase("users", "JSON") #=> ./users.json
```

------

### `delete(self, obj)`

> Delete a object from the database established in PyBase init.

#### Parameters

- `obj`
    - The object which will be deleted from the database.

#### Raises

- `KeyError`
    - If key isn't found.
- `ValueError`
    - If obj doesn't have a value (is equal to zero or None).

#### Example
```py
# {'bloodbath': 'dev', 'night': 'tester'}
delete('bloodbath') #=> {'night': 'tester'}
```

------

### `exists(self, database: str, db_path: str = pathlib.Path().absolute())`

> Fetch if the given database exists.

#### Parameters

- `database : str`
    - The name of the database **with extension**.

- `db_path : str`
    - The path where the database is located (default is current working directory).
    - Example: `/home/bloodbath/Desktop/PyBase`

#### Raises

- `TypeError`
    - If database or db_path isn't a String.

#### Returns

- `bool`
    - Returns `True` or `False` depending on if the database given exists in the given path.

#### Example
```py
# /home/bloodbath/Desktop/PyBase/config.yaml
exists('config.yaml') #=> True / False
```

------

### `fetch(self, obj: str, sub: dict = None)`

> Fetch an object and its sub_objects inside the database established in PyBase init.

#### Parameters

- `obj : str`
    - The object which will be fetched inside the database.
- `sub : dict, optional`
    - The sub_object(s) of the object which will be fetched inside the database.

> Note: sub **cannot** contain more than 5 objects or nested dictionaries for now.

#### Raises

- `TypeError`
    - If obj isn't a String or if sub isn't a list.
- `ValueError`
    - If sub have more than 5 objects inside.
- `KeyError`
    - If sub doesn't exist in the database.

#### Returns

- `str`
    - If the object or sub_objects are a String.
- `int`
    - If the object or sub_objects are a Integer.
- `float`
    - If the object or sub_objects are a Float.
- `bool`
    - If the object or sub_objects are a Boolean.

#### Example
```py
#----- Fetch without sub_objects -------------------------------------
# {'user': 'bloodbath'}
fetch('user') #=> <class 'str'>

#----- Fetch with sub_objects ----------------------------------------
# When searching for sub_objects, it's recommended to set a value of
# None to the objects, since their value doesn't affect the search.
# 
# {'users': {
#     'bloodbath': 12345,
#     'night': 67890
#     }
# }
fetch('user', {'night': None}) #=> <class 'int'>
```

------

### `insert(self, content: dict)`

> Insert a dictionary content inside the database file established in PyBase init.

#### Parameters

- `content : dict`
    - The content which will be inserted inside the database.

#### Raises

- `TypeError`
    - If content isn't a dictionary.

#### Example
```py
# {}
insert({'dev': 'bloodbath'}) #=> {'dev': 'bloodbath'}
```

------

### `read()`

> Read the database file established in PyBase init to access its objects.
> 
> **Note:** __this method isn't for writing purposes. To add objects to your db, please use `insert`.__

#### Parameters

#### Raises

#### Returns
- `dict`
    - A dictionary which contains all the database objects.

#### Example
```py
# {'editors': {
#   'GUI': 'VSC',
#   'TUI': 'Neovim'
#   }
# }
#
#----- Reading the entire database -----------------------
read() #=> {'editors': {'GUI': 'VSC', 'TUI': 'Neovim'}}

#----- Reading the GUI object ----------------------------
read()['editors']['GUI'] #=> {'GUI': 'VSC'}
```
