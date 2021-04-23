# Server setup

All directories are relative to the `<installation_dir>/screensaver` directory.

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

## Initialize the database

The Django [migrate](https://docs.djangoproject.com/en/3.1/ref/django-admin/#django-admin-migrate) command will initialized the database (create the tables specified in models.py):
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

## Set up Authorization

- **Read** permissions for a Resource allow GET operations
- **Write** permissions for a Resource all PUT, POST, PATCH, and DELETE operations (where implemented, and as allowed by Resource specific constraints). These API permissions are also represented in the corresponding capabilities in the Web application. For instance, write permission is required create or edit a user, library, screen, etc.

All Resources require an Authorization implementation assignment, see [reports.api.api_base.Authorization](https://github.com/hmsiccbl/screensaver/blob/master/reports/api/api_base.py) for details.

By default, Screensaver is set up to use the User and Group permission system to authorize staff users, and other, resource-specific permission implementations for screener user permissions.
* See [ICCB-L Data Sharing Rules](reference#iccb-l-screener-data-sharing-rules)
* See [ICCBL Authorization implementation](reference#iccbl-authorization-implementation)

