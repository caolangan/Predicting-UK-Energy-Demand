# Predicting UK Energy Demand
General Assembly Capstone project aiming to predict the UK energy demand on the national grid using time series analysis.

## Table of Contents
* [Introduction](#introduction)
* [Project Aims](#project-aims)
* [Data Collection & Handling](#data-collection--handling)
   * [Data Pre-Processing Steps Taken](#data-pre-processing-steps-taken)
   * [The Clean Demand Data](#the-clean-demand-data)    
* [Modelling Approach](#modelling-approach)
   * [Evaluating the Time Series](#evaluating-the-time-series)
   * [Fitting the SARIMA and SARIMAX Models](#fitting-the-sarima-and-sarimax-models)
* [Results](#results) 
* [Python Libraries](#python-libraries) 


## Introduction 
The National Grid is the energy network responsible for supplying and distributing electricity around the UK. It does this through connecting power stations with major substations whilst ensuring the energy demand is satisfied. 

The main sectors this energy supplies can be broken  down as follows:
* **Industry**- Manufacturing, Engineering, Construction, Food & Beverages, etc. 
* **National Services** – Public Administration, Commercial and Agriculture. 
* **Transport**.
* **Domestic**. 

   
## Project Aims
The UK Grid has a set base load it can supply. When the demand rises above this base load, more energy must be supplied to the grid to meet these demands. 
   
To assess these demands the grid uses amber and red warnings to classify how strenuous these demands will be on the grid. The more severe the load, the more energy must be supplied, in some cases even imported. 

This project aims to generate time series models to accurately predict the demand at hourly and daily intervals. 
Accurate predictions can enable: 
   1) **Foresight** - Allow for more efficient planning of energy supply. 
   2) **Maintenance** - Give good indications as to times when to repair/modify the grid's infrastructure that                           will cause the least disruption. 
   3) **Economic advantages** - Allow energy suppliers to evaluate their pricing strategies.  
 

## Data Collection & Handling
Historical national grid data (In this project data on the last 10 years was used) was collected from [a national grid tracker](https://www.gridwatch.templar.co.uk/). Where you can download the data as a csv file which contains timestamped data on the energy demand as well as the various energy sources i.e., Oil, Wind, nuclear, etc.

In this project, I was predominately interested in the time series of the demand data and so decided to bid farewell to the other features for now, but they do show some interesting trends as you can see below and are well worth further investigation. (See image below)

![image](https://user-images.githubusercontent.com/74314773/112242472-d6d65400-8c43-11eb-9534-375409dc2943.png)

### Data Pre-Processing Steps Taken
1) Dropped unhelpful columns, for example, Solar as it is only an estimate and therefore not entirely helpful to his project.
2) Resampled the timeseries into hourly and daily timesteps to access how the demand changes at differing levels of granularity.  
3) Had to forward fill the Na values in the hourly resampled time series due to the irregularity of the original time series observations.
4) Feature engineering- Created exogenous variables to be used in the SARIMAX model. These Included month, year, week day and time of the day (hour ranging from 0 to 24).

### The Clean Demand Data 
Below is the resampled hourly demand time series with lines indicating the different amber and red load warnings. 
![image](https://user-images.githubusercontent.com/74314773/112237613-f0bf6900-8c3a-11eb-89ae-96b3e25d6488.png)

## Modelling Approach
This section will outline the steps taken to generate and find the most accurate model to predict the demand. 
### Evaluating the Time Series
Before any modelling can be done, the time series has to be evaluated as the models require the series to be stationary: 
1) **Check Stationarity**- Is differencing needed?
2) **Plot Correlograms**- ACF (autocorrelation function) and PACF (partial autocorrelation), to find the optimal parameters for the model. 

The timeseries was seasonally decomposed to access stationarity and the correlograms were plotted using the python **pmdarima** and **statsmodels** modules, respectively. This provided estimates as to the order of differencing needed before fitting any models on the time series. 

### Fitting the SARIMA and SARIMAX Models
Firstly, the **Sliding Window Forecast** method from **pmdarima.model_selection** was used to test out a range of p,d,q and seasonal P,D,Q,m parameters. 

The mean cross validation scores for each of the respective models was found and using compared to find the model which performed the best. 

A common model used as a baseline in time series analysis is the Naïve Prediktor
model. This sets the value you want to forecast as the previously observed value. 

Once the optimal parameters were found the SARIMA model was fitted and then exogenous variables were introduced to fit a SARIMAX model and assess their performances.


## Results 
The graph below shows the results of cross validating various SARIMA models, as you can see even the baseline model performed relatively well over a short prediction interval. 
![image](https://user-images.githubusercontent.com/74314773/112645996-f8e7f600-8e3e-11eb-9eb1-4511564778d9.png)

From these results the best parameters were chosen, and exogenous variables were added. Then the model was fitted. A fit of the model can be seen below. With RMSE score of 1105.09
![image](https://user-images.githubusercontent.com/74314773/112646385-4f553480-8e3f-11eb-801c-c4a88f4bdc48.png)

## Python Libraries
The main Python libraries used in this project were: 
* math
* numpy
* pandas
* datetime
* matplotlib
* seaborn
* plotly
* pmdarima
* statsmodels
* tqdm 
