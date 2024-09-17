# djsfc

Stuff needed together should be together.

Ignore folks yelling "html and py in the same file!? WHAT?!".

djsfc is best served with htmx.

## Installation

Add template builtins to your `TEMPLATES` setting like this:

```python
TEMPLATES = [
    {
        ...
        'OPTIONS': {
            'builtins': [
                'djsfc',
            ],
        },
    },
]
```

Add `'djsfc.TemplateLoader'` to your `TEMPLATES` setting like this:

```python
TEMPLATES = [
    {
        ...
        'OPTIONS': {
            'loaders': [
                ...
                'djsfc.TemplateLoader',
            ],
        },
    },
]
```

Create router and a view:

```python
from django.template.response import TemplateResponse
from djsfc import Router, parse_template

router = Router(__name__)
template = parse_template('<p>Hello, {{ name }}!</p>', router)

@router.route('GET', '')
@login_required
def index(request, pk):
    return TemplateResponse(request, template, {'name': 'world'})
```

Add router to your `urlpatterns` setting like this:

```python
from your_view_module import router

urlpatterns = [
    ...
    *router.urls,
]
```

## Python deps for development

This project uses Poetry for dependency management. To install the dependencies, run:

    poetry install

To activate the virtual environment, run:

    poetry shell
