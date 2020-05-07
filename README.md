# PyBuilder Archetype API Plugin

This plugin generates a structure for a project that requieres endpoints (APIs or web services). This plugin needs
[pybuilder_archetype_base](https://github.com/yeuk0/pybuilder-archetype-base) due to its dependancy with one of its
tasks (`create_archetype_api`).

In the following diagram there is every directory and file created during `create_archetype_api` execution (take note
 that `create_archetype_base` task will add more packages and directories -check its `README.md` file for more
 information):

```text
src
└── package_name
    ├── api  # For every script related with the web services
    |   ├── __init__.py
    |   └── api_example.py
    ├── config
    |   ├── __init__.py
    |   └── constants.py
    ├── __init__.py
    ├── gunicorn_config.py  # Gunicorn launching configuration
    ├── main.py  # Script with Flask app
    └── wsgi.py  # WSGI file for server launch
requirements.txt
```

Content from `requirements.txt` and `constants.py` files will be added to the currently existing ones, trying to keep
 the values set by other plugins.

## How to use pybuilder_archetype_api

> **NOTICE**: This plugin only works on Windows due to its dependency with pybuilder_archetype_base PyBuilder plugin.
Using this plugin in other OS shall not work properly. Multi-platform support soon.

Add plugin dependencies to your `build.py` (it requires [pybuilder_archetype_base](https://github.com/yeuk0/pybuilder-archetype-base) and [pybuilder_pycharm_workspace](https://github.com/yeuk0/pybuilder-pycharm-workspace)
to work properly):

```python
use_plugin('pypi:pybuilder_pycharm_workspace')
use_plugin('pypi:pybuilder_archetype_base')
use_plugin('pypi:pybuilder_archetype_api')
```

Configure the plugin within your `init` function:

```python
@init
def initialise(project):
    project.set_property('project_base_path', project_path)
```

This will tell the plugin which is the project location in the filesystem. `project_base_path` property value should
 be always the same.

Launch the task with:

```console
(venv) C:\Users\foo\PycharmProjects\bar> pyb_ create_archetype_api
```

### `build.py` file recommended

Check [pybuilder_archetype_base `build.py` recommendation](https://github.com/yeuk0/pybuilder-archetype-base#buildpy-file-recommended).

## Properties

Plugin has next properties with provided defaults

| Name | Type | Default Value | Description |
| --- | --- | --- | --- |
| project_base_path | Path | None | Project's path in filesystem (same as `build.py` file). Mandatory |
