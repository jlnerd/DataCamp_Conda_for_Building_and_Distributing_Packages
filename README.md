# Conda for Building and Distributing Packages (DataCamp)
https://campus.datacamp.com/courses/conda-for-building-distributing-packages/

## Description
This readme highlights the key steps/processes to creating a python package via anaconda-project. It roughly follows the steps outlined in the [Conda for Building and Distributing Packages](https://campus.datacamp.com/courses/conda-for-building-distributing-packages/) DataCamp course, however, here our focus is on creating a quick reference to apply the lessons learning from this DataCamp course

## Initialize a New Project
We will be creating a project called ```mortgage_rates```. All lines which begin with ```$``` indicated command line interface (CLI) commands
```
$ mkdir mortgage_rates
$ cd mortgage_rates/
$ anaconda-project init # Initialize the Anaconda Project specification
$ nano /home/repl/mortgage_rates/anaconda-project.yml # Edit the anaconda-project.yml file to add a description of the project. 
# Insert whatever description you want
```

## Add packages and commands
Here, we add the required packages to the project and prepare the environment. This Python 3 based project will need to install Pandas for data processing and statsmodels to fit the autoregressive model and make predictions.
All other dependencies of these packages, like NumPy and Scipy will be installed automatically.
```
$ anaconda-project add-packages python=3
$ anaconda-project add-packages pandas
$ anaconda-project add-packages statsmodels
```

Now it's time to add the URL to download the 30-year mortgage rates. In a project, files are downloaded automatically when a command is run. A download is defined through the add-download command which takes two arguments.

```
$ anaconda-project add-download <ENV_VARIABLE> <DOWNLOAD_URL>
```
Here, we add a download for https://goo.gl/jpbAsR with the variable name ```MORTGAGE_RATES```
```
$ anaconda-project add-download MORTGAGE_RATES https://goo.gl/jpbAsR
```

To add a command to run a script, we execute the following line:
```
$ anaconda-project add-command [flags] <name> <command-to-execute>
```

## Locking Package Versions
Use ```anaconda-project lock``` to write the current versions of every package, including low-level dependencies, for the Mac, Linux, and Windows platforms to the anaconda-project-lock.yml file so that other users can exactly recreate the environment as you were using today.

## Sharing Your Project
Below, we create a compressed project archive and share it on Anaconda Cloud.

First, we archive the ```mortgage_rates``` project with the command:
```$ anaconda-project archive <zip-file>```
where ```<zip-file>``` is the path to the zip file of interest.

Next, logon to anaconda using ```$ anaconda login```

Finally, upload the archive.
```
$ anaconda upload <zip-file> --package-type=project
```


## Meta.yaml
A typical meta.yaml file is shown below:
```
{% set setup_py = load_setup_py_data() %}

package:
    name: 'mortgage_forecasts'
    version: {{ setup_py.get('version') }}

source:
    path: ./

build:
    script: python setup.py install --single-version-externally-managed --record=record.txt

requirements:
    run:
        - python
        - scipy
        - numpy 1.11*
        - matplotlib >=1.5, <2.0

    build:
        # Packages used by setup.py
        # to install this package.
        # May also install compilers
        # for non-python code.
        - python
        - setuptools

about:
    license: {{ setup_py.get('license') }}
    license_file: LICENSE
    summary: {{ setup_py.get('description') }}
```
Read the meta.yaml documentation for more details.


## Buld the Conda Package
