---
layout: default
title: Development
nav_order: 6
---
# Developer notes
{: .no_toc }

1. TOC
{:toc}
---


# Building for development

The client JavaScript application is built using NPM and may be deployed to the `STATIC_ROOT` file location using the Django management command (see Django settings).

# Install NPM to build the web application

<https://www.npmjs.com/get-npm>

## Install the web application dependancies

`$ npm install`

## Building the client
This has been tested with node v12.13.0, npm v6.13.0.

```
cd reports/static
npm install
npm run build
```

Output is a set of `bundle.<sha_hash>.js` files created by the webpack bundler.


## Deploying the client

**TODO** remove this section: superceded by pending client installation instructions from release bundle 

* Note: this step is not needed in development when using the built in Django server, e.g.: `./manage.py runserver`, static files will be served directly by the server.
* The Django `collectstatic` command assists in the moving the static web application files to the `STATIC_ROOT` file location:


```
cd <project_root>
./manage.py collectstatic --noinput --clear --ignore="*node_modules*" --ignore="*api_init*" --ignore="webpack*"

```





{% include testing.md %}
{% include code-of-conduct.md %}

