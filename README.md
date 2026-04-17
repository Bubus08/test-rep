python -m venv venv
Powershell -ExecutionPolicy Bypass
.\venv\Scripts\activate
pip install flask
pip install -U Flask-SQLAlchemy

pip list



python3 app.py



extentions SQLite and SQLite viewer





























{% extends "base.html" %}

{% block content %}
<h1>Checkout</h1>

{% if items %}
    <h2>Your Basket:</h2>
    <ul>
        {% for item in items %}
            <li>
                <img src="{{ item.product.product_image or url_for('static', filename='images/owl.jpg') }}" alt="Product Image" width="100">
                <strong>{{ item.product.name }}</strong> x{{ item.quantity }}
                <p>Price per item: £{{ "%.2f"|format(item.product.price) }}</p>
                <p>Total: £{{ "%.2f"|format(item.product.price * item.quantity) }}</p>
            </li>
        {% endfor %}
    </ul>
    
    <h3>Total: £{{ "%.2f"|format(total) }}</h3>

    <form method="POST">
        <button type="submit">Confirm Order</button>
    </form>
{% else %}
    <p>Your basket is empty.</p>
{% endif %}
{% endblock %}





#account



<h2>Past Orders</h2>
{% if past_orders %}
    {% for order_data in past_orders %}
        <div class="order">
            <h3>Order ID: {{ order_data.order.id }}</h3>
            <p>Order Date: {{ order_data.order.date }}</p>
            <p>Total: £{{ "%.2f"|format(order_data.order.total) }}</p>  <!-- You should add the `total` column to the Order model if it doesn't exist -->
            
            <h4>Items in this order:</h4>
            <ul>
                {% for item in order_data.items %}
                    <li>
                        <strong>{{ item.product.name }}</strong> (x{{ item.quantity }}) - £{{ "%.2f"|format(item.product.price * item.quantity) }}
                    </li>
                {% endfor %}
            </ul>
        </div>
        <hr>
    {% endfor %}
{% else %}
    <p>You haven't placed any orders yet.</p>
{% endif %}
