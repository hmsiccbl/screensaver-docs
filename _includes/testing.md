# Testing

Screensaver tests are run using the Django management `test` command. Tests subclass `django.test.TestCase`, a subclass of `unittest.TestCase` that wraps each test, and each test class, in a transaction. See the Django documentation [Writing and running tests](https://docs.djangoproject.com/en/3.1/topics/testing/overview/) for more information.

The Screensaver test suite requires a PostgreSQL database instance; this test database instance will be created when tests are run. The name of the test database is formed by prepending **test_** to the `NAME` given in the `DATABASES` section of `settings.py`, e.g `test_screensaver`.

## Initial run

Before the tests are run, the application **metadata** must be initialized. This step is built in to the test suite `setupModule` function and can be optionally turned on with the `--reinit_metahash` flag. 
* `--reinit_metahash` should be used for the initial setup of the test database, or whenever the application metadata have been changed.
* See [Bootstrapping metadata](setup/server.html#bootstrapping-metadata) for more information.

``` bash
# use the --reinit_metahash flag for the initial run
# use the --keepdb flag so that the metadata will be kept
manage.py test --reinit_metahash --keepdb

# run a single test with the --reinit_metahash flag, to reduce the time for the initial run
manage.py test db.test.tests.ScreenResource.test1_create_screen --reinit_metahash --keepdb 

```

## After initializing metadata

``` bash
manage.py test --keepdb

# run a single test
manage.py test db.test.tests.ScreenResource.test1_create_screen --keepdb
```
