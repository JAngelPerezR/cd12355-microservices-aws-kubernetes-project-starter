FROM python:3.12-slim

ENV DB_USERNAME $DB_USERNAME
ENV DB_PASSWORD $DB_PASSWORD
ENV DB_HOST $DB_HOST
ENV DB_PORT $DB_PORT
ENV DB_NAME $DB_NAME

COPY . app

WORKDIR app

RUN apt update -y && \
    apt install build-essential libpq-dev -y && \
    pip install --upgrade pip setuptools wheel && \
    pip install -r requirements.txt

CMD python app.py
