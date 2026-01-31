# Quick start (FastAPI/Starlette)

Use this as a minimal pattern to wire SQLAdmin into a FastAPI or Starlette app.

## Install
- `pip install sqladmin`

## Minimal setup (sync engine)
- Create SQLAlchemy engine and models.
- Initialize `Admin(app, engine)`.
- Add `ModelView` classes for models.

Example (simplified):

```python
from fastapi import FastAPI
from sqlalchemy import create_engine
from sqladmin import Admin, ModelView

app = FastAPI()
engine = create_engine("sqlite:///example.db")

class UserAdmin(ModelView, model=User):
    column_list = [User.id, User.email]

admin = Admin(app, engine)
admin.add_view(UserAdmin)
```

## Session maker option
If you already manage sessions, pass `session_maker` to `Admin` instead of just `engine`.

## Async engine option
SQLAdmin supports async SQLAlchemy engines. Use `create_async_engine` and pass the async engine to `Admin`.

See the project README and docs for full examples and async setup details.
