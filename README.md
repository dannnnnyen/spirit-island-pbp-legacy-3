# Spirit Island PBP Helper

A website to assist playing Spirit Island over discord in the play by post section.

## Pre-requisites

Ensure that you've installed [Python](https://www.python.org/downloads/) and [Poetry](https://python-poetry.org/docs/#installing-with-pipx) before starting.

## Running locally

Copy `.env.template` to `.env` and fill in the variables

```
poetry install --no-root
poetry run ./manage.py migrate auth
poetry run ./manage.py migrate
poetry run ./manage.py collectstatic
poetry run ./manage.py runserver
```

*NOTE*: If running in a Windows shell, instead run the above manage.py commands with the format `poetry run python .\manage.py [...]`. E.g.

```
poetry run python .\manage.py migrate auth
```

## Test

```
poetry run ./manage.py test
```

## Making a new admin account for your instance

```
poetry run ./manage.py createsuperuser
```

## Troubleshooting

If no images are showing up when running locally, consider setting [`DEBUG`](https://docs.djangoproject.com/en/stable/ref/settings/#debug) to True.
In this project, this is done by setting the `DEBUG` environment variable to `yes` (the value that `island/settings.py` is checking for), typically using the `.env` file.
Doing so makes Django serve [static files](https://docs.djangoproject.com/en/stable/howto/static-files/) such as images.

If no images are showing up when running in production, check that you've configured your chosen web server to serve the static files (exact configuration depends on the web server).

If you encounter file not found errors on Windows when running `poetry install` with paths that look similar to the following:

```
C:\Users\username\AppData\Local\Packages\PythonSoftwareFoundation.Python.3.12_qbz5n2kfra8p0\LocalCache\Local\pypoetry\Cache\virtualenvs\spirit-island-zmMjpaKz-py3.12\Lib\site-packages\pkg_resources\tests\data\my-test-package_unpacked-egg\my_test_package-1.0-py3.7.egg\EGG-INFO
```

The problem is likely that the path exceeds Windows' default allowed path length.
You can fix this by launching `regedit`, navigating to `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem`, and editing the `LongPathsEnabled` key from 0 to 1.
