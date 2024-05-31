FROM python:3.11-slim

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /code

RUN apt-get update && apt-get install -y openssl

RUN pip install django django-sslserver

COPY . /code/
WORKDIR /code

RUN mkdir -p ssl
RUN bash -c openssl req -x509 -newkey rsa:4096 -keyout ssl/key.pem -out ssl/cert.pem -days 365 -nodes

EXPOSE 8000
CMD ["python", "manage.py", "runsslserver", "0.0.0.0:8000", "--certificate", "/code/ssl/cert.pem", "--key", "/code/ssl/key.pem"]
