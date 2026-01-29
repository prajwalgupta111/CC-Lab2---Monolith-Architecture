# CC Lab 2 – Monolithic FastAPI Application

## Overview

This project is part of **Cloud Computing Lab 2** and demonstrates the working and limitations of a **monolithic architecture** using a FastAPI web application. The application includes features such as user registration, login, event listing, event registration, and checkout, all running as a single deployed unit.

The lab also focuses on identifying performance bottlenecks and improving response time using **Locust load testing**.

---

## Features Implemented

* User registration and login
* Event listing and registration
* User-specific event dashboard (`/my-events`)
* Checkout functionality
* Global exception handling
* Load testing using Locust (terminal/headless mode)

---

## Technology Stack

* **Python**
* **FastAPI**
* **SQLite**
* **Jinja2 Templates**
* **Locust** (for load testing)

---

## Project Structure

```
CC Lab-2/
├── main.py
├── database.py
├── checkout/
├── events/
├── my_events/
├── locust/
├── templates/
├── requirements.txt
└── fest.db
```

---

## How to Run the Application

### 1. Create and activate virtual environment

```bash
python -m venv .venv
.\.venv\Scripts\activate
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Initialize database

```bash
python insert_events.py
```

### 4. Run the server

```bash
python -m uvicorn main:app --reload
```

Server will start at:

```
http://127.0.0.1:8000
```

---

## Load Testing with Locust (Terminal Mode)

Locust was used in **headless mode** to test performance.

### `/events` route

```bash
locust -f locust/events_locustfile.py --headless -u 1 -r 1 -t 30s --host http://localhost:8000
```

### `/my-events` route

```bash
locust -f locust/myevents_locustfile.py --headless -u 1 -r 1 -t 30s --host http://localhost:8000
```

---

## Performance Optimization Summary

Performance bottlenecks were identified in the `/events` and `/my-events` routes, where unnecessary CPU-intensive loops were present inside request handlers. These loops caused increased response time under load and affected the entire application due to the monolithic architecture.

The optimization involved removing these unnecessary loops so that each route only executes required database operations and response rendering. After optimization, Locust results showed reduced average response time with similar request throughput.

---

## Key Learning Outcomes

* Understanding monolithic application architecture
* Identifying CPU-bound bottlenecks in request handlers
* Using Locust for load testing
* Improving performance through simple code-level optimizations

---



**PES1UG2XCS426**
Cloud Computing Lab – CC Lab 2


