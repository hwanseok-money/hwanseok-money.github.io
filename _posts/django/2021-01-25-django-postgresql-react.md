---
title: "[Django] Django, PostgreSQL, React 연동하는 방법"
excerpt: "Django+React+DB프로젝트의 기본 템플릿"
date: 2021-01-25
last_modified_at:
categories:
  - Django
tags:
  - Django
  - The Insta
toc : true
toc_label: "Table of contents"
toc_icon: "list"  # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: false
---

**Info Notice:**  
안녕하세요. **HwanSeok**입니다.  
{: .notice--info}

# venv

## Create venv

```shell
cd {project root}
mkdir venvs
cd venvs
python -m venv thereact
cd bin
pwd # /home/niklasjang/pycharm_projects/venvs/thereact/bin
```

## Apply alias

Update ~/.bashrc  

```shell
vi ~/.bashrc
```

In ~/.bashrc    

```shell 
(... default settings...)
# Add Below
alias activate=". /home/niklasjang/pycharm_projects/venvs/thereact/bin/activate"
```

Activate venv  

```shell
cd {project root}

activate 
```

Output  

```shell
(thereact) niklasjang@niklasjang-ultrabook:~/pycharm_projects/The-Insta$ 
```

# Database(postgresql) 

## Install

<https://www.postgresql.org/download/linux/ubuntu/>  

```shell
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get -y install postgresql
```

## Log in as default user

<https://docs.boundlessgeo.com/suite/1.1.1/dataadmin/pgGettingStarted/firstconnect.html#setting-a-password-for-the-postgres-user>

```shell
sudo -u postgres psql postgres
\password 'user password'
\q
```

## Create user, database

```shell
sudo -u postgres psql

create database 'theinsta';
CREATE USER 'hwanseok' WITH PASSWORD 'password';
ALTER ROLE 'hwanseok' SET client_encoding TO 'utf8'; 
ALTER ROLE 'hwanseok' SET default_transaction_isolation TO 'read committed'; 
ALTER ROLE 'hwanseok' SET TIME ZONE 'Asia/Seoul';
GRANT ALL PRIVILEGES ON DATABASE 'theinsta' 명 To 'hwanseok';
```  

# Django Project

## Create Project

```shell
cd {project root}
mkdir The-Insta
cd The-Insta
django-admin startproject config .
tree
```

Output  

```shell
(thereact) niklasjang@niklasjang-ultrabook:~/pycharm_projects/The-Insta$ tree
.
├── LICENSE
├── README.md
├── __pycache__
│   ├── dev_settings.cpython-38.pyc
│   └── manage.cpython-38.pyc
├── config
│   ├── __init__.py
│   ├── __pycache__
│   │   ├── __init__.cpython-38.pyc
│   │   ├── settings.cpython-38.pyc
│   │   ├── urls.cpython-38.pyc
│   │   └── wsgi.cpython-38.pyc
│   ├── asgi.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── dev_settings.py
└── manage.py
```  

## Hide SECRET_KEY, Set database

```shell
# config/settings.py
try:
    from dev_settings import *
except ImportError:
    pass
```

```shell
# ./dev_settings.py

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = '********************'
# Database
# https://docs.djangoproject.com/en/3.1/ref/settings/#databases
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': '**********',
        'USER': '**********',
        'PASSWORD': '**********',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

## prerequisite for react

```shell
pip install djangorestframework django-cors-headers
```

```python
# config/settings.py

# Application definition
INSTALLED_APPS = [
    ... omit ... 
    'corsheaders',            # add this
    'rest_framework',         # add this
    '{app name}',                   # django-admin startapp {app name}
  ]

MIDDLEWARE = [
    'corsheaders.middleware.CorsMiddleware',    # add this
    ... omit ...
]


CORS_ORIGIN_WHITELIST = ( # add this
    'http://localhost:3000', # Local React app addr. It must be http. Not https
)

LANGUAGE_CODE = 'ko-kr' # change this

TIME_ZONE = 'Asia/Seoul' # change this
```


# Migrate Django with Database

```shell
sudo apt install libpq-dev
pip install psycopg2
python manage.py migrate
python manage.py runserver
```

```shell
# Ouput
System check identified no issues (0 silenced).
January 25, 2021 - 07:21:52
Django version 3.1.5, using settings 'config.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

# React Client

## Create React Project

```shell
npm install -g create-react-app
create-react-app the-insta-client
```

## Install yarn

```shell
npm install --global yarn
``` 

## Test Start

```shell
cd the-insta-client
yarn start
```  

## Settings CSS, JS

```shell
yarn add bootstrap reactstrap
mkdir src/components
touch src/components/Modal.js
yarn add axios
```

1. [/src/index.css][1]
1. [/src/index.js][2]
1. [/src/components/Modal.js][3]
1. [/src/App.js][4]
1. [/src/serviceWorker.js][5]


## Add Proxy

```json
// /package.json
[...]       
"name": "frontend",
"version": "0.1.0",
"private": true,
"proxy": "http://localhost:8000", // add this
"dependencies": {
  "axios": "^0.18.0",
  "bootstrap": "^4.1.3",
  "react": "^16.5.2",
  "react-dom": "^16.5.2",
  "react-scripts": "2.0.5",
  "reactstrap": "^6.5.0"
},
[...]
```

## Axios test

Restart the development server for the proxy to register with the application.

```shell
axios.get("/api/todos/")
axios.get("http://localhost:8000/api/todos/")
yarn start
```

**Success Notice:**
{: .notice--success}

# 개발환경

- ubuntu 20.04
- python 3.8.5
- django 3.1.5
- pip 20.0.2
- yarn 1.22.10


[1]: https://github.com/hwanseok-dev/the-insta-client/blob/v1.0/src/index.css
[2]: https://github.com/hwanseok-dev/the-insta-client/blob/v1.0/src/index.js
[3]: https://github.com/hwanseok-dev/the-insta-client/blob/v1.0/src/components/Modal.js
[4]: https://github.com/hwanseok-dev/the-insta-client/blob/v1.0/src/App.js
[5]: https://github.com/hwanseok-dev/the-insta-client/blob/v1.0/src/serviceWorker.js