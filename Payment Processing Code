# payment.py
import stripe

stripe.api_key = "YOUR_STRIPE_SECRET_KEY"

def process_payment(investment_amount, investor_id):
    try:
        # Create a PaymentIntent
        payment_intent = stripe.PaymentIntent.create(
            amount=investment_amount,
            currency="usd",
            payment_method_types=["card"],
        )

        # Confirm the PaymentIntent
        stripe.PaymentIntent.confirm(
            payment_intent.id,
            payment_method="pm_card_visa",
        )

        # Update the investment document
        investment = Investment.objects.get(id=investor_id)
        investment.investment_amount = investment_amount
        investment.save()

        return {"success": True, "message": "Payment processed successfully"}
    except stripe.error.CardError as e:
        return {"success": False, "message": "Card error: {}".format(e.user_message)}
    except stripe.error.RateLimitError as e:
        return {"success": False, "message": "Rate limit error: {}".format(e.user_message)}
    except stripe.error.InvalidRequestError as e:
        return {"success": False, "message": "Invalid request error: {}".format(e.user_message)}
```

### Review and Rating System Code
```
# models/review.py
from flask import Flask, request, jsonify
from flask_mongoengine import MongoEngine

app = Flask(__name__)
app.config["MONGODB_DB"] = "broker_bridge"
db = MongoEngine(app)

class Review(db.Document):
    investor_id = db.ReferenceField("User")
    property_id = db.ReferenceField("Property")
    rating = db.IntField(required=True, min_value=1, max_value=5)
    review = db.StringField(required=True)

    def __repr__(self):
        return f"Review('{self.investor_id}', '{self.property_id}')"
```