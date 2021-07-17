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
(.venv)$ sortinghat-admin --config=config.settings.devel setup
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
