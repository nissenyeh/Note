# Virtual Environment

## What's Virtual Environment

- A Virtual Environment which can run python.The pip packages is installed in different environment won't disturb each others.

## How to install Virtual Environment

- Create a random file
- create a Virtual Environment 
```vim
python3 -m venv djangogirls_venv // 
```

- swithch to the Virtual Environment 
```vim
source djangogirls_venv/bin/activate 
```

# Django

## Run Server and connect to Database

- Database setting in `.env` file

```py
DB_CONNECTIONS=mysql
DB_HOST=XXX.XXX.X.XXX
DB_PORT=XXXX
DB_DATABASE=maltose-dev
DB_USERNAME=root
DB_PASSWORD=password
```

- Install package which project need

```js
$ source djangogirls_venv/bin/activate 
$ pip install XXXX or
$ pip install -r `requirements/local.txt` 
```

- Run Server
```js
$ python manage.py runserver
```


# Connect to MySQL

