# Async SQLAlchemy setup

Use these patterns when your FastAPI app uses SQLAlchemy async engines and sessions.

## Engine and sessionmaker
- Create an async engine with `create_async_engine`.
- Create an async sessionmaker (often `async_sessionmaker` in SQLAlchemy 2.x).
- Pass the async engine or sessionmaker into `Admin`.

Minimal outline:

```python
from sqlalchemy.ext.asyncio import create_async_engine, async_sessionmaker
from sqladmin import Admin

engine = create_async_engine("postgresql+asyncpg://user:pass@host/db")
SessionLocal = async_sessionmaker(engine, expire_on_commit=False)

admin = Admin(app, engine)
# or admin = Admin(app, session_maker=SessionLocal)
```

## Async hooks example
When using an async session, make hooks `async def` and await DB operations:

```python
from sqladmin import ModelView

class UserAdmin(ModelView, model=User):
    async def on_model_change(self, data, model, is_created, request):
        # Example: normalize email before save
        if "email" in data and data["email"]:
            data["email"] = data["email"].lower()
```

## Gotchas
- Ensure your models are defined with SQLAlchemy 2.x style if your app uses 2.x.
- Use a compatible async driver (e.g., `asyncpg` for Postgres, `aiosqlite` for SQLite).
- Keep sync and async engines separate; do not mix them in the same Admin instance.
