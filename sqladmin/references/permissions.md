# Role-based permissions patterns

Use these patterns to implement per-user or per-role access control.

## Model-level access
Override `is_accessible` in your ModelView to enforce role checks:

```python
class UserAdmin(ModelView, model=User):
    def is_accessible(self, request):
        user = request.state.user
        return user and user.role == "admin"
```

## Menu visibility
Hide a view from the sidebar with `is_visible`:

```python
class AuditLogAdmin(ModelView, model=AuditLog):
    def is_visible(self, request):
        user = request.state.user
        return user and user.role in {"admin", "auditor"}
```

## Per-action guards
For custom actions, check permissions inside the action handler and return an error or flash message when unauthorized.

## Shared policy helpers
Extract common permission logic into a helper function or class used by multiple views to keep policies consistent.

## Authentication backend integration
Populate `request.state.user` (or a similar attribute) in your authentication backend so your views can access user context.

## Middleware example (populate request.state.user)
Attach user context early so ModelView methods can read it:

```python
from starlette.middleware.base import BaseHTTPMiddleware

class AuthContextMiddleware(BaseHTTPMiddleware):
    async def dispatch(self, request, call_next):
        # Example: replace with your real auth lookup
        request.state.user = request.session.get("user")
        return await call_next(request)
```

Add this middleware to your app before initializing SQLAdmin so admin routes see `request.state.user`.
