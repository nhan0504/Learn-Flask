# Introduction
- Flask is a micro web framework that is designed to be simple and easy to use

# Getting started
## Install
```
pip install Flask
```
- If run into errno 13 then use command 
```
pip install Flask --user
```

## Create an instance of flask
- `__name__` is a special attribute with the value of the name of the module (The name of the file)
``` python
from flask import Flask
app = Flask(__name__)
```