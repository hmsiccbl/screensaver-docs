---
layout: default
title: Setup
nav_order: 3
has_children: true
---
The Screensaver LIMS consists of a **single page web application** and a **web server**:
* The **Screensaver web server** is a REST API implemented with Python using the [Django](https://www.djangoproject.com/) framework.
* Screensaver uses a [PostgreSQL](https://www.postgresql.org/) database to support data storage and reporting.
* The **Screensaver web application** is a JavaScript program that loads in the user's browser.
