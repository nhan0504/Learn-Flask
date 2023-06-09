# Introduction
- Flask is a micro web framework that is designed to be simple and easy to use

# Install
```
pip install Flask
```
- If run into errno 13 then use command 
```
pip install Flask --user
```

# Create an instance of flask
`__name__` is a special attribute with the value of the name of the module (The name of the file)
``` python
from flask import Flask
app = Flask(__name__)
```

# Create a route
- `@app.route` decorator
- `<int:item_id>`: A parameter of type int
``` python
@app.route('/items/<int:item_id>')
def get_item(item_id):
    # Retrieve the item with the specified ID from the database
    item = retrieve_item_from_database(item_id)
    return item
```

## Route with POST methods
``` python 
from flask import request
@app.route('/items', methods=['POST'])
def create_item():
    # Retrieve the item data from the request body
    item_data = request.get_json()
    
    # Create a new item in the database using the item data
    new_item_id = create_item_in_database(item_data)
    
    # Return a response indicating that the item was created
    return {'id': new_item_id, 'message': 'Item created successfully'}
```

# Organize related routes
- Use Blueprint -> organize related routes, views, and other code -> Register that Blueprint with the Flask application
Create a blueprint
``` python
from flask import Blueprint, jsonify

item_bp = Blueprint('item', __name__)

@item_bp.route('/items')
def get_items():
    # Retrieve a list of items from the database
    items = retrieve_users_from_database()
    return jsonify(items)
```
Register with the flask application
``` python
from flask import Flask
from item_bp import item_bp

app = Flask(__name__)
app.register_blueprint(item_bp)
```