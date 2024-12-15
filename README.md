# Django Mpesa Integration

This project integrates Mpesa with a Django application to handle payments. It uses Celery for background task processing, Redis as the message broker, and implements environment variable management for secure configuration.

## Features

- Mpesa API integration for handling payments and callbacks
- Celery for processing background tasks
- Redis for task message brokering
- Django for the main application
- Secure configuration management using environment variables

## Prerequisites

Before you begin, ensure that you have the following installed:

- Python 3.8+
- Django 3.x
- Celery
- Redis
- Mpesa credentials for API access

## Tech Stack

- **Frontend**: Django templates, HTML, CSS, Bootstrap
- **Backend**: Django, Celery, Redis
- **Database**: MySQL, or other relational DB (based on configuration)
- **API Communication**: Mpesa API, Celery for background task processing
- **Environment Management**: Python 3.8+, Django 3.x, environment variables for secure configuration
- **Others**: Redis for message brokering, requests library for Mpesa API interaction, Docker for containerization, Docker Compose for setup management.
  
## Project Structure

```
django-mpesa-integration/
├── django_mpesa_integration/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── asgi.py
│   ├── wsgi.py
│   ├── celery.py           # Celery configuration file
│   └── config.py           # (New) Add this file for configuration handling (e.g., environment variables)
├── payments/
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── models.py
│   ├── tasks.py           # Celery tasks related to Mpesa integration
│   ├── views.py
│   ├── urls.py
│   ├── templates/
│   │   └── payment_form.html
│   ├── static/
│   │   ├── js/
│   │   └── css/
│   └── migrations/
│       └── __init__.py
├── Dockerfile              # (New) Dockerfile for containerization
├── docker-compose.yml      # (New) Docker Compose file for setting up Redis and Celery
├── manage.py
├── requirements.txt        # (New) Updated with necessary dependencies for Mpesa, Celery, Redis, etc.
├── db.sqlite3              # (Database file if using SQLite; if using another DB, this will be different)
├── .env                    # (New) Environment variables file for secure configuration (API keys, credentials, etc.)
└── README.md               # Updated project documentation

```
## Installation

### 1. Clone the Repository

```bash
git clone https://github.com/OumaCavin/django_mpesa_integration.git
cd django_mpesa_integration
```

### 2. Create a Virtual Environment

Create and activate a virtual environment for the project:

```bash
python -m venv mpesa_env
mpesa_env\Scripts\activate  # For Windows
source mpesa_env/bin/activate  # For macOS/Linux
```

### 3. Install Dependencies

Install the required Python packages:

```bash
pip install -r requirements.txt
```

This will install:

- `django`: The web framework for the application
- `celery`: The background task queue
- `redis`: The message broker for Celery
- `requests`: To handle HTTP requests to the Mpesa API

### 4. Set Up Environment Variables

Create a `.env` file in the root of the project and add the necessary environment variables for secure configuration:

```bash
MPESA_LIPA_NA_MPESA_SHORTCODE=your_shortcode
MPESA_LIPA_NA_MPESA_SHORTCODE_SECRET=your_shortcode_secret
MPESA_LIPA_NA_MPESA_SHORTCODE_LIPA_NA_MPESA_SECURITY_KEY=your_security_key
MPESA_LIPA_NA_MPESA_SHORTCODE_LIPA_NA_MPESA_LIPA_NA_MPESA_SHORTCODE_LIPA_NA_MPESA_CLIENT_KEY=your_client_key
REDIS_URL=redis://localhost:6379/0
```

Make sure to replace the placeholders with actual values from your Mpesa account and Redis setup.

### 5. Migrate the Database

Run the Django migrations to set up the database schema:

```bash
python manage.py migrate
```

### 6. Start the Redis Server

Ensure Redis is running by starting it:

```bash
redis-server
```

You can download and install Redis from the [official Redis website](https://redis.io/download) if it's not already installed.

### 7. Start Celery Worker

Open a new terminal window, activate your virtual environment, and run Celery:

```bash
celery -A django_mpesa_integration.celery worker --loglevel=info
```

### 8. Run the Django Development Server

Start the Django development server:

```bash
python manage.py runserver
```

This will run the application at `http://127.0.0.1:8000/`.

### 9. Testing the Mpesa Integration

Test the integration by triggering an Mpesa payment request from the web interface. Make sure the Celery worker is running to handle tasks asynchronously.

## Background Task Processing with Celery

This project uses Celery to process tasks such as handling Mpesa payment callbacks in the background. Ensure that you have a Redis server running and Celery worker active to process these tasks.

### 1. Start Redis Server
Make sure the Redis server is running before starting Celery. You can use the following command to start the Redis server:

```bash
redis-server
```

### 2. Start Celery Worker
To start the Celery worker for background task processing:

```bash
celery -A django_mpesa_integration.celery worker --loglevel=info
```

## Configuration

The following settings need to be configured in the Django settings file (`settings.py`):

```python
# Mpesa API Configuration
MPESA_LIPA_NA_MPESA_SHORTCODE = os.getenv("MPESA_LIPA_NA_MPESA_SHORTCODE")
MPESA_LIPA_NA_MPESA_SHORTCODE_SECRET = os.getenv("MPESA_LIPA_NA_MPESA_SHORTCODE_SECRET")
MPESA_LIPA_NA_MPESA_SECURITY_KEY = os.getenv("MPESA_LIPA_NA_MPESA_SECURITY_KEY")
MPESA_LIPA_NA_MPESA_CLIENT_KEY = os.getenv("MPESA_LIPA_NA_MPESA_CLIENT_KEY")

# Celery Configuration
CELERY_BROKER_URL = os.getenv("REDIS_URL", "redis://localhost:6379/0")
CELERY_RESULT_BACKEND = os.getenv("REDIS_URL", "redis://localhost:6379/0")

# Redis Configuration (for Celery)
REDIS_URL = os.getenv("REDIS_URL", "redis://localhost:6379/0")
```

## Troubleshooting

- **Permission Error**: If you encounter permission issues when running the worker (`PermissionError: [WinError 5] Access is denied`), try running your terminal as an administrator or check the permissions of the files being accessed.
- **Redis Connection Error**: Make sure the Redis server is running and that the `REDIS_URL` environment variable is correctly set.
  
## Contributing

Feel free to submit pull requests for any improvements or bug fixes. Please ensure that your code follows the project's code style.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### **Source Code**

To learn more about the Django Mpesa Integration Project check out my:

**[Project Source code](https://github.com/OumaCavin/mpesa-django-integration/tree/mpesa-integration)**.
