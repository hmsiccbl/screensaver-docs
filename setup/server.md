---
layout: default
title: Server Configuration
nav_order: 5
parent: Setup
---
{: .no_toc }

1. TOC
{:toc}
---


# Django settings

All paths are relative directory where the Github repository was downloaded to.

Settings are provided in the files:
* `lims/base_settings.py` provides default values,
* `lims/settings.py` overrides the `base_settings.py` and may be modified for facility specific settings,
* application wide metadata is provided in an `lims/app_data.py` file. 

## Review `lims/base_settings.py`
* `lims/base_settings.py` contains default settings for the operation of the Django server.
* see [Django settings](https://docs.djangoproject.com/en/3.1/ref/settings/) for more information on settings.

## Create a facility-specific `lims/app_data-<facility_name>.py`
* `lims/app_data.py` contains a template of public `APP_PUBLIC_DATA` metadata. 
* The `APP_PUBLIC_DATA` data structure is available to all authenticated users at the URI `reports/api/v1/resource/app_data`
* To set facility-specific values, the `APP_PUBLIC_DATA` may be overridden, see the example `lims/app_data-facility-example.py`
* Copy the `lims/app_data-facility-example.py` and set facility-specific values as needed.

## Configure facility specific `lims/settings.py`

`lims/settings.py` contains facility and installation specific overrides of the values in `base_settings.py`.

`lims/settings-example-production.py` contains an example `settings.py` file for a production configuration.

Copy `lims/settings-example-production.py` to `lims/settings.py` and adjust values as needed:
* Update the reference `from .app_data-facility-example import APP_PUBLIC_DATA `
* Update `DATABASES` to specify the database connection parameters
  * see [Django database setup](https://docs.djangoproject.com/en/3.1/intro/tutorial02/#database-setup) for more information.
* Add a [custom authentication backend](https://docs.djangoproject.com/en/3.1/topics/auth/customizing/) to`AUTHENTICATION_BACKENDS` if you will require features not provided by the Django authentication in the database.
  * TODO: generic authentication backend instructions
* Set the `STATIC_ROOT` to the location where static files will be served from (this is the "docroot" of the application).
* Set a `SECRET_KEY`
* Logging configuration: note that output log file locations should be accessible from all webserver instances.
* `TEMP_FILE_DIR`: 
  * directory location for temporary files created during download operations; this directory should be visible to all server instances.
  * Note: temporary files are created to minimize runtime memory requirements for file downloads, and in some cases to enable asynchronous downloads. In cases where these files can not be removed immediately on completion of streaming to the HTTP socket; these files are periodically purged; see reports.api.base._clear_old_files for details.
  * `TEMP_FILE_DIR_MAX_BYTES` is set to 2GB by default

* Set the `WELL_STRUCTURE_IMAGE_DIR` to serve compound images; this directory must be visible from all webserver instances.
* Configure background processing settings:
  * Background processing is off by default
  * See [Background Processing](reference#request-background-processing)

# Initialize the database

Execute the Django [migrate](https://docs.djangoproject.com/en/3.1/ref/django-admin/#django-admin-migrate) command to initialized the database (create the tables specified in models.py):
``` bash
./manage.py migrate
```
* see [Django docs: Getting started: Database setup](https://docs.djangoproject.com/en/3.1/intro/tutorial02/#database-setup) for more details.


# Create a super-user account

At least one super-user account must be set up to administer the system.

``` bash
./manage.py createsuperuser
```
* see [Django docs: Getting started: Creating an admin user](https://docs.djangoproject.com/en/3.1/intro/tutorial02/#creating-an-admin-user) for more details.

# Set up Authorization

- **Read** permissions for a Resource allow GET operations
- **Write** permissions for a Resource all PUT, POST, PATCH, and DELETE operations (where implemented, and as allowed by Resource specific constraints). These API permissions are also represented in the corresponding capabilities in the Web application. For instance, write permission is required create or edit a user, library, screen, etc.

All Resources require an Authorization implementation assignment, see [reports.api.api_base.Authorization](https://github.com/hmsiccbl/screensaver/blob/master/reports/api/api_base.py) for details.

By default, Screensaver is set up to use the User and Group permission system to authorize staff users, and other, resource-specific permission implementations for screener user permissions.
* See [ICCB-L Data Sharing Rules](reference#iccb-l-screener-data-sharing-rules)
* See [ICCBL Authorization implementation](reference#iccbl-authorization-implementation)

# Testing with the Django development server

The Django development server may be used as both the web server and the application server for development and testing purposes (for non-production use only).

To run the development server:

`./manage.py runserver`

* Note that this invokes the Django development server, which is not suitable for production use. For more information, see the [Django runserver documentation](https://docs.djangoproject.com/en/3.2/ref/django-admin/#runserver)
* See [Deploying in a production environment](#deploying-in-a-production-environment)


# Bootstrapping metadata

The Resource, Field and Vocabulary **metadata** must be loaded to the Screensaver database. This information is used to build the resource definition schemas that are required for the operation of the REST API and also for the operation of the web application client. 


## Loading the application metadata into the database

* The default Resource, Field, and Vocabulary metadata files are defined at:
  * `reports/static/api_init/`
  * `db/static/api_init/`
* These default metadata files must be loaded into the database for the Screensaver application to access. 
* For convenience, the `db_init.py` script is provided with the `api_init_actions.csv` that specifies the API interactions, in order to load all of the bootstrap metadata. 
* Using this process, all of the resource, field and vocabulary definitions for a server may be loaded with one command.
* Individual metadata files may be loaded separately, see [Usage](api-usage) for more information.
* These server initialization commands will **fully reset all of the metadata for the installation**, so care should be taken to ensure that all server metadata has been saved prior to executing.
* These server initialization commands are idempotent, this process may be run repeatedly to fully reinitialize the server metadata.
* For convenience, the metadata for the `reports` sub-application is contained separately from the metadata for the `db` sub-application.

## Bootstrap instructions

1. Start the development server:
``` bash
./manage.py runserver
```

2. In a separate window, execute the bootstrapping commands

``` bash
# bootstrap the reports sub-application
# note `localhost` may be replaced with the location of the public server in production
PYTHONPATH=. python reports/utils/db_init.py --input_dir=./reports/static/api_init/ \
  -f ./reports/static/api_init/api_init_actions.csv \
  -u http://localhost:8000/reports/api/v1 -U <admin_username>

# bootstrap the db sub-application
PYTHONPATH=. python reports/utils/db_init.py --input_dir=./db/static/api_init/ \
  -f ./db/static/api_init/api_init_actions.csv \
  -u http://localhost:8000/reports/api/v1 -U <admin_username>

```

# Bootstrapping user and usergroup data

Administrative user, usergroup and permission **application data** are usually required for the screening facility staff. 
* It is recommended that these data also be set up through the REST API interface.
* The User, Usergroup, and Pemission data may be stored in (CSV/XLSX) files that may be modified and uploaded as needed,
* To facilitate this process, the `db_init.py` script may be provided with an `api_init_actions.csv` file in the same manner as with the bootstrap metadata process above, so that all of the user, usergroup, and permission data may be loaded at once. 

``` bash
PYTHONPATH=. python reports/utils/db_init.py \
  --input_dir=../iccbl/production_data/lims \
  -u https://dev.screensaver.med.harvard.edu \
  -f ../iccbl/production_data/lims/api_init_actions_patch.csv -U sde

```
* TODO: provide example admin user, usergroup, and permission (CSV) files.

# Deploying in a production environment

Adjust settings for production
* **DEBUG=FALSE** should always be used in production to avoid leaking runtime information
* **SECRET_KEY** should be set to a protected value
* **ALLOWED_HOSTS** should be adjusted for the production server address

see [Settings](#settings)

A production setup should consist of:
* A **web server** to efficiently serve static files, such as [nginx](https://www.nginx.com/) or [apache](https://httpd.apache.org/)
  * The web server should directly serve the directory specified as the **STATIC_ROOT** (see [Settings](#settings)):
    * the Screensaver web application client code is deployed to the **STATIC_ROOT** directory
  * The web server will be configured as a [reverse proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/) to direct API requests to the application server.
  * Requests to these paths will be directed to the WSGI application server:
    * `/db` - for LIMS application requests
    * `/reports` - for the supporting "reports" application requests
    * `/accounts` - for the Django authentication application requests
* A production ready **WSGI application server** such as [gunicorn](https://gunicorn.org/)
  * See [WSGI](https://en.wikipedia.org/wiki/Web_Server_Gateway_Interface) specification for Python web servers 
  * See the Django documentation [How to deploy with WSGI](https://docs.djangoproject.com/en/3.2/howto/deployment/wsgi/)
  * Make sure that the WELL_STRUCTURE_IMAGE_DIR, TEMP_FILE_DIR, and any directories configured in the logging setup are visible to all instances of the WSGI server.


