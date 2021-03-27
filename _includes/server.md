# Server setup

All directories are relative to the `<installation_dir>/screensaver` directory.

## Database

Create a new PostgreSQL user and database instance using the [createuser](https://www.postgresql.org/docs/9.6/app-createuser.html) and [createdb](https://www.postgresql.org/docs/9.6/app-createdb.html) commands.

## Django installation

The Django server installation uses the `lims` directory as the default application location.

* The default Django settings file is `lims/settings.py`.
* For the Screensaver installation, a `lims/base_settings.py` file is provided with default values for the `lims/settings.py` file.
* Additionally, application wide metadata is provided in an `lims/app_data.py` file. 

### Review `lims/base_settings.py`
* `lims/base_settings.py` contains default settings for the operation of the Django server.
* see [Django settings](https://docs.djangoproject.com/en/3.1/ref/settings/) for more information on settings.

### Create a facility-specific `lims/app_data-<facility_name>.py`
* `lims/app_data.py` contains a template of public `APP_PUBLIC_DATA` metadata. 
* The `APP_PUBLIC_DATA` data structure is available to all authenticated users at the URI `reports/api/v1/resource/app_data`
* To set facility-specific values, the `APP_PUBLIC_DATA` may be overridden, see the example `lims/app_data-facility-example.py`
* Copy the `lims/app_data-facility-example.py` and set facility-specific values as needed.

### Create a lims/settings.py

`lims/settings.py` contains facility and installation specific overrides of the values in `base_settings.py`.

`lims/settings-example-production.py` contains an example `settings.py` file for a production configuration.

Copy `lims/settings-example-production.py` to `lims/settings.py` and adjust values as needed:
* Update the reference `from .app_data-facility-example import APP_PUBLIC_DATA `
* Update `DATABASES` to specify the database connection parameters
  * see [Django database setup](https://docs.djangoproject.com/en/3.1/intro/tutorial02/#database-setup) for more information.
* set the `AUTHENTICATION_BACKENDS` to a authentication module for your installation.
* set the `STATIC_ROOT` to the location where static files will be served from (this is the "docroot" of the application).
* set a `SECRET_KEY`
* Configure background processing settings:
  * Background processing is off by default
```
BACKGROUND_PROCESSING = True
APP_PUBLIC_DATA.BACKGROUND_PROCESSING = BACKGROUND_PROCESSING

BACKGROUND_PROCESSOR = {
    SCHEMA.SETTINGS.BACKGROUND.POST_DATA_DIR: os.path.join(
        PROJECT_ROOT, "..", "logs", "background", "post_data"
    ),
    SCHEMA.SETTINGS.BACKGROUND.JOB_OUTPUT_DIR: os.path.join(
        PROJECT_ROOT, "..", "logs", "background", "job_output"
    ),
    SCHEMA.SETTINGS.BACKGROUND.RESPONSE_DATA_DIR: os.path.join(
        PROJECT_ROOT, "..", "logs", "background", "response_data"),
    SCHEMA.SETTINGS.BACKGROUND.RESPONSE_DATA_DIR_MAX_BYTES: (2**30)*1, # 1GB
    SCHEMA.SETTINGS.BACKGROUND.MAX_JOBS_PER_PERSON: 3,
    "credential_file": os.path.join(
        PROJECT_ROOT, "..", "production_data", "credentials.txt"
    ),
    "python_environ_script": os.path.join(PROJECT_ROOT, 'scripts', "run_webconf_consolelogs.sh"),
    "background_process_script": "reports.utils.background_client_util",
    }
```
  * see the background processing discussion for more details
* Logging configuration: note that output log file locations should be accessible from all webserver instances.
* set the `TEMP_FILE_DIR` to a directory location for temporary files created during download operations; this directory should be visible to all server instances.
* set the `WELL_STRUCTURE_IMAGE_DIR` to serve compound images; this directory must be visible from all webserver instances.

## Initialize the database

The Django [migrate](https://docs.djangoproject.com/en/3.1/ref/django-admin/#django-admin-migrate) command will initialized the database:
``` bash
./manage.py migrate
```
* see [Django docs: Getting started: Database setup](https://docs.djangoproject.com/en/3.1/intro/tutorial02/#database-setup) for more details.


## Create a super-user account

At least one super-user account must be set up to administer the system.

``` bash
./manage.py createsuperuser
```
* see [Django docs: Getting started: Creating an admin user](https://docs.djangoproject.com/en/3.1/intro/tutorial02/#creating-an-admin-user) for more details.

