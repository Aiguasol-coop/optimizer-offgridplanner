FROM docker.io/python:3.12.9-slim-bookworm

RUN apt-get update && \
    apt-get install -y git && \
    apt-get install coinor-cbc -y && \
    apt-get install graphviz -y

COPY . /app
WORKDIR /app

RUN pip install --upgrade pip \
 && pip install -r requirements.txt

RUN useradd --create-home appuser \
 && chown -R appuser /app
USER appuser

ENV CELERY_TASK_NAME=default

ENTRYPOINT celery -A tasks worker --loglevel=info --queues=${CELERY_TASK_NAME}