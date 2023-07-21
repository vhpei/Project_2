# Project 2  
## First Part  
### Challenge  

The customer needs update the storage clothing in each store for October of 2019.  

### Objective  

Precisely predict the weekly sales considering seasonality, trend and explanatory variables. For additional, should be done an analysis of the data that will be used in the model.  

## Second Part  

The customer does not know the data that are in the bases of data and its potential.  

### Objective  

Must create an idea unique and creative that takes advantage of available data. This can involve the development of new features, identification trends or proposed data-driven solutions for address challenges or take advantage specific opportunities.  

## Data

- [cities.csv](https://github.com/vhpei/Projeto_2/blob/main/cities.csv) (2 KB)
- [product.csv](https://github.com/vhpei/Projeto_2/blob/main/product.csv) (47 KB)
- [sales.csv](https://github.com/vhpei/Projeto_2/blob/main/sales.csv) (648.3 MB)

These files were added to the repository via [git LFS](https://git-lfs.com/).  

## Notebook

All the steps done for this project are done in the [notebook](https://github.com/vhpei/Projeto_2/blob/main/Projeto_2.ipynb) within this repository, the notebook repository is presented as follows.  
Along the notebook it contains comments throughout the code and conclusions for the data analysis for example.

<details>
<summary>Set up</summary> 
<p>In this section is present the setup for the rest of the notebook, libraries and functions used are present here</p>
<ul>
<details>
<summary>Import libraries</summary>
<p>All libraries used during this code are imported in this section</p>
</details>
<details>
<summary>Functions used along the code</summary>
<p>All the function used along the code are listed here, namely city population, latitude, longitude and season</p>
</details>
</ul>
</details>
<details>
<summary>Data Understanding and cleaning</summary>
<p>In this section some data cleaning will be performed. The city names were corrected, null values were replaced using the interpolate function of pandas, aswell as a k-nearest neighbors algorithm, for the first 2 csv files.  
For the third csv file, some columns were droped, and null values were filed</p>
<ul>
<details>
<summary>Product</summary></p>
<p>O ficheiro tem 10 colunas com 699 registos.

As 10 colunas referentes a esta tabela são as seguintes:

- product_id

Variável do tipo object.

Não existem duplicados.

Inicia por P seguido de 4 números.
- product_length, product_depth, product_width

Variável do tipo float64.

product_length - 18 valores ausentes

product_depth - 16 valores ausentes

product_width - 16 valores ausentes

Os valoras ausentes foram preenchidos com recurso ao pandas interpolate.

- cluster_id

Variável do tipo object

Contém 10 valores distintos

Contém 50 valores ausentes

Os valores em falta foram preenchidos com recurso ao K-nearest neighbors.

- hierarchy1_id, hierarchy2_id, hierarchy3_id, hierarchy4_id, hierarchy5_id

Variáveis do tipo object. Contém a hierarquia dos produtos, ou seja, organização por famílias.

Começam com 3 caracteres alfanuméricos, e à medidade que se avança na hierarquia vão sendo acrescentados mais 2 à medidade que avançamos na especifidade da família de produtos
<p>O ficheiro final contém 10 colunas e 699 linhas sem ausência de valores</p>
</details>
<details>
<summary>Sales</summary>
<p>This file contains 14 columns and 8886058 lines.</p> 
<p>From this file we only imported data before 30/09/2019 because we were trying to predict sales for the next periods.</p>
<p>Therefore we were left with 8574076 lines</p>

The columns in this file are as follows:

- Unnamed: 0

Variable type int64 with index like values

This column was not adding any information to the objective at hand so it was immediatly dropped.

- store_id

Variable type object.

Contains 5 alphanumeric values

- product_id

The same characteristics as the product_id in Product

- date

Variable type object, it contains dates in the forma YYYY-MM-DD

- Sales

Variable type float64, quantity of product sold, can be decimal numbers

- revenue

Variable type float64, refers to the amount of revenue for that store, product on that date

- stock

Variable type float64, refers to the amount of stock for that store, product on that date

- Price

Variable type float64, refers to the price of a product.

Contains 89354 missing values.

These values were replaced with mean values for that specific product.

6617 missing values remained these were replaced with 0, given that we were not going to use the price as a feature

- promo_type_1

Variable type object, refers to a type of promotion

- promo_bin_1

Variable type object, classifies the intensity of the promotion

7393924 missing values replaced with none, meaning that there was not impact for that promotion

- promo_type_2/promo_bin_2/promo_discount_2/promo_discount_type_2

These columns were dropped because eventhough promo_type_2 has no missing values it doesnt add information atleast for this project, we may included in the future, however the 3 remaining ones have 8565802 missing values.
</details>
<details>
<summary>Cities</summary>
The file has 6 columns and 63 lines.

- store_id

Same characteristics as store_id in sales

- storetype_id

Column with 4 alphanumeric values, characterizes each store in a group.

- store_size

Variable type int64, represents the size of the store.

- city_id_old

Variable type object, represent and if of city

- country_id

Variable type object, refers to country tuurkey in this case

- city_code

Variable type object refers to the name of the city

To this we added columns with longitude, latitude, city population aswell as correcting the names of the cities
</details>
<details>
<summary>External Data</summary>
In this part of the notebook we created a dataframe which contains the date the season and holidays in case that day is an holiday in Turkey.
</details>
</ul>
</details>
<details>
<summary>Data Analytics</summary>
<p>In this section graphs from the data are present, with data grouped by store and date, we noticed a lot of outliers along the time, and a specific outlier present in all stores in the last week of September 2019.</p>
</details>
<details>
<summary>Modelling</summary>
<p>In this section is where the entire modeling occurs it also includes some data understanding and preparation</p>
<ul>
<details>
<summary>Data understanding</summary>
In this section we want to verify if our data is good, we have replaced missing values and cleaned the data before, but in this section we want to check if there is the correct number of weeks in each year if we are missing some years among other things.

The following stores only have information of 2 years
To these stores we need to check if they only opened in 2018 and if so check that all the weeks are present  
S0005 [2018 2019] 48 39  
S0036 [2018 2019] 46 39  
S0046 [2018 2019] 43 39  
S0061 [2018 2019] 40 39  
S0071 [2018 2019] 29 39  
S0076 [2018 2019] 42 39  
S0092 [2018 2019] 22 39  
S0109 [2018 2019] 17 39  
  
The following store only has information of 1 year  
S0007 [2019] 27  

In addition to the ones before here we are displaying other stores that are missing some weeks of information eventhough there is information for the 3 years, for store S0059 is because it only opened in the middle of 2017 and all weeks are present, for store S0136 is because it is closed in some parts of the year.  
S0059  [2017 2018 2019] 31 52 39  
S0136  [2017 2018 2019] 12 20 19  
  
We are supposed to have 39 weeks in the year of 2019 because we are trying to predict the next 5 weeks 
  
In some cases there is a real problem of prediction because for a time series analysis if we defined the seasonality as 52 weeks we need atleast 104 observations to be given a prediction which is data that we dont have.   

In this analysis we have gained even more insights on the data, we have checked that there is only 2 stores with missing dates which is good, because that means that all stores for which we don't have data since 02 January 2017 opened later then that, and it gave more insights on store S0059 that it just opened later in 2017 and doesnt have missing data.  

The stores that have missing data are stores S0136, and S0072.  

For store S0136 this was expected already.  
For store S0072 there is only one day missing, therefore we will replace it with the average of the revenue for the store  

By this analysis excluding the store S0136, we can infer that the stores that opened more recently have weeks in wich their revenue is 0, later we can verify more thorougly when this happens, for now we think that it might be in the weeks of the opening.
</details>
<details>
<summary>Prediction for stores with complete data and all years</summary>
<ul>
<details>
<summary>Data Preparation</summary>
Here we prepared the data to make the predictions after, so we've grouped the data by date weekly starting on monday and by store, we've added features based on the data we have and these features are month, weekofyear, is_open, IsWinter, IsSummer, IsSpring, IsAutumn, IsHoliday, LastWeekHoliday, NextWeekHoliday.

These features are almost all binary columns except fot weekofyear and month.
</details>
<details>
<summary>Simple Models</summary>
We firts used several simple models to make predictions to then compare with ARIMA, SARIMA and SARIMAX.
<ul>
<details>
<summary>Linear Regression and Average</summary>
</details>
<details>
<summary>Moving Average</summary>
</details>
<details>
<summary>Exponential Smoothing</summary>
</details>
<details>
<summary>Seasonal Naive</summary>
</details>
<details>
<summary>Holt's Linear trend</summary>
</details>
</ul>
</details>
<details>
<summary>Auto (S)arima(x) Weekly (revenue)</summary>
</details>
<details>
<summary>Save (S)arima(x) models</summary>
</details>
<details>
<summary>Best Model</summary>
</details>
<details>
<summary>Graphs for training and test data</summary>
</details>
<details>
<summary>Prediction</summary>
<ul>
<details>
<summary>Prepare data</summary>
</details>
<details>
<summary>Predictions</summary>
</details>
<details>
<summary>Graphs for forecast (testing)</summary>
</details>
</ul>
</details>
</ul>
</details>
<details>
<summary>Incomplete Data</summary>
<ul>
<details>
<summary>Data Preparation</summary>
Here we prepared the data for the stores that were missing dates in order to make the predictions after, so we've grouped the data by date weekly starting on monday and by store, we've added features based on the data we have and these features are month, weekofyear, is_open, IsWinter, IsSummer, IsSpring, IsAutumn, IsHoliday, LastWeekHoliday, NextWeekHoliday.

These features are almost all binary columns except fot weekofyear and month.
</details>
<details>
<summary>Simple Models</summary>
We firts used several simple models to make predictions to then compare with ARIMA, SARIMA and SARIMAX.
<ul>
<details>
<summary>Linear Regression and Average</summary>
</details>
<details>
<summary>Moving Average</summary>
</details>
<details>
<summary>Exponential Smoothing</summary>
</details>
<details>
<summary>Seasonal Naive</summary>
</details>
<details>
<summary>Holt's Linear trend</summary>
</details>
</ul>
</details>
<details>
<summary>Auto (S)arima(x) Weekly (revenue)</summary>
</details>
<details>
<summary>Save (S)arima(x) models</summary>
</details>
<details>
<summary>Best Model</summary>
</details>
<details>
<summary>Graphs for training and test data</summary>
</details>
<details>
<summary>Prediction</summary>
<ul>
<details>
<summary>Prepare data</summary>
</details>
<details>
<summary>Predictions</summary>
</details>
<details>
<summary>Graphs for forecast (testing)</summary>
</details>
</ul>
</details>
</ul>
</details>
<details>
<summary>Store S0136</summary>
<ul>
<details>
<summary>Data Preparation</summary>
Here we prepared the data for store S0136 in order to make the predictions after, so we've grouped the data by date weekly starting on monday and by store, we've added features based on the data we have and these features are month, weekofyear, is_open, IsWinter, IsSummer, IsSpring, IsAutumn, IsHoliday, LastWeekHoliday, NextWeekHoliday.

These features are almost all binary columns except fot weekofyear and month.

We knew that the store was closed in October so the prediction would be 0, however we wanted to find out what the predicition would be if the store was opende so we set the value is_open to the months of October as 1.
</details>
<details>
<summary>Simple Models</summary>
We firts used several simple models to make predictions to then compare with ARIMA, SARIMA and SARIMAX.
<ul>
<details>
<summary>Linear Regression and Average</summary>
</details>
<details>
<summary>Moving Average</summary>
</details>
<details>
<summary>Exponential Smoothing</summary>
</details>
<details>
<summary>Seasonal Naive</summary>
</details>
<details>
<summary>Holt's Linear trend</summary>
</details>
</ul>
</details>
<details>
<summary>Auto (S)arima(x) Weekly (revenue)</summary>
</details>
<details>
<summary>Save (S)arima(x) models</summary>
</details>
<details>
<summary>Best Model</summary>
</details>
<details>
<summary>Graphs for training and test data</summary>
</details>
<details>
<summary>Prediction</summary>
<ul>
<details>
<summary>Prepare data</summary>
</details>
<details>
<summary>Predictions</summary>
</details>
<details>
<summary>Graphs for forecast (testing)</summary>
</details>
</ul>
</details>
</ul>
</details>
</ul>
</details>

## Evaluation

For the evaluation of each model we used RMSE, MAE and MAPE and thw way we chose which model to use to make predictions was to check of these 3 metrics, which model had the best metrics.

Formula: RMSE = sqrt((1/n) * Σ(y_observed - y_predicted)^2)  
Formula: MAE = (1/n) * Σ|y_observed - y_predicted|  
Formula: MAPE = (1/n) * Σ|((y_observed - y_predicted)/y_observed)| * 100  

n - represents the total number of observations.  
y_observed - refers to the actual or observed values.  
y_predicted - represents the values predicted by the model.  

RMSE measures the dispersion of errors between the predicted values and the actual values. By focusing on prediction accuracy, the use of RMSE penalizes larger errors more significantly, making it sensitive to outliers and large deviations. This sensitivity proves valuable when larger errors need to be penalized disproportionately.

MAE measures the average magnitude of errors between the predicted values and the actual values. Unlike RMSE, it gives equal weight to all errors, making it less sensitive to outliers and large deviations. This characteristic is particularly useful when we need a metric that treats all errors fairly, regardless of their magnitude.

MAPE measures the relative errors between the predicted values and the actual values. Expressed as a percentage, it allows for better interpretation in practical terms. MAPE is particularly useful when we need to understand the magnitude of errors relative to the actual values and when percentage errors are relevant for the analysis.

After this process here is a table that contains the best model for each store.

|store|best_method|
|:-----:|   :----:  |
|S0002|holt|
|S0003|average|
|S0005|average|
|S0007|moving_avg|
|S0010|holt|
|S0012|average|
|S0014|seasonal_naive|
|S0015|moving_avg|
|S0016|exp_smoothing|
|S0020|holt|
|S0022|moving_avg|
|S0023|holt|
|S0026|holt|
|S0030|sarima|
|S0032|moving_avg|
|S0036|average|
|S0038|holt|
|S0039|holt|
|S0040|moving_avg|
|S0041|moving_avg|
|S0045|average|
|S0046|average|
|S0050|holt|
|S0052|moving_avg|
|S0055|seasonal_naive|
|S0056|holt|
|S0058|holt|
|S0059|moving_avg|
|S0061|regression|
|S0062|moving_avg|
|S0067|holt|
|S0068|arima_nom|
|S0071|moving_avg|
|S0072|holt|
|S0073|exp_smoothing|
|S0076|holt|
|S0077|arima_nom|
|S0080|exp_smoothing|
|S0083|moving_avg|
|S0085|average|
|S0086|average
|S0088|holt|
|S0089|arima_nom|
|S0091|average|
|S0092|average|
|S0094|holt|
|S0095|exp_smoothing|
|S0097|moving_avg|
|S0099|moving_avg|
|S0102|moving_avg|
|S0104|holt|
|S0107|seasonal_naive|
|S0108|holt|
|S0109|average|
|S0120|seasonal_naive|
|S0122|exp_smoothing|
|S0126|exp_smoothing|
|S0131|holt|
|S0132|holt|
|S0136|regression|
|S0141|average|
|S0142|moving_avg|
|S0143|exp_smoothing|
