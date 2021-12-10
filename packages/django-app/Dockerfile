FROM python:3.9-slim as base
ENV PYTHONUNBUFFERED 1

# install pipenv and compilation dependencies
# https://cryptography.io/en/latest/installation/
RUN apt-get update && apt-get install -y build-essential libssl-dev libffi-dev python3-dev cargo
RUN pip install --upgrade pip

# install python dependencies
RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code
RUN pip install -r requirements.txt

# install application into container
COPY . /code

# run application
EXPOSE 8000

WORKDIR /code/app

# this CMD is overridden by the command in docker-compose.yml for local development
CMD /code/bin/wait-for-it.sh db:5432 -- python /code/app/manage.py runserver 0.0.0.0:8000
