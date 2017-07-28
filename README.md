# CryptoCurrencyTrader
A machine learning program in python to generate cryptocurrency trading strategies using machine learning.
The script is inspired by both the pytrader project https://github.com/owocki/pytrader, and the auto-sklearn project https://automl.github.io/auto-sklearn/stable/. 

# Disclaimer
The information in this repository is provided for information purposes only. The Information is not intended to be and does not constitute financial advice or any other advice, is general in nature and not specific to you.

## Input Data
Minor changes were made to the Poloniex API python wrapper which is inluded in the repository https://github.com/s4w3d0ff/python-poloniex. Data is retrieved via the Poloniex API in OHLC (open, high, low, close) candlestick format.

### Technical Indicators - Training Inputs
A series of technical indicators are calculated and provided as inputs to the machine learning optimisation, exponential moving averages and exponential moving volatilities over a series of windows. A kalman filter is also provided as an input.

### Training Targets - Strategy Score
An ideal trading strategy is generated based on past data, every candlestick is given a score which represent the potential profit or loss before the next price reversal exceeding the combined transaction fee and bid ask spread. This minimum price reversal is represented by Δp in the diagram below.
![Alt text](strategyscore.jpg?raw=true "Optional Title")

### Strategy Generation
A buy threshold and sell threshold are selected which maximise profit based on the score returned for the training data, where a sell or buy signal is generated if the respective threshold is crossed.

## Machine Learning Meta-fitting and Hyper Parameter Optimisation
The machine learning optimisation is based on a two layer random search, as outlined in the diagram below. The meta-fitting selects a machine learning and preprocessing pair, the selected machine learning model is then optimised using a second random grid search to fit the hyperparameters for that particular machine learning model. (Without GPU support the tensorflow fitting may take a long time!)
![Alt text](ML_Flowchart.png?raw=true "Optional Title")

## Example results
With none of the different automated machine learning optimisation strategies was I able to get a set of fitting parameters which was consistently profitable at multiple offsets. Some of the offsets would be profitable an example is included below.
![Alt text](Fitting_example.png?raw=true "Optional Title")

## Validation
In order to estimate the amount of overfitting, a series of offset hyperparameter fittings are performed. If the trading strategy is not overfit, fitting should be approximately consistent across at all offsets in terms of profit fraction and fitting error.

## To Do
With none of the different automated machine learning optimisation strategies was I able to get a set of fitting parameters which was consistently profitable at multiple offsets.
* Add more candlestick inputs.
* Add none price data.
* Improve selection of technical indicators to efficiently provide the most information from the market (reduce redundancy.)


## Python 2.7 + Tensorflow + MiniConda
There is an easy way to configure your system for these scripts by using the Anaconda package manager. Start by following the Anaconda installation instructions found here:

* https://conda.io/docs/installation.html - Install the latest Anaconda for package management
* https://conda.io/docs/_downloads/conda-cheatsheet.pdf - Handy Anaconda command line cheatsheet

Once you have Anaconda installed, use the following setup appropriate for your system architecture. 

## OSX / linux
To get the correct packages setup on Linux, execute the following from a shell prompt:

    conda create -n tensorflow-p2 python=2.7
    source activate tensorflow-p2
    conda install numpy pandas matplotlib tensorflow jupyter notebook scipy scikit-learn nb_conda  
    conda install -c auto multiprocessing statsmodels arch
    pip install arch polyaxon

## Windows
To get the correct packages setup on Windows, execute the following from a command prompt:

    conda create -n tensorflow-p2 python=2.7
    activate tensorflow-p2
    conda install numpy pandas matplotlib tensorflow jupyter notebook scipy scikit-learn nb_conda  
    conda install -c auto multiprocessing statsmodels arch
    pip install arch polyaxon


