FROM python:2.7

ENV PYTHONUNBUFFERED 1


RUN apt-get update && apt-get install -y \
    git \
    fabric \
    python-setuptools \
    python-dev \
    libxml2-dev \
    libxslt1-dev \
    gcc \
    python-pip \
&& rm -rf /var/lib/apt/lists/*

RUN groupadd -r django \
    && useradd -r -g django django

COPY ./deploy/compose/lrsapp/gunicorn.sh ./deploy/compose/lrsapp/entrypoint.sh /
RUN sed -i 's/\r//' /entrypoint.sh \
    && sed -i 's/\r//' /gunicorn.sh \
    && chmod +x /entrypoint.sh \
    && chown django /entrypoint.sh \
    && chmod +x /gunicorn.sh \
    && chown django /gunicorn.sh

COPY . /app
COPY ./deploy/settings.ini.tmpl /app/adl_lrs/settings.ini

COPY ./requirements /requirements
RUN pip install --no-cache-dir -r /requirements/docker.txt \
    && rm -rf /requirements

RUN chown -R django /app \
    && mkdir -p /logs/celery /logs/supervisord /logs/uwsi /logs/nginx \
    && chown -R django /logs


USER django
WORKDIR /app

ENTRYPOINT ["/entrypoint.sh"]
