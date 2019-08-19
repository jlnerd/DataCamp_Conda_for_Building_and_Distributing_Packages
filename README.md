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
# Use whatever description you want
```

## Add packages and commands
Here, we add the required packages to the project and prepare the environment. This Python 3 based project will need to install Pandas for data processing and statsmodels to fit the autoregressive model and make predictions.
All other dependencies of these packages, like NumPy and Scipy will be installed automatically.
```
$ anaconda-project add-packages python=3
$ anaconda-project add-packages pandas
$ anaconda-project add-packages statsmodels
```
