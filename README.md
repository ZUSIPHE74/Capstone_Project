# News System - Django Capstone Project

This is a role-based Django news application with three user types:
- `Reader`: view approved content and subscriptions
- `Journalist`: submit articles for review
- `Editor`: review, approve, and reject submissions

## Core Features
- Custom `User` model with role-based behavior
- Publisher and journalist subscription flow
- Article workflow: `draft -> pending -> approved/rejected`
- Dashboard routing by role after login
- REST API endpoint for subscribed approved articles
- Automated tests for auth, workflow, and API behavior

## Tech Stack
- Python 3.12+
- Django 6.0.2
- Django REST Framework 3.16.1
- SQLite (default)

## Local Setup
1. Open the project root directory (the folder containing `manage.py`, `news_project`, and `news_app`).

2. Create and activate a virtual environment:
```bash
python -m venv .venv
# Windows
.\.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Apply migrations:
```bash
python manage.py migrate
```

5. Start the app:
```bash
python manage.py runserver
```

Open: http://127.0.0.1:8000/

## Project Structure
- Active project path: project root (`manage.py`, `news_project/`, `news_app/`, `templates/`).
- Included legacy copy: `news_system/` (kept for reference/history; not the active runtime path).

If your machine reports `attempt to write a readonly database`, set a writable SQLite path:
```bash
# Windows PowerShell
$env:SQLITE_DB_PATH='db_test.sqlite3'
python manage.py migrate
python manage.py runserver
```

## Demo Accounts
These accounts are auto-created on login page load:
- `reader_demo` / `DemoPass123!`
- `journalist_demo` / `DemoPass123!`
- `editor_demo` / `DemoPass123!`

## Secrets and Configuration
- This project currently uses a demo `SECRET_KEY` for review purposes.
- Do not commit real production secrets or access tokens to a public repository.
- If you deploy this app, replace sensitive values using environment variables.

## Run Tests
```bash
python manage.py test
```

## Docker
Build:
```bash
docker build -t news-system .
```

Run:
```bash
docker run --rm -p 8123:8000 news-system
```

The container runs migrations on startup, then serves the app on port `8000`.
Open in browser: `http://127.0.0.1:8123/`

## Sphinx Documentation
Generated documentation is included in the repository under:
- `docs/html/index.html`

To regenerate docs locally:
```bash
pip install -r docs/requirements.txt
sphinx-build -b html docs docs/html
```

## API
- `GET /api/articles/`
- Requires authenticated session
- Returns approved articles from subscribed publishers or followed journalists
