---
layout: default
title: Installation
nav_order: 2
parent: Setup
---
{: .no_toc }

1. TOC
{:toc}
---

# Install Python using Conda

Python 3.8 should be installed using a separate environment. The [Miniconda](https://docs.conda.io/en/latest/miniconda.html) version of the Conda package managment system is recommended.

Once Miniconda is installed, create a separate "screensaver" environment

``` bash
conda create -p <installation_dir>/miniconda/screensaver python=3.8

# activate the environment
conda activate <base directory>/miniconda/screensaver
```

# Install PostgresSql 9.6

Create a new PostgreSQL user and database instance using the [createuser](https://www.postgresql.org/docs/9.6/app-createuser.html) and [createdb](https://www.postgresql.org/docs/9.6/app-createdb.html) commands.



# Download the latest Screensaver release

Clone the Screensaver repository to the installation directory:

```bash
git clone git@github.com:hmsiccbl/screensaver.git <installation_directory>
```


# Install dependencies

Activate the python environment and install the dependencies specified in the requirements.txt file.

``` bash
conda activate miniconda/screensaver
cd <installation_dir>
pip install -r requirements.txt
```

# Download the Web application bundle file from the latest release

<https://github.com/hmsiccbl/screensaver/releases/latest>

* Unpack the bundle to the web application root directory

