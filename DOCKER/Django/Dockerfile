FROM python:3.9-alpine
LABEL AUTHOR="Litesh Garg" version='1.0'

ENV PYTHONNUMBUFFERED 1


COPY ./requirements /requirements
RUN apk add --update --no-cache postgresql-client jpeg-dev
RUN apk add --update --no-cache --virtual .temp-build-deps \
    gcc libc-dev linux-headers postgresql-dev musl-dev zlib zlib-dev
RUN pip install -r /requirements/local.txt
RUN apk del .temp-build-deps

RUN mkdir /app
WORKDIR /app
COPY ./ /app

RUN mkdir -p /vol/web/media
RUN mkdir -p /vol/web/static

RUN adduser -D djangoUser
RUN chown -R djangoUser:djangoUser /vol/
RUN chmod -R 755 /vol/web
USER djangoUser
