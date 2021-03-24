# Predicting UK Energy Demand
General Assembly Capstone project aiming to predict the UK energy demand on the national grid using time series analysis.

## Table of Contents
* [Introduction](#introduction)
* [Project Aims](#project-aims)
* [Data Collection & Handling](#data-collection--handling)
   * [Data Pre-Procesing Steps Taken]()    
* [Modelling Approach](#modelling-approach)
* [Results](#results)
* [Python Libraries](#python-libraries) 


## Introduction 
   The National Grid is the energy network responsible for supplying and distributing electricity around the UK. 
   
   It does this through connecting power stations with major substations whilst ensuring the energy demand is satisfied. 
   
   The main sectors this energy supplies can be brocken  down as follows:
   * **Industry**- Manufacturing, Engineering, Construction, Food & Beverages, etc. 
   * **National Services** – Public Administration, Commercial and Agriculture. 
   * **Transport**.
   * **Domestic**. 

   
## Project Aims
The UK Grid has a set base load it can supply. When the demand rises above this base load, more energy has to be supplied to the grid to meet these demands. 
   
In order to asses these demands the grid uses amber and red warnings to classify how strenuous these demands will be on the grid. The more severe the load, the more energy has to be supplied, in some cases even imported. 

This project aims to generate time series models to accuratly predict the dmeand at hourly and daily intervals. 
Accurate predictions can enable: 
   1) **Foresight** - Allow for meore efficient planning of energy supply. 
   2) **Maintenance** - Give good indications as to times  when to repair/modify the grid's infastrucutre that                           will cause the least disruption. 
   3) **Economic advantages** - Allow energy suppliers to evaluate their pricing stratergies.  

## Data Collection & Handling
Historical national grid data was collected from [a national grid tracker](https://www.gridwatch.templar.co.uk/). Where you can download the data as a csv file which contains timestamped data on the energy demand as well as the various energy sources i.e. Oil, Wind, nuclear, e.t.c.

In this project, I was predominately interested in the time series of the demand data and so decided to bid farewal to the other features for now, but they do show some interesting trends as you can see below and are well worth further investigation. (See image below)
![image](https://user-images.githubusercontent.com/74314773/112242472-d6d65400-8c43-11eb-9534-375409dc2943.png)

### Data Pre-Procesing Steps Taken
1) Dropped unhelpful columns, e.g. Solar as it is only an estimate and therefore not entirely helpful to his project.
2) Resampled the timeseries into hourly and daily timesteps to access how the demand changes at differing levels of granularity.  
3) Had to forward fill the Na values in the hourly resampled time series due to the irregularity of the original time series observations.

### The Clean Data 
Below is the resampled hourly demand time series with lines indicating the different amber and red load warnings. 
![image](https://user-images.githubusercontent.com/74314773/112237613-f0bf6900-8c3a-11eb-89ae-96b3e25d6488.png)


## Modelling Approach

## Results

## Python Libraries
