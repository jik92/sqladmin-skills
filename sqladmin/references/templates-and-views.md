# Templates and custom views

## Template overrides
- SQLAdmin uses Jinja2 templates. You can override them by providing your own templates directory.
- Common override points include list, create, edit, and details views.

Approach:
1) Create a `templates/sqladmin/` directory in your project.
2) Copy the template you want to override from SQLAdmin and edit it.
3) Set `templates_dir` on `Admin` if you use a non-default templates location.

## Per-view templates
You can set view-specific templates on a ModelView, for example:
- `list_template`
- `create_template`
- `edit_template`
- `details_template`

## Custom pages
Create a custom admin page by extending `BaseView` and using `@expose`:

```python
from sqladmin import BaseView, expose

class ReportsView(BaseView):
    name = "Reports"
    icon = "fa-solid fa-chart-line"

    @expose("/", methods=["GET"])
    async def index(self, request):
        return await self.templates.TemplateResponse(
            request,
            "sqladmin/reports.html",
            {"stats": {"users": 120}},
        )
```

Register the view with `admin.add_view(ReportsView)`.
