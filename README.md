# Flask-Admin

Flask-Admin is now part of Pallets-Eco, an open source organization managed by the
Pallets team to facilitate community maintenance of Flask extensions. Please update
your references to `https://github.com/pallets-eco/flask-admin.git`.

[![image](https://d322cqt584bo4o.cloudfront.net/flask-admin/localized.svg)](https://crowdin.com/project/flask-admin) [![image](https://github.com/pallets-eco/flask-admin/actions/workflows/tests.yaml/badge.svg?branch=master)](https://github.com/pallets-eco/flask-admin/actions/workflows/test.yaml)

## Pallets Community Ecosystem

> [!IMPORTANT]\
> This project is part of the Pallets Community Ecosystem. Pallets is the open
> source organization that maintains Flask; Pallets-Eco enables community
> maintenance of related projects. If you are interested in helping maintain
> this project, please reach out on [the Pallets Discord server][discord].

## Introduction

Flask-Admin is a batteries-included, simple-to-use
[Flask](https://flask.palletsprojects.com/) extension that lets you add admin
interfaces to Flask applications. It is inspired by the *django-admin*
package, but implemented in such a way that the developer has total
control over the look, feel, functionality and user experience of the resulting
application.

Out-of-the-box, Flask-Admin plays nicely with various ORM\'s, including

- [SQLAlchemy](https://www.sqlalchemy.org/)
- [pymongo](https://pymongo.readthedocs.io/)
- and [Peewee](https://github.com/coleifer/peewee).

It also boasts a simple file management interface and a [Redis client](https://redis.io/) console.

The biggest feature of Flask-Admin is its flexibility. It aims to provide a
set of simple tools that can be used to build admin interfaces of
any complexity. To start off, you can create a very simple
application in no time, with auto-generated CRUD-views for each of your
models. Then you can further customize those views and forms as
the need arises.

Flask-Admin is an active project, well-tested and production-ready.

## Examples

Several usage examples are included in the */examples* folder. Please add your own, or improve on the existing examples, and submit a *pull-request*.

### How to run this example

Clone the repository and navigate to this example:

```shell
git clone https://github.com/pallets-eco/flask-admin.git
cd flask-admin/examples/sqla
```

> This example uses [`uv`](https://docs.astral.sh/uv/) to manage its dependencies and developer environment.

Run the example using `uv`, which will manage the environment and dependencies automatically:

```shell
uv run main.py
```

Check the Flask app running on <http://localhost:5000>.

The first time you run this example, a sample sqlite database gets populated automatically. To suppress this behaviour, comment the following lines in main.py:

```python
if not os.path.exists(database_path):
    with app.app_context():
        build_sample_db()
```

## Documentation

Flask-Admin is extensively documented, you can find all of the
documentation at <https://flask-admin.readthedocs.io/en/latest/>.

The docs are auto-generated from the *.rst* files in the */doc* folder.
If you come across any errors or if you think of anything else that
should be included, feel free to make the changes and submit a *pull-request*.

To build the docs in your local environment, from the project directory:

```shell
tox -e docs
```

## Installation

To install Flask-Admin using pip, simply:

```shell
pip install flask-admin
```

## Contributing

If you are a developer working on and maintaining Flask-Admin, checkout the repo by doing:

```shell
git clone https://github.com/pallets-eco/flask-admin.git
cd flask-admin
```

Flask-Admin uses [`uv`](https://docs.astral.sh/uv/) to manage its dependencies and developer environment. With
the repository checked out, to install the minimum version of Python that Flask-Admin supports, create your
virtual environment, and install the required dependencies, run:

```shell
uv sync
```

This will install Flask-Admin but without any of the optional extra dependencies, such as those for sqlalchemy
or mongoengine support. To install all extras, run:

```shell
uv sync --extra all
```

## Tests

Tests are run with *pytest*. If you are not familiar with this package, you can find out more on [their website](https://pytest.org/).

In order for the full test suite to pass, you will need to have all of Flask-Admin's optional extras install. Run:

```shell
uv sync --extra all
```

Then, to run the tests, simply run this command from the project's directory:

```shell
uv run pytest
```

You should see output similar to:

    .............................................
    ----------------------------------------------------------------------
    Ran 102 tests in 13.132s

    OK

**NOTE!** For all the tests to pass successfully, you'll need several services running locally:
Postgres (with the postgis and hstore extension), MongoDB, and Azurite.
You'll also need *libgeos* available.
See tests.yaml for Docker configuration and follow service-specific setup below.

## Setting up local Postgres for tests

```shell
psql postgres
> CREATE DATABASE flask_admin_test;
> # Connect to database "flask_admin_test":
> \c flask_admin_test;
> CREATE EXTENSION postgis;
> CREATE EXTENSION hstore;
```

If you\'re using Homebrew on MacOS, you might need this:

```shell
# Install postgis and geos
brew install postgis
brew install geos

# Set up a PostgreSQL user
createuser -s postgresql
brew services restart postgresql
```

## Setting up Azure Blob Storage emulator for tests

1. Run the [Azurite emulator](https://learn.microsoft.com/azure/storage/common/storage-use-azurite?tabs=visual-studio%2Cblob-storage)

2. Set the connection string for the emulator:

```shell
export AZURE_STORAGE_CONNECTION_STRING="DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;"
```

You can also run the tests on multiple environments using *tox*.

## 3rd Party Stuff

Flask-Admin is built with the help of
[Bootstrap](https://getbootstrap.com/),
[Select2](https://github.com/ivaynberg/select2) and
[Bootswatch](https://bootswatch.com/).

If you want to localize your application, install the
[Flask-Babel](https://pypi.python.org/pypi/Flask-Babel) package.

You can help improve Flask-Admin\'s translations through Crowdin:
<https://crowdin.com/project/flask-admin>

<!-- refs -->
[discord]: https://discord.gg/pallets
