# Hero
FastAPI is a popular package nowadays, and I have decided to share my setup for an async web-server using this
framework. The Hero app repository is an example of ultimate setup for async web-service.

## Dependencies
Here is a short description of python packages used in the article (just to make a whole picture to save your time):

1. [Poetry](https://python-poetry.org) - is a tool for dependency management and packaging in Python. It allows you to
   declare the libraries your project depends on and it will manage (install/update) them for you;
2. [FastAPI](https://fastapi.tiangolo.com) - is a modern, fast (high-performance), web framework for building APIs with
   Python 3.6+ based on standard Python type hints;
3. [Pydantic](https://pydantic-docs.helpmanual.io) - Data validation and settings management using Python type hinting;
4. [SQLAlchemy](https://www.sqlalchemy.org) - SQLAlchemy is the Python SQL toolkit and Object Relational Mapper that
   gives application developers the full power and flexibility of SQL;
5. [SQLModel](https://sqlmodel.tiangolo.com) - SQLModel is a library for interacting with SQL databases from Python
   code, with Python objects;
6. [Alembic](https://alembic.sqlalchemy.org/en/latest/) - Alembic is a lightweight database migration tool for usage
   with the SQLAlchemy Database Toolkit for Python.

## mysql 
`docker run --name=mysql1 -p 3307:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql/mysql-server:8.0
`
then enter into the container `docker exec -it [container-id] bash`
then log into mysql `mysql -u root -p`
create DB
create user `CREATE USER 'heroes_my'@'%' IDENTIFIED BY 'heroes_my';`
and then grant privileges 
`GRANT ALL ON *.* TO 'heroes_my'@'%';`
`FLUSH PRIVILEGES;`

## env file
update environment variables. for example mysql url will be like `mysql+asyncmy://heroes_my:heroes_my@0.0.0.0:3307/heroes_db`

## Alembic Migration and commands
Alembic Initilization 
`alembic init -t async migrations`

Alembic migration file generation `alembic revision --autogenerate -m "heroes"`

Alembic run migration `alembic upgrade head`

## Deployment
Use this command to build Docker container: `docker build --build-arg ENV_FILE=".env" -t hero-app -f Dockerfile .`

And this command to start container: `docker run -d -p "8080:80" --name hero-app hero-app`


## poetry related commands
add plugin: `poetry add [plugin-name]`

add plugin under specific group: `poetry add [plugin-name] --group [group name]`

install plugins from pyproject file: `poetry install`

remove plugin: `poetry remove [plugin-name]`


Source: https://medium.com/@estretyakov/the-ultimate-async-setup-fastapi-sqlmodel-alembic-pytest-ae5cdcfed3d4
