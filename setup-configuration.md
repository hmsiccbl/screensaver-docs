---
layout: default
title: Setup
nav_order: 3
has_children: true
---
The Screensaver LIMS consists of a **single page web application** interfacing over the web with a **web server**:
* The **Screensaver server** is a Python based web server that provides REST API implemented with the [Django](https://www.djangoproject.com/) web application and framework and the [PostgreSQL](https://www.postgresql.org/) database. 
* The **Screensaver web application** a JavaScript program that loads in the user's browser from the web server.
