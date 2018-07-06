# Dockerize a Django Application

This guide demonstrates how to use docker and docker compose to setup and run a simple Django/PostgreSQL application.

## Getting Started

For this project we need to have a Dockerfile,a python dependencies (requirements.txt),and docker-compose.yml file.

### Prerequisites

Having Docker and Docker Compose installed.

### Download the sample 

In a terminal window, run the following command to clone the sample app repository to your local machine, then change to the directory that contains the sample code.

```
git clone https://github.com/Taddist/Docker_Django.git
cd Docker_Django
```

## Create Docker Image

In the Git repository, take a look at Dockerfile. This file describes the Python environment that is required to run the application. The file requirements.txt include basic requirements to start and deploy our Django application.

To build the Docker image , run the docker build command 

```
docker-compose build 
```
The command produces output similar to the following:
```
Building web
Step 1/7 : FROM python:3
 ---> ce54ff8f2af6
Step 2/7 : ENV PYTHONUNBUFFERED 1
 ---> Using cache
 ---> 3281e3a9d689
Step 3/7 : RUN mkdir /code
 ---> Using cache
 ---> 2afacc41190a
Step 4/7 : WORKDIR /code
 ---> Using cache
 ---> 33cacd4482d8
Step 5/7 : ADD requirements.txt /code/
 ---> Using cache
 ---> 5483be67f2e1
Step 6/7 : RUN pip3 install -r requirements.txt
 ---> Using cache
 ---> 84c0a3fb3b82
Step 7/7 : ADD . /code/
 ---> 17b941c2ab26
Successfully built 17b941c2ab26
Successfully tagged dockerdjango_web:latest
```
Every time that you modify the elements inside requirements.txt file you should repeat this step.

## Create Django Project
The project is created using the same commands described into Django website.
```
docker-compose run web django-admin.py startproject mydjangoApp
```
This will build the web service's image, once the image is built, Compose runs it and create the django project's directory with files representing the project. You can list those files by :

```
drwxr-xr-x 2 root   root   mydjangoApp
-rw-rw-r-- 1 user   user   docker-compose.yml
-rw-rw-r-- 1 user   user   Dockerfile
-rwxr-xr-x 1 root   root   manage.py
-rw-rw-r-- 1 user   user   requirements.txt
```
Now we have a new directory named mydjangoApp, but it's protected because Docker runs with the root privilege.

```
sudo chown -R $USER:$USER .

```


## Setup the database 
Edit the mydjangoApp/settings.py file. Replace the DATABASES = ... with the following :

```
  DATABASES = {
    'default': {
      'ENGINE': 'django.db.backends.postgresql_psycopg2',
      'NAME': 'postgres',
      'USER': 'postgres',
      'HOST': 'db',
      'PORT': 5432,
    }
  }
```
These settings are determined by the postgres Docker image specified in docker-compose.yml.
## Test the system
At this point we're ready to take a look at our empty application. Run docker-compose up to start the Django server.
```
docker-compose up 
```
Congratulation now your Django app is up and running on port 8000 on your localhost. 
