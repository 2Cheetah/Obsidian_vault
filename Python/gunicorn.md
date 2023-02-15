# gunicorn
#wsgi #server #flask

## Start a server with gunicorn and poetry

Let's say a project is created with poetry and has the following structure:
```text
├── gunicorn_training
│   ├── app.py
│   └── __init__.py
├── poetry.lock
├── pyproject.toml
├── README.md
└── tests
    └── __init__.py
```

`flask` and `gunicorn` are installed.

`app.py` has the following code:
```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, World!"
```

To run the server with `gunicorn` it's needed to run the following command from the parent directory:
```bash
poetry run gunicorn app:app --chdir ./gunicorn_training
```

If the following output can be seen, then the server was started successfully:
```text
[2023-02-15 12:36:56 +0800] [16968] [INFO] Starting gunicorn 20.1.0
[2023-02-15 12:36:56 +0800] [16968] [INFO] Listening at: http://127.0.0.1:8000 (16968)
[2023-02-15 12:36:56 +0800] [16968] [INFO] Using worker: sync
[2023-02-15 12:36:56 +0800] [16973] [INFO] Booting worker with pid: 16973
```
