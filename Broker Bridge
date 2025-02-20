# models/investment.py
from flask import Flask, request, jsonify
from flask_mongoengine import MongoEngine

app = Flask(__name__)
app.config["MONGODB_DB"] = "broker_bridge"
db = MongoEngine(app)

class Investment(db.Document):
    investor_id = db.ReferenceField("User")
    investment_amount = db.DecimalField(required=True, min_value=500)
    investment_date = db.DateTimeField(required=True, default=datetime.utcnow)
    portfolio_value = db.DecimalField(required=True, default=0)

    def update_portfolio_value(self, new_value):
        self.portfolio_value = new_value
        self.save()
```

### Property Listings Code
```
# models/property.py
from flask import Flask, request, jsonify
from flask_mongoengine import MongoEngine

app = Flask(__name__)
app.config["MONGODB_DB"] = "broker_bridge"
db = MongoEngine(app)

class Property(db.Document):
    title = db.StringField(required=True)
    description = db.StringField(required=True)
    price = db.DecimalField(required=True)
    location = db.StringField(required=True)
    images = db.ListField(db.StringField())
    broker_id = db.ReferenceField("User")

    def __repr__(self):
        return f"Property('{self.title}', '{self.location}')"
```

### Transactions Code
```
# models/transaction.py
from flask import Flask, request, jsonify
from flask_mongoengine import MongoEngine

app = Flask(__name__)
app.config["MONGODB_DB"] = "broker_bridge"
db = MongoEngine(app)

class Transaction(db.Document):
    investor_id = db.ReferenceField("User")
    property_id = db.ReferenceField("Property")
    transaction_amount = db.DecimalField(required=True)
    transaction_date = db.DateTimeField(required=True, default=datetime.utcnow)

    def __repr__(self):
        return f"Transaction('{self.investor_id}', '{self.property_id}')"
```