# Updating the application metadata
Resource, Field and Vocabulary **metadata** are used to specify runtime information required for the operation of Screensaver.

- The server metadata can be fully managed using the REST API, see [Loading application metadata](../setup-configuration#bootstrapping-metadata-and-application-data) for more information.
- The `django_requests.py` utility is provided to assist with form authentication and HTTP session management when communicating with the REST API.

## Example metadata operations

A note about the [HTTP request method](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) (aka "action"): 
* for most operations, the `PATCH` action will be specified; as this will perform an update to the entities posted for the resource endpoint,
* care should be taken when specifing the `PUT` action, as this will **replace** the complete set of entities for a resource endpoint.

Update the field definitions for a the `"screen" (/db/api/v1/screen)` resource:
``` bash
PYTHONPATH=. python reports/utils/django_requests.py \
	-u <admin_user> \
	-a PATCH https://screensaver.med.harvard.edu/reports/api/v1/field/ \
	--header "Content-Type: text/csv" --header "Accept: application/json" \
	-f db/static/api_init/metahash_fields_screen.csv
```

Update vocabulary definitions:
``` bash
PYTHONPATH=. python reports/utils/django_requests.py \
  -u <admin_user> \
  -a PATCH https://screensaver.med.harvard.edu/reports/api/v1/vocabulary/ \
  --header "Content-Type: text/csv" --header "Accept: application/json" \
  -f reports/static/api_init/vocabulary_data.csv
```


