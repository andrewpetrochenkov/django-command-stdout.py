[![](https://img.shields.io/badge/released-2021.6.21-green.svg?longCache=True)](https://pypi.org/project/django-command-stat/)
[![](https://img.shields.io/badge/license-Unlicense-blue.svg?longCache=True)](https://unlicense.org/)

### Installation
```bash
$ pip install django-command-stat
```

### How it works
collected statistics:
+   calls count
+   errors count
+   cpu time
+   memory
+   started, finished time

implementations:
+   `StatCommand` management command class
+   `@command_stat` decorator

#### `settings.py`
```python
INSTALLED_APPS+=['django_command_stat']
```

#### `migrate`
```bash
$ python manage.py migrate
```

### Examples
`StatCommand`
```python
from django_command_stat.management.base import StatCommand

class Command(StatCommand):
    def handle(self,*args,**options):
        # your code
```

`@command_stat` decorator
```python
from django_command_stat.decorators import command_stat

class Command(BaseCommand):
    @command_stat
    def handle(self,*args,**kwargs):
        ...
```

```python
class BaseCommand(BaseCommand):
    def execute(self,*args,**kwargs):
        return command_stat(self.handle)(self,*args,**kwargs)
```

```python
from django.core.management import call_command

command_stat(call_command)(name,*args,**options)
```

