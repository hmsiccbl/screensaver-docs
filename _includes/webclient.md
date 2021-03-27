# Build and deploy the Web application client
The client JavaScript application is built using NPM and may be deployed to the `STATIC_ROOT` file location using the Django management command (see Django settings).

## Building the client
This has been tested with node v12.13.0, npm v6.13.0.

```
cd reports/static
npm install
npm run build
```

Output is a set of `bundle.<sha_hash>.js` files created by the webpack bundler.


## Deploying the client

* Note: this step is not needed in development when using the built in Django server, e.g.: `./manage.py runserver`, static files will be served directly by the server.
* The Django `collectstatic` command assists in the moving the static web application files to the `STATIC_ROOT` file location:


```
cd <project_root>
./manage.py collectstatic --noinput --clear --ignore="*node_modules*" --ignore="*api_init*" --ignore="webpack*"

```
