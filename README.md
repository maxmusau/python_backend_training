# Python Backend Training Project (Django + FastAPI)

## Overview

This project is a **training guide for a Software Engineering Intern**
learning how to implement **Python-based business logic using Django and
FastAPI**.\
The training focuses on:

-   Python backend fundamentals
-   Django business data modeling
-   FastAPI REST API development
-   Business logic implementation
-   Building a small backend service

The goal is to help the intern understand how **enterprise backend
systems process business rules and expose APIs**.

------------------------------------------------------------------------

# Training Structure

## Day 1 -- Python Backend Foundations

Focus on Python concepts used in backend business logic.

### Example: Order Validation Logic

``` python
def validate_order_amount(amount):
    MIN_ORDER = 10
    MAX_ORDER = 1000

    if amount < MIN_ORDER:
        return "Order amount too low"
    elif amount > MAX_ORDER:
        return "Order amount exceeds limit"
    else:
        return "Order amount is valid"

print(validate_order_amount(50))
```

Key Concepts - Python functions - Business rule validation - Conditional
logic

------------------------------------------------------------------------

## Day 2 -- Django Business Application Development

### Example Django Model

`models.py`

``` python
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.FloatField()
    stock = models.IntegerField()

    def __str__(self):
        return self.name
```

Run migrations

``` bash
python manage.py makemigrations
python manage.py migrate
```

### Example Django View

``` python
from django.http import JsonResponse
from .models import Product

def list_products(request):
    products = Product.objects.all().values()
    return JsonResponse(list(products), safe=False)
```

Concepts - Django ORM - Database modeling - CRUD operations

------------------------------------------------------------------------

## Day 3 -- FastAPI REST API Development

### Basic FastAPI App

``` python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():
    return {"message": "Backend API running"}
```

Run server

``` bash
uvicorn main:app --reload
```

### Request Validation with Pydantic

``` python
from pydantic import BaseModel

class Product(BaseModel):
    name: str
    price: float
    stock: int

@app.post("/products/")
def create_product(product: Product):
    return {
        "message": "Product created",
        "product": product
    }
```

Concepts - REST APIs - Request validation - JSON responses

------------------------------------------------------------------------

## Day 4 -- Business Logic Implementation

### Order Processing Logic

``` python
def process_order(product_price, quantity):
    total = product_price * quantity

    if total > 500:
        discount = total * 0.10
    else:
        discount = 0

    final_amount = total - discount

    return {
        "total": total,
        "discount": discount,
        "final_amount": final_amount
    }
```

Concepts - Business rules - Discount logic - Service layer functions

------------------------------------------------------------------------

## Day 5 -- Mini Backend Project

Example: **Task Management API**

### Task Model

``` python
from pydantic import BaseModel

class Task(BaseModel):
    title: str
    description: str
    completed: bool = False
```

### Task API

``` python
tasks = []

@app.post("/tasks/")
def create_task(task: Task):
    tasks.append(task)
    return {"message": "Task added", "task": task}

@app.get("/tasks/")
def get_tasks():
    return tasks
```

Concepts - API endpoints - Mock database - Backend service development

------------------------------------------------------------------------

# Project Structure Example

    backend-training/
    │
    ├── django_app/
    │   ├── models.py
    │   ├── views.py
    │   └── urls.py
    │
    ├── fastapi_service/
    │   └── main.py
    │
    ├── business_logic/
    │   └── order_service.py
    │
    └── README.md

------------------------------------------------------------------------

# Best Practices

### Use Clear Functions

``` python
def calculate_total(price: float, quantity: int) -> float:
    return price * quantity
```

### Handle Errors Properly

``` python
from fastapi import HTTPException

@app.get("/products/{id}")
def get_product(id: int):
    if id > 10:
        raise HTTPException(status_code=404, detail="Product not found")
    return {"product_id": id}
```

------------------------------------------------------------------------

# Final Exercise for the Intern

Build a **Simple Inventory API** with:

-   Add product
-   List products
-   Update stock
-   Delete product
-   Apply discount rule

Technologies

-   Python
-   Django ORM
-   FastAPI
-   REST APIs

------------------------------------------------------------------------

This project demonstrates how **backend engineers implement business
logic and expose services in real-world enterprise systems.**
