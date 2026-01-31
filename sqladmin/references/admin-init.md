# Admin initialization options

`Admin` is the main entrypoint for SQLAdmin.

Common initialization options include:
- `app`: Starlette or FastAPI app instance.
- `engine` or `session_maker`: SQLAlchemy engine or sessionmaker (sync or async).
- `base_url`: Base path for admin routes.
- `title`, `logo_url`, `favicon_url`: Branding.
- `middlewares`: Extra middlewares to apply to admin.
- `templates_dir`: Root templates directory used by SQLAdmin.
- `authentication_backend`: Optional `AuthenticationBackend` for login.
- `debug`: Enable debug mode.

Check the SQLAdmin API reference when you need the exact parameter list or defaults.
