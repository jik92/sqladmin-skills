# ModelView configuration

Use these common ModelView options to control admin behavior.

## General metadata
- `name`, `name_plural`: Override displayed model name(s).
- `icon`: Icon class for sidebar.
- `category`: Grouping in sidebar.
- `page_size`: Pagination size for list view.
- `can_create`, `can_edit`, `can_delete`, `can_view_details`, `can_export`: Permissions.

## List view
- `column_list`: Explicit columns for list view.
- `column_exclude_list`: Exclude columns from list view.
- `column_searchable_list`: Enable search for columns.
- `column_sortable_list`: Allow sorting.
- `column_default_sort`: Default sort column(s).
- `column_labels`: Friendly labels for columns.
- `column_formatters`: Custom display formatters.
- `column_formatters_detail`: Formatters for details view.

## Details view
- `column_details_list`: Columns shown in details view.
- `column_details_exclude_list`: Columns hidden in details view.

## Form view
- `form_columns`: Explicit form field order.
- `form_excluded_columns`: Exclude form fields.
- `form_overrides`: Override field type widgets.
- `form_args`: Field-specific arguments (validators, labels, etc.).
- `form_widget_args`: HTML/widget-level overrides.

## Export
- `export_types`: Restrict export formats.
- `export_max_rows`: Maximum export rows.

## Filters
- `column_filters`: Enable filters by columns or custom filters.

## Hooks and actions
- `on_model_change`: Hook before create/update.
- `on_model_delete`: Hook before delete.
- `after_model_change`: Hook after create/update.
- `after_model_delete`: Hook after delete.
- `action`: Register custom list actions.

See docs for full option lists and examples.
