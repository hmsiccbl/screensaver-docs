# Environment setup

## Install Python using Conda

Python 3.8 should be installed using a separate environment. The [Miniconda](https://docs.conda.io/en/latest/miniconda.html) version of the Conda package managment system is recommended.

Once Miniconda is installed, create a separate "screensaver" environment

``` bash
conda create -p <installation_dir>/miniconda/screensaver python=3.8

# activate the environment
conda activate <base directory>/miniconda/screensaver
```

## Install PostgresSql 9.6

Create a new PostgreSQL user and database instance using the [createuser](https://www.postgresql.org/docs/9.6/app-createuser.html) and [createdb](https://www.postgresql.org/docs/9.6/app-createdb.html) commands.



## Download the Screensaver source code

[github.com/hmsiccbl/screensaver](https://github.com/hmsiccbl/screensaver)


## Install dependencies

Activate the python environment and install the dependencies specified in the requirements.txt file.

``` bash
conda activate miniconda/screensaver
cd <installation_dir>
pip install -r requirements.txt
```



