NOT TO BE USED FOR PRODUCTION. TESTING AND LOCAL DEVELOPMENT ONLY!


# Overview


## Changes to Note

One breaking change in this branch is the conversion of the use of Python's Windows INI ConfigParser format to a similar dotenv (.env) format. The Settings section below describes the transition.

# Settings

By default, to ease transition from previous versions, `settings.py`
will attempt to load the dotenv file `adl_lrs/settings.env` to import
settings values.

OS environment variables will take precedent over anything defined
within the .env file. One useful environment variable to set for the
launched container is `DOTENV_FILE`. If `DOTENV_FILE` is defined and contains the path to another dotenv file, that file will be used to populate values. This
can be useful in containerization when you may mount a volume containing
secrets that you don't want built into an image.

Read More:

 * [12-Factor Application](https://12factor.net/config)
 * [django-environ](http://django-environ.readthedocs.io/)


## Migrating previous .ini values
The main difference in file formats is the removal of variables
sections.

A sample settings file is included in the `deploy` directory:
`deploy/settings.env.example`. This file can be copied to
`adl_lrs/settings.env` and the values updated for your particular needs.

Some sensible development default values are now defined for some variables within the `settings.py` file.

# Docker-Compose

## Setup

docker-compose -f production.yml build
docker-compose -f production.yml start
docker-compose -f production.yml up
docker-compose -f production.yml run lrsapp python manage.py createsuperuser


# Kubernetes

