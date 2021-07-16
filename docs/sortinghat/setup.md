# How to setup SortingHat

## Requirements

- Python >= 3.6
- Poetry >= 1.1.0
- MySQL >= 5.7 or MariaDB 10.0
- Django = 3.1
- Graphene-Django >= 2.0
- uWSGI >= 2.0

You will also need some other libraries for running the tool, you can find the
whole list of dependencies in [pyproject.toml](https://github.com/chaoss/grimoirelab-sortinghat/blob/muggle/pyproject.toml) file.

## Installation

### Getting the source code

Clone the repository, and change to the `muggle` branch

```
$ git clone https://github.com/chaoss/grimoirelab-sortinghat
$ git checkout muggle
```

### Backend

#### Prerequisites

##### Poetry

We use [Poetry](https://python-poetry.org/docs/) for managing the project.
You can install it following [these steps](https://python-poetry.org/docs/#installation).

##### mysql_config

Before you install SortingHat tool you might need to install `mysql_config`
command. If you are using a Debian based distribution, this command can be
found either in `libmysqlclient-dev` or `libmariadbclient-dev` packages
(depending on if you are using MySQL or MariaDB database server). You can
install these packages in your system with the next commands:

- **MySQL**

```
$ apt install libmysqlclient-dev
```

- **MariaDB**

```
$ apt install libmariadbclient-dev
```

#### Installation and configuration

Install the required dependencies (this will also create a virtual environment).

```
$ poetry install
```

Activate the virtual environment:

```
$ poetry shell
```

Migrations, fixtures and create a superuser:

```
(.venv)$ ./manage.py makemigrations --settings=config.settings.devel
(.venv)$ ./manage.py migrate --settings=config.settings.devel
(.venv)$ ./manage.py loaddata sortinghat/core/fixtures/countries.json --settings=config.settings.devel
(.venv)$ ./manage.py createsuperuser --settings=config.settings.devel
```

#### Running the backend

Run SortingHat backend Django app:

```
(.venv)$ ./manage.py runserver --settings=config.settings.devel
```

### Frontend

#### Prerequisites

##### yarn

To compile and run the frontend you will need to install `yarn` first.
The latest versions of `yarn` can only be installed with `npm` - which
is distributed with [NodeJS](https://nodejs.org/en/download/).

When you have `npm` installed, then run the next command to install `yarn`
on the system:

```
npm install -g yarn
```

Check the [official documentation](https://yarnpkg.com/getting-started)
for more information.

#### Installation and configuration

Install the required dependencies

```
$ cd ui/
$ yarn install
```

#### Running the frontend

Run SortingHat frontend Vue app:

```
$ yarn serve
```

## SortingHat service

Starting at version 0.8, SortingHat is released with a server app. The server has two
modes, `production` and `development`.

When `production` mode is active, a WSGI app is served. The idea is to use a reverse
proxy like NGINX or similar, that will be connected with the WSGI app to provide
an interface HTTP.

When `development` mode is active, an HTTP server is launched, so you can interact
directly with SortingHat using HTTP requests. Take into account this mode is not
suitable nor safe for production.

You will need a django configuration file to run the service. You can use and modify
one of the ones stored in `config/settings` folder. The file must be accessible
via `PYTHONPATH` env variable. For the next examples, we will use `devel.py` file.

In order to run the service for the first time, you need to execute the next commands:

Build the UI interface:

```
$ cd ui
$ yarn build
```

Copy the static files to the location where they will be served (`STATIC_ROOT` var):

```
$ ./manage.py collectstatic --settings=config.settings.devel
```

Run the server (use `--dev` flag for `development` mode):

```
$ sortinghatd --config config.settings.devel
```

By default, this runs a WSGI server in `127.0.0.1:6314`. The `--dev` flag runs
a server in `127.0.0.1:8000`.

## Compatibility between versions

SortingHat 0.7.x is not longer supported. Any database using this version will not work.

SortingHat databases 0.7.x are no longer compatible. The `uidentities` table was renamed
to `individuals`. The database schema changed in all tables to add the fields `created_at`
and `last_modified`. Also in `domains`, `enrollments`, `identities`, `profiles` tables,
there are some specific changes to the column names:

- `domains`
  - `organization_id` to `organization`
- `enrollments`
  - `organization_id` to `organization`
  - `uuid` to `individual`
- `identities`
  - `uuid` to `individual`
- `profiles`
  - `country_code` to `country`
  - `uuid` to `individual`

Please update your database following the next steps:

1. Use the script `utils/create_sh_0_7_fixture.py` to create the fixture
   JSON file

   ```
   $ python3 utils/create_sh_0_7_fixture.py test_sh -o test_sh_fixture.json
   [2021-06-10 17:29:11,461][INFO] Start creating fixture file for test_sh
   [2021-06-10 17:29:21,252][INFO] Fixture file created to test_sh_fixture.json
   ```

2. Create a new database.

   ```
   mysql> CREATE DATABASE new_sh CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_520_ci;
   ```

3. Execute Django migrate.

   ```
   $ python3 manage.py migrate --settings=config.settings.devel
   ```

4. Load fixture JSON file using Django
   ```
   $ python3 manage.py loaddata test_sh_fixture.json --settings=config.settings.devel
   Installed 148542 object(s) from 1 fixture(s)
   ```

## Running tests

SortingHat comes with a comprehensive list of unit tests for both
frontend and backend.

#### Backend test suite

```
(.venv)$ ./manage.py test --settings=config.settings.testing
```

#### Frontend test suite

```
$ cd ui/
$ yarn test:unit
```
