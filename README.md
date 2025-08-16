# Create a virtual environment
python -m venv env

# Activate the virtual environment (on Unix/Mac)
source env/bin/activate
# Or on Windows: env\Scripts\activate

# Install required packages
pip install django djangorestframework

# Create the Django project
django-admin startproject webhook_system .

# Create the payments app
python manage.py startapp payments

# Make migrations and migrate (using SQLite for simplicity; for PostgreSQL, update settings.py DATABASES accordingly)
python manage.py makemigrations
python manage.py migrate

# Run the server
python manage.py runserver


api end points
===============
1)   POST http://localhost:8000/webhook/payments
    haders=>X-Razorpay-Signature :1e55af4e30f3a59e19c669a86ec9df614a277bdf51b14291630f7fd7134d4b53
    json body=>
    {"event":"payment.authorized","payload":{"payment":{"entity":{"id":"pay_0114","status":"authorized","amount":5000,"currency":"INR"}}},"created_at":1751889865,"id":"evt_auth_0114"}
    
    generate this Razorpay-Signature by running /webhook_system\payments> python .\signature.py
2)get http://localhost:8000/payments/pay_014/events    or http://localhost:8000/payments/{payment_id}/events
project tree
=============

webhook_system/
├── manage.py
├── db.sqlite3  # This will be created after migrate
├── mock_payloads/  # Create this directory manually and add the JSON files as per instructions
│   ├── payment_authorized.json
│   ├── payment_captured.json
│   └── payment_failed.json
├── payments/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations/
│   │   ├── __init__.py
│   │   └── 0001_initial.py  # This will be created after makemigrations
│   ├── models.py
│   ├── tests.py
│   └── views.py
└── webhook_system/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
