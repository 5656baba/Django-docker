FROM python:3.9.5 AS python-base

ENV PYTHONUNBUFFERED 1
RUN mkdir /app
WORKDIR /app
ADD requirements.txt /app/
RUN pip install --upgrade pip \
&& pip install -r requirements.txt
COPY . /app/

FROM python:3.9.5-alpine
ENV PYTHONUNBUFFERED 1

RUN mkdir /app
WORKDIR /app
RUN apk add --no-cache --virtual .build-deps \
    gcc \
    make \
    libc-dev \
    musl-dev \
    linux-headers \
    pcre-dev \
    mariadb-dev
COPY --from=python-base /app/requirements.txt /app/
RUN pip install --upgrade pip \
&& pip install -r /app/requirements.txt

COPY . /app/ 
