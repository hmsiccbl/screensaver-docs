# API Usage

All features of the Screensaver server may be accessed though the REST API.

## API Schema

The Screensaver server consists of the **Reports** and the **DB** applications.
* The **Reports** application provides functionality to suppport the API operation,
* The **DB** application provides functionality to support high throughput screening data managment. 

### Schema discovery

The API top-level schema is browseable from the web browser at:
* Reports: `http://<server_url>/reports/api/v1/`
* DB: `http://<server_url>/db/api/v1/`

Each resource in the API is defined by a **schema definition** that is also browseable from the web browser at: 
* `http://<server_url>/reports/api/v1/<resource_name>/schema`
* e.g. `https://screensaver.med.harvard.edu/db/api/v1/screen/schema`

### Reports application

Located at `http://<server_url>/reports/api/v1/<resource_name>`

API Resources by name:
* `resource`: metadata definitions of API endpoints (resources) including title and description.
* `field`: metadata definitions of API resource fields.
* `vocabulary`: metadata definitions of application vocabularies.
* `job`: property and state managment for background jobs.
* `user`: user records
* `usergroup`: user group definitions
* `permission`: permission definitions

### DB application

Located at `http://<server_url>/db/api/v1`

API Resources by name:
* `screen`: HTS screening projects
* `study`: HTS in-silico projects
* `library`
* `well`
* `reagent`
* `librarycopy`
* `librarycopyplate`
* `cherrypickrequest`
* `activity`: parent resource for library screenings and service activities.
* `libraryscreening`
* `screensaveruser`
* `checklistitem`

## Interacting with the API

The HTTP REST API may be accessed using tools such as `curl` or `wget`. For a production server, requests must maintain an authenticated session cookie to interact with the browser. Login actions must utilize the form based authentication provided by the URL `accounts/login`. To facilitate the form based authentication and session managment, the `reports.utils.django_requests.py` utility is provided with the following usage examples. 

**Example using the `django_requests.py` utility**
```bash
PYTHONPATH=. python reports/utils/django_requests.py -u sde -a GET https://screensaver.med.harvard.edu/reports/api/v1/job?state=completed
```

