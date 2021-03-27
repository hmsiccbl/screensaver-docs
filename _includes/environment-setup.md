# Environment setup

## Install Python using Conda

Python should be installed using a separate environment. The [Miniconda](https://docs.conda.io/en/latest/miniconda.html) version of the Conda package managment system is recommended.

Once Miniconda is installed, create a separate "screensaver" environment

``` bash
conda create -p <installation_dir>/miniconda/screensaver python=3.8

# activate the environment
conda activate <installation_dir>/miniconda/screensaver
```

## Download Screensaver

Clone the screensaver repository to the `<installation_dir>/screensaver` directory
``` bash
cd <installation_dir>
git clone git@github.com:hmsiccbl/screensaver.git
```

## Install dependencies

Activate the python environment and install the dependencies specified in the requirements.txt file.

``` bash
cd <installation_dir>
conda activate miniconda/screensaver
cd screensaver
pip install -r requirements.txt
```



