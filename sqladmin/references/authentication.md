# Authentication and access control

SQLAdmin uses an `AuthenticationBackend` to protect the admin UI.

## Required pieces
- Create a class that inherits `AuthenticationBackend`.
- Implement:
  - `login(request)`: Validate credentials and set session state.
  - `logout(request)`: Clear session state.
  - `authenticate(request)`: Return `True`/`False` to allow access.

Typical pattern:
- Use a signed session cookie (provide `secret_key` to the backend).
- Store a flag like `request.session["token"]` on login.
- Check the flag in `authenticate`.

## Wiring into Admin
Pass the backend to `Admin`:
- `Admin(app, engine, authentication_backend=AuthBackend(secret_key="..."))`

## Per-view access
Override in a ModelView:
- `is_accessible(request)` to control access to that view.
- `is_visible(request)` to hide it from the menu.

Use these to implement role-based access control or per-model restrictions.
