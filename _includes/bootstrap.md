# Bootstrapping metadata and application data

Resource, Field and Vocabulary **metadata** are used to specify runtime information required for the operation of Screensaver.

Additionally, User, Usergroup, and Permission **application data** are required to setup administrative user accounts for the system. 

## Loading the application metadata into the database

* The default Resource, Field, and Vocabulary metadata files are defined at:
  * `reports/static/api_init/`
  * `db/static/api_init/`
* These default metadata files must be loaded into the database for the Screensaver application to access. 
* For convenience, the `db_init.py` script is provided with the `api_init_actions.csv` specification file. Using this process, all of the resource, field and vocabulary definitions for a server may be loaded with one command.
* Individual metadata files may be loaded separately, see [Usage](usage) for more information.
* These server initialization commands will **fully reset all of the metadata for the installation**, so care should be taken to ensure that all server metadata has been saved prior to executing.
* These server initialization commands are idempotent, this process may be run repeatedly to fully reinitialize the server metadata.
* For convenience, the metadata for the `reports` sub-application is contained separately from the metadata for the `db` sub-application.

### Bootstrap instructions

Start the server:
``` bash
./manage.py runserver
```

In a separate window, execute the bootstrapping commands

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

## User, Usergroup, and Permissions for administrative users


``` bash
PYTHONPATH=. python reports/utils/db_init.py \
  --input_dir=../iccbl/production_data/lims \
  -u https://dev.screensaver.med.harvard.edu \
  -f ../iccbl/production_data/lims/api_init_actions_patch.csv -U sde

```

