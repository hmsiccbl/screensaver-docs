
# Interacting with the API

## Authentication

The first step in interaction with the API is authenticating the user.

Screensaver authenticates users through a form based login that acquires a [secure HTTP session](https://docs.djangoproject.com/en/3.1/topics/http/sessions/).  

Specifically, the client must get the login form provided by the URL `accounts/login`, and the client must post authentication criteria and a [CSRF token](https://docs.djangoproject.com/en/3.1/ref/csrf/) obtained from this form to the same URL (`accounts/login`).

To facilitate this process, Screensaver provides the `reports.utils.django_requests.py` utility. This utility is a wrapper for the Python [requests](https://docs.python-requests.org/en/master/) package. This utility will acquire a secure HTTP session and will perform GET, PUT, POST, and DELETE operations using this session.  

* see: [Django Authenication System](https://docs.djangoproject.com/en/3.1/topics/auth/default/)
* see: [https://docs.djangoproject.com/en/3.1/ref/csrf/](https://docs.djangoproject.com/en/3.1/ref/csrf/)

**Examples: using the `django_requests.py` utility**
```bash

# Show help
PYTHONPATH=. python reports/utils/django_requests.py -h
usage: django_requests.py [-h] [-u USERNAME] [-p PASSWORD] [-c CREDENTIAL_FILE] [-f FILE] -a {GET,POST,PUT,PATCH,DELETE} [--header HEADER] [-v]
                          [--login_form LOGIN_FORM]
                          url

Utility to perform HTTP operations using a secure HTTP session, authentiated with the Screensaver server.

positional arguments:
  url                   the URL to connect to

optional arguments:
  -h, --help            show this help message and exit
  -u USERNAME, --username USERNAME
  -p PASSWORD, --password PASSWORD
  -c CREDENTIAL_FILE, --credential_file CREDENTIAL_FILE
                        credential file containing the username:password for api authentication
  -f FILE, --file FILE  file to POST, PUT, or PATCH
  -a {GET,POST,PUT,PATCH,DELETE}, --action {GET,POST,PUT,PATCH,DELETE}
                        HTTP action
  --header HEADER       HTTP header (may be repeated)
  -v, --verbose         Increase verbosity (specify multiple times for more)
  --login_form LOGIN_FORM
                        default: '/accounts/login/'


# GET
PYTHONPATH=. python reports/utils/django_requests.py \
  -u sde -a GET https://screensaver.med.harvard.edu/reports/api/v1/job?state=completed

# PATCH
PYTHONPATH=. python reports/utils/django_requests.py \
  -u sde -a PATCH https://screensaver.med.harvard.edu/reports/api/v1/field/ \
  --header "Content-Type: text/csv" \
  --header "Accept: application/json" \
  -f db/static/api_init/metahash_fields_useragreement.csv -v

```
## Upload operations

Uploading of data can be used to either create new records, or to update existing records.

## Definitions
* A **[REST](https://en.wikipedia.org/wiki/Representational_state_transfer) API** defines a set of HTTP resources that support a simple set of HTTP opererations, principally GET, PUT, POST, DELETE, and optionally PATCH.  
* **Resource**: an API endpoint, identified by a URI, that provides REST operations on records associated with the URI.
* **Field**: a column or attribute of a record for a Resource.
* **Schema**: a data structure containing definitions of the Resources and Fields. The Schema defines metadata information about the Resource as well as all of the metadata for each Field of the Resource.

The Screensaver server consists of the **Reports** and the **DB** applications.
* The **Reports** application provides functionality to suppport the API operation
  * `http://<server_url>/reports/api/v1/`
* The **DB** application provides functionality to support high throughput screening data managment. 
  * `http://<server_url>/db/api/v1/`

To determine the Fields that define a Resource, administrators must query the API to retrieve the Field schema for the Resource.

## Schema discovery

Each resource in the API is defined by a **schema definition** that is also browseable from the web browser at: 
* `http://<server_url>/reports/api/v1/<resource_name>/schema?full=true`
* `http://<server_url>/db/api/v1/<resource_name>/schema?full=true`  
* NOTE: the parameter "full=true" retrieves the full set of fields for the resource: combining resource-specific fields with fields inherited from parent resources. The "full" set of fields is most useful.

e.g. [demo.screensaver.med.harvard.edu/db/api/v1/screen/schema?full=true](https://demo.screensaver.med.harvard.edu/db/api/v1/screen/schema?full=true)

The Resource and Field definitions themselves are also defined by a schema. To view:
* `http://<server_url>/reports/api/v1/resource/schema?full=true`
* `http://<server_url>/reports/api/v1/field/schema?full=true`


## Schema discovery from the Web application


The API Schema may also be browsed from the Web application, using the reporting table view interface:
* Resource report view: [https://demo.screensaver.med.harvard.edu/#resource](https://demo.screensaver.med.harvard.edu/#resource)
* Field report view: [https://demo.screensaver.med.harvard.edu/#field](https://demo.screensaver.med.harvard.edu/#field)

NOTES:
* No hierachical data are presented, to find the fields for a particular resource, filter the field view using the "Resource" drop down on the top left.
* Each Resource or Field record has been flattened to fit in the tabular view; some fields contain nested data that will be presented as a single field.

Many resources are defined by combining several base resources into the full composite resource, therefore, when browsing in the Field report view, the "full" resource is obtained by combining the base resources:

Composite Resource | Combines the base Resources | "full" Fields query
---|---|---
SmallMoleculeReagent | Well, Reagent, and SmallMoleculeReagent fields | [#field/search/scope__in=fields.well,fields.reagent,fields.smallmoleculereagent](https://demo.screensaver.med.harvard.edu/#field/rpp/25/page/1/search/scope__in=fields.well,fields.reagent,fields.smallmoleculereagent)
NaturalProductReagent | Well, Reagent, and NaturalProdutReagent fields | [#field/search/scope__in=fields.well,fields.reagent,fields.naturalproductreagent](https://demo.screensaver.med.harvard.edu/#field/rpp/25/page/1/search/scope__in=fields.well,fields.reagent,fields.naturalproductreagent)
SilencingReagent | Well, Reagent, and SilencingReagent fields | [#field/search/scope__in=fields.well,fields.reagent,fields.silencingreagent](https://demo.screensaver.med.harvard.edu/#field/rpp/25/page/1/search/scope__in=fields.well,fields.reagent,,fields.silencingreagent)

## Determining fields that may be edited

The Field.editability attribute defines whether a particular field is editable. Editability values:
* "u" - the field may be updated.
* "c" - the field may be specified on creation.
* blank - the field cannot be set or updated.

TODO: Screensaver will soon provide a "Generate template file" function as a button on the different report views. The API will generate a blank file of the chosen serialization format (CSV, XLSX, ...) that will contain all of the updateable fields for the Resource, as well as the "key" field(s) for that Resource.

## Determining data type for each field

The Field.data_type attribute defines the data type for the field in the database. See the field.data_type vocabulary for the full description at `https://<server_url>/#vocabulary/rpp/25/page/1/search/scope__exact=field.data_type`, for example [https://demo.screensaver.med.harvard.edu/#vocabulary/rpp/25/page/1/search/scope__exact=field.data_type](https://screensaver.med.harvard.edu/#vocabulary/rpp/25/page/1/search/scope__exact=field.data_type)

## List of data types

Data Type | Description | Serialization
--- | ---
string | Text data | --
boolean | Boolean data | "true" or "false"
date | Date value | "%Y-%m-%d", e.g. "2021-03-01"
datetime | Date and time | "%Y-%m-%d %H:%M:%S", e.g. "2021-03-01 10:12:11" 
list | List of string or integer values | Separate values using semicolons
float | Float value | Floating point number; note that precision is not specified and may be truncated depending on the specification of the particular database field.
decimal | Floating point value with precision | On input the precision will be limited to the precision specified in the "display_options" for the field
integer | Integer values | Only integer values are accepted

## Serialization (textual representation of the data type on import and export)

Data should be serialized as follows:

### CSV, XLSX, SDF

Serialize all data into string format; strings with spaces may be quoted, numerical data may be represented as string or number, however it is recommended that all data be converted to string to minimize errors caused by display formatting hiding significant figure data in Excel.

### JSON

All data may be input as string format; if numerical data are imported, data may be represented as string or number; list data are represented as JSON lists.

# API Resource Listing

## Reports application

Located at `http://<server_url>/reports/api/v1/<resource_name>`

API Resources by name:
* `resource`: metadata definitions of API endpoints (resources) including title and description.
* `field`: metadata definitions of API resource fields.
* `vocabulary`: metadata definitions of application vocabularies.
* `job`: property and state managment for background jobs.
* `user`: user records
* `usergroup`: user group definitions
* `permission`: permission definitions

## DB application

Located at `http://<server_url>/db/api/v1`

API Resources by name:
* `screen`: HTS screening project.
* `study`: HTS in-silico project.
* `library`: A collection of reagents.
* `well`: A single location in a plate layout for a library.
* `reagent`: A reagent contained in a well.
* `librarycopy`: A physical copy of a set of library plates.
* `librarycopyplate`: A single physical plate of a librarycopy.
* `activity`: The parent resource for library screenings and service activities.
* `libraryscreening`: A collection of librarycopyplates to be screened.
* `screenresult`: A collection of raw or derived result values for a library screening.
* `datacolumn`: Meta data describing a column of result values.
* `cherrypickrequest`: The configuration details for a cherry pick request screening.
* `screenercherrypick`: Library source plate wells that have been requested for a cherry pick screening.
* `labcherrypick`: Library copy wells that have been selected to fulfill screener cherry picks requested.
* `screensaveruser`: A staff or screening user of the system.
* `checklistitem`: A screening user checklist item.


