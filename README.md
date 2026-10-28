# FastAPI DevOps Starter

A minimal FastAPI application with a health endpoint and an automated test.

## Project files

- `app/__init__.py`: marks the application directory as a Python package.
- `app/main.py`: creates the FastAPI application and defines `GET /health`.
- `tests/test_health.py`: verifies HTTP 200 and the expected JSON response.
- `requirements.txt`: pins the application and test dependencies.
- `.gitignore`: excludes local environments, caches, and environment secrets.

## Local setup

Use Python 3.11 or 3.12. Run the following commands from the repository root
in a Linux or macOS shell:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
```

FastAPI provides the web framework, Uvicorn runs the server, pytest runs the
tests, and HTTPX supports FastAPI's test client.

## Run the application

With the virtual environment activated, run:

```bash
python -m uvicorn app.main:app --reload
```

Open <http://127.0.0.1:8000/health> in your browser, or use another terminal:

```bash
curl -i http://127.0.0.1:8000/health
```

Expect HTTP `200 OK` and this JSON body:

```json
{"status":"ok"}
```

Interactive API documentation is available at <http://127.0.0.1:8000/docs>.
Use Ctrl+C to stop the server. The `--reload` option is for local development.

## Run the tests

From the repository root, with the virtual environment activated:

```bash
python -m pytest
```

The test calls the application in process using `TestClient`; you do not need
to start Uvicorn separately. It checks that `GET /health` returns HTTP 200 and
exactly `{"status": "ok"}`.

The health endpoint confirms that the application can respond. It does not
check external services such as databases.
