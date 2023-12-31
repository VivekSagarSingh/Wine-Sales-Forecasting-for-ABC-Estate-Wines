
# Wine-Sales-Forecasting-for-ABC-Estate-Wines
• Analysed historical monthly sales data & created multiple Time Series Forecasting models for 2 different wine products, Sparkling wine & Rose Wine.

• Recommended SARIMA model as the optimum forecasting model for Sparkling wine & Triple Exponential Smoothing model for Rose wine, to predict monthly sales for the next 12 months along with appropriate lower
and upper confidence limits.

## Problem Statement

For this particular assignment, the data of two different types of wine sales in the 20th century is to be analysed. Both of these data are from the same company but of different wines. As an analyst in the ABC Estate Wines, we are tasked to analyse and forecast Wine Sales in the 20th century.

### NOTE: Here, for illustration purposes I have shared the detailed report for the first product i.e. 'Sparkling Wine' only. The analysis for 'Rose wine' can be found in the ipynb file attached.

## Steps involved:
## 1. Read the data as an appropriate Time Series data and plotted the same.
<img width="584" alt="Screenshot 2023-12-31 at 5 02 47 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/9fc03a8e-5c44-4e5d-b706-d593295966af">



## 2. EDA
### Univariate Analysis:
Since we have a time series data and that too with a single variable, we will only be
able to do limited univariate analysis.

<img width="566" alt="Screenshot 2023-12-31 at 5 04 35 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/19c97be7-65a9-4038-a56a-8fdefea3d819">


As we can see there are no missing values in the dataset.
There is only one variable named ‘Sparkling’ and it is of Integer datatype.


<img width="246" alt="Screenshot 2023-12-31 at 5 05 42 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/de63a8ff-dbe0-461a-aa97-a62f3a3da848">

Looking at the spread of the data i.e. the min, 25th, 50th and 75th percentile and
comparing them to the max value , we can clearly see that there is skewness and
presence of outliers in the data. But since it is a Time series data it may have some
peak seasons which is clear from the time series plot displayed above. So we are not
going to treat these outliers as they have a strong seasonality component. This will
become further clear after seeing the decomposition plot.

### Yearly Boxplot:

<img width="580" alt="Screenshot 2023-12-31 at 5 07 41 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/f03b7966-c30c-4dba-882d-b60bba9053ed">


#### Insights:

• As we can see there are a few outliers across all the years. These are probably the
months which had peak sales. To confirm this we will have a look at the monthly
boxplots.

• Also it seems that in the year 1995, the sales have been quite low compared to other
years, but the reason behind this is completely statistical and has got nothing to do
with the business aspect of it.

• The reason for this is that the dataset contains the sales data only till July of 1995 so
obviously when compared across all years 1995 will have only 7 months of data
while other years will have 12 months of data.

• Looking at the average units sold in an year, represented by green triangle , we can
see that there is very little change across different years.

### Monthly Boxplot:
<img width="580" alt="Screenshot 2023-12-31 at 5 08 21 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/79fab29f-29dc-46c9-b461-8e434eb9716d">


#### Insights:
• There is a clear distinction of ‘Wine Sales' within different months spread across
various years.

• For the first 6 months, the number of units sold are maintaining more or less a fixed
range I.e. between 1000 to 2500 units across all years.

• But starting July it starts increasing drastically reaching upto more than 7000 units
in the month of December.

### Pivot table and Sales graph for monthly Wine Sales across years:

<img width="381" alt="Screenshot 2023-12-31 at 5 08 47 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/cee12ee1-6fe9-4bd4-b5a4-76c1ae720770">

<img width="581" alt="Screenshot 2023-12-31 at 5 09 40 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/d66918b6-99f6-4d34-abc2-f7f791bed85e">


#### Insights:
• Here we can clearly see that sales in month of December and November are a cut
above the rest of the months with December being the month with the most sales
throughout the years.

• The absence of data from year 1995 for months of august to December is also
clearly visible here.

• But even so these cannot be considered as missing values as the data collection
itself has ended in this case with last data entry being for July 1995. And the data
after this point will come under forecasting.

### Empirical Cumulative Distribution (ECDF) plot:
<img width="581" alt="Screenshot 2023-12-31 at 5 10 01 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/f0ae9605-be38-43bf-a3c4-1006c033a1fc">



#### Insights:
• Here it becomes evidently clear that 60% of the total sales are in the range of 1000
to 2000 units.

• Then the next 20% of the sales fall in the range of 2000 to 3000 units while the last
20% gets saturated over the span of 3000 to 7000 units.

• These observations are in tune with the observations obtained from the previous
plots.




## 3. Data Decomposition

### Additive Decomposition:
<img width="498" alt="Screenshot 2023-12-31 at 5 10 33 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/466de48d-0093-4453-9747-b2c011f58ac1">


In additive decomposition, as we can see, the residuals are located around 0 from the
plot of the residuals in the decomposition.

### Multiplicative Decomposition:
<img width="498" alt="Screenshot 2023-12-31 at 5 10 49 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/7ab05e82-5308-4ab8-bd31-c52b4e11e3d6">


In multiplicative decomposition, as we can see, the residuals are located around 1 from
the plot of the residuals in the decomposition.

Comparing the two decomposition plots, it seems that for this dataset, **Multiplicative
decomposition is a better fit** as residuals are more concentrated around 1 in this plot
as compared to around 0 in the additive plot.

By looking at the trend line, we can see that in the initial years the sales remained
more or less stables around the 2300 mark, but around year 1987 sales got boosted
peaking at 2800 mark in 1988 and then it consolidated around 2500 to 2600 mark.

**Also looking at the seasonal plot, it is evident that there is a 12 month seasonality.**

## 4. Splitting the data into training and test

#### Here, as specified in the problem statement the test data is starting from the year 1991.

### Plotting the train and test data:
<img width="577" alt="Screenshot 2023-12-31 at 5 12 05 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/db5d2eea-8b93-46fc-9d6d-0c71ceaed3ed">


## 5. Building Models
#### Models to be built: 
* Linear Regression
* Naïve forecast
* simple average model
* All the exponential smoothing models (alongwith additive & multiplicative errors)
* ARIMA
* SARIMA

data and evaluate the model using RMSE on the test data.
Other models such as . should also be built on the training
data and check the performance on the test data using RMSE.
Building Models:

### Model 1: Linear Regression
We know that Linear regression needs at least one independent variable X to explain
the target variable, Y but here we only have one variable available that is Wine sales
'Sparkling', as we converted the date-time variable into the index.

So we have defined an independent variable and assigned it to a new column ‘time'
separately for both train and test data.

<img width="578" alt="Screenshot 2023-12-31 at 5 12 42 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/125d30ab-668b-4b45-8ed2-385b4df018f1">


Now that our training and test data has been modified, let us go ahead use Linear
Regression to build the model on the training data and then test the model by doing a
forecast on the test data.

#### Some Linear Regression forecast values on test data:
<img width="261" alt="Screenshot 2023-12-31 at 5 21 56 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/b091ecb2-fe31-4222-9350-86ec76a36193">


#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="579" alt="Screenshot 2023-12-31 at 5 23 34 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/71534278-e85c-4119-b8fc-65304aa1e8d8">


#### Inference:
• As we can see from the forecast plot, linear regression is not a good model for this
test data as the data itself is not linear to begin with.

### Model 2: Naive Approach
In the Naive model, the prediction for tomorrow is the same as today and the
prediction for day after tomorrow is same as tomorrow.

Therefore we can say that as the prediction for tomorrow is same as today, the
prediction for day after tomorrow should also be today.

By following this same logic we will end up with one single value as the forecast value
of the complete test data, and that value would be the data entry just before the start
of the test data, I.e. the sales value belonging to 1990-12-01 which is 6047.

#### Some Naive forecast values on test data:
<img width="164" alt="Screenshot 2023-12-31 at 5 24 37 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/7ad5a68e-094a-475b-94e6-a24416d98734">


#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="580" alt="Screenshot 2023-12-31 at 5 25 43 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/b0045243-81f7-4b08-8d98-6e81a201026d">


#### Model Evaluation by comparing test RMSE values from the previous models:

<img width="185" alt="Screenshot 2023-12-31 at 5 26 27 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/599a2511-679c-4593-bb87-e7cb5307fad4">

#### Inference:

• Since the assumption behind Naive forecast is quite arbitrary and not practical
when put to real world scenarios, it is obvious that this model will not be a good fit
for the test data.

• Comparing it with the Linear regression model, the LnR model still performed better
than the Naive model as per the Test RMSE value.

### Model 3: Simple Average

In simple average method, we forecast by simply using the average of the training
values.

#### Some forecast values on test data:
<img width="239" alt="Screenshot 2023-12-31 at 5 27 21 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/7cc03452-5f44-4c21-92b6-a56fa1131764">


#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="577" alt="Screenshot 2023-12-31 at 5 28 00 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/ba07d2df-e9ea-4862-8473-8c1b70252d42">


#### Model Evaluation by comparing test RMSE values from the previous models:
<img width="205" alt="Screenshot 2023-12-31 at 5 28 31 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/8987c243-d4ee-4f34-ad22-39a05f5d23e6">


#### Inference:
• Like the previous models this model is also not a good fit since it relies on the
average of all the training data values, which is too simple a logic for a real world
dataset.

• But among the models built thus far simple average model performs slightly better
than the other two models as per the Test RMSE value.

### Model 4: Simple Exponential Smoothing
This model uses a weighted average of past observations to make predictions. It is a
basic form of exponential smoothing and therefore the weighted average doesnot
change in this particular smoothing model. This model does not do well in the presence of the trend.

#### Some forecast values on test data:
<img width="220" alt="Screenshot 2023-12-31 at 5 29 44 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/872a0f19-e421-40c7-abeb-c27db8636e2e">


#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="575" alt="Screenshot 2023-12-31 at 5 31 48 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/0fa0de2c-3884-458a-b5fc-ed538ecf122c">


#### Model Evaluation by comparing test RMSE values from the previous models:
<img width="271" alt="Screenshot 2023-12-31 at 5 32 46 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/d1a56f85-aae1-448c-8d07-8fc9cea2bb81">


#### Inference:
• Since it is a simple form of smoothing and our data clearly has a trend, therefore not
a good fit.

• Compared to other models it performed just below Simple Average model as per
the Test RMSE value.

### Model 5: Double Exponential Smoothing (Holt’s Linear Method)
This model is an extension of SES(Single Exponential Smoothing) known as Double
Exponential model which estimates two smoothing parameters Thus taking care of the
drawback of SES.

• Two separate components are considered: Level and Trend.

• Level is the local mean.

• One smoothing parameter α corresponds to the level series

• A second smoothing parameter β corresponds to the trend series.

• But this model also has a drawback, it doesnot do well when data has
seasonality.
#### Some forecast values on test data:
<img width="181" alt="Screenshot 2023-12-31 at 5 34 09 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/ce5e4a49-03eb-4a7f-96b2-242ec5dceb74">


#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="574" alt="Screenshot 2023-12-31 at 5 35 58 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/1ec887c3-4d80-4424-99de-c9e07e39f0dd">


#### Model Evaluation by comparing test RMSE values from the previous models:
<img width="264" alt="Screenshot 2023-12-31 at 5 36 57 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/df021c40-32b1-4e0d-8ffd-ec6b9d6f80d1">


#### Inference:
• Since our data has quite a prominent seasonality, this is not a good fit.

• Even though this model is supposed to perform better than simple exponential
smoothing , it gas not done so in our case. This is probably because the data
doesnot have a well defined linear trend, which makes it difficult to predict when
trend is taken into account.

### Model 6: Triple Exponential Smoothing (Holt Winter's linear method with ‘additive errors’)
• In addition to alpha and beta, a new parameter gets added here called gamma
which takes care of seasonality, thus making this form of smoothing better than the
other two.

• Here we have taken triple smoothing model with additive errors, but from the
decomposition plot we saw that our dataset is more likely to have multiplicative
errors which we will see in the next model.

#### Some forecast values on test data:
<img width="223" alt="Screenshot 2023-12-31 at 5 37 53 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/22697df4-9847-4948-a8d6-0a606f26461d">


#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="575" alt="Screenshot 2023-12-31 at 5 38 46 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/edfe945b-e2a0-43d0-833a-38ef6345cc5b">


#### Model Evaluation by comparing test RMSE values from the previous models:
<img width="304" alt="Screenshot 2023-12-31 at 5 40 59 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/abde6417-b9b2-4b96-8581-a0c9a33ed3e2">


#### Inference:
• Here we can see that the RMSE score improved drastically as compared to other
models, as triple smoothing model takes care for seasonality too along with trend.

• Till now this is the best performing model.


### Model 7: Holt Winter's linear method with ‘multiplicative’ errors
As discussed above triple exponential smoothing can also be applied for multiplicative
errors which we will now see.

#### Some forecast values on test data:
<img width="172" alt="Screenshot 2023-12-31 at 5 42 06 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/a41258a6-3303-4019-97e1-c6d43f7d2241">



#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="578" alt="Screenshot 2023-12-31 at 5 42 42 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/e4a2a53d-215c-4dc9-9cf6-be53cb759e11">

<img width="469" alt="Screenshot 2023-12-31 at 5 43 04 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/c8570784-f5d8-4ffa-9f06-558b67348934">
<img width="448" alt="Screenshot 2023-12-31 at 6 04 43 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/2ec24fb8-5330-4523-99e7-c6d14197cf7e">



#### Model Evaluation by comparing test RMSE values from the previous models:
<img width="334" alt="Screenshot 2023-12-31 at 6 08 28 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/2b93990d-af64-47d6-be62-3150783734fa">




#### Inference:
• This model has also performed quite well when compared to other models except
the previous model I.e. triple exponential smoothing model with additive errors.

• But we considered this to instead perform better since the errors or residuals in the
dataset are more likely to be multiplicative than additive.

• Therefore we will apply this model once more using the brute force method to
determine the best values for the parameters alpha, beta and gamma.

### Model 8: Using Brute force method i.e. best parameters (alpha, beta and gamma) for Holt Winter's linear method with multiplicative errors

The brute force method for parameter determination involves systematically trying out
different parameter values within a specified range and evaluating the performance of
the model for each combination of parameters.

#### Determining the best values for parameters alpha, beta and gamma based on the Test RMSE values :
<img width="368" alt="Screenshot 2023-12-31 at 6 08 59 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/8fdba66f-d9af-4fd9-a9b9-1eb1fb099685">

The values so obtained are alpha = 0.3, beta = 0.3, gamma = 0.3, for a test rmse value
of 361.397, and the same can be seen in the above figure.

#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="526" alt="Screenshot 2023-12-31 at 6 09 32 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/576e2e10-6d7d-4bfb-9e5f-c3c3c5e4e1c7">

#### Model Evaluation by comparing test RMSE values from the previous models:
<img width="334" alt="Screenshot 2023-12-31 at 6 09 51 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/993c70b1-1329-4ed3-ba26-dc7d90699a69">

#### Inference:
• As we can see after applying the brute force method to get the best parameters,
triple smoothing with multiplicative errors performed better than the model with
additive errors. Thus becoming the best performing model till now.

• But this creates a question as to whether the model with additive errors can also
perform better with brute force method so much so that it might even surpass this
current multiplicative model.

• It can happen but not with this dataset as we have already discussed that this
dataset contains multiplicative errors. Also the proof that brute force method won’t
improve the additive error model for this particular dataset is present in the
attached python file where that model is also build.

## Checking for stationarity of the time series data (at alpha = 0.05) using Dickey-Fuller Test:

**NOTE : We are checking for stationarity in the data as it a pre-requisite for ARIMA & SARIMA models that the data be stationary.**

### Step 1 : Checking for stationarity using Dickey-Fuller Test :

**• Null Hypothesis, H0 :** Time Series is non-stationary.

**• Alternate Hypothesis, Ha :** Time Series is stationary.

if p-value < 0.05 (alpha value) then null hypothesis: Time series data is non-stationary
is rejected,

if not, then null hypothesis is true i.e. Time series data is indeed non-stationary.

#### Dickey-Fuller (DF) Test results:
<img width="243" alt="Screenshot 2023-12-31 at 6 10 26 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/29869eef-65b5-4291-988d-c0b85c10bdc6">

**the p-value is 0.6 which is clearly > 0.05, thus Null hypothesis is true. Thus Time series data is not stationary.**

### Step 2 : Making the time series data stationary using the differencing method:
#### Non differenced (or) Original Time series data:
<img width="489" alt="Screenshot 2023-12-31 at 6 10 52 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/111b62c8-0320-44a7-ae50-2e3561aaf06b">

#### Performing differencing ( d=1 ) on the non-stationary data:
<img width="489" alt="Screenshot 2023-12-31 at 6 11 20 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/c8f00fb9-a3c0-4a9f-95f7-a64c5dfcf2d8">

#### Checking for stationarity using the Dickey-Fuller test for the differenced(d=1) data:
<img width="197" alt="Screenshot 2023-12-31 at 6 11 38 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/e4a5d1a6-8a3d-48a4-9501-d44a5bcf62b1">

The p-value is 0 which is clearly < 0.05, thus Null hypothesis is rejected i.e. Time series
differenced(d=1) data is Stationary.

**Thus we have achieved Stationarity**

### Now building an automated version of the ARIMA/SARIMA models:
#### Here parameters were selected using the lowest 'AIC' (Akaike Information Criteria) on the training data and the models were evaluated on the test data using RMSE.

### Model 9: ‘ARIMA’ model based on lowest Akaike Information Criteria (AIC).
• ARIMA stands for Auto Regression Integrated Moving Average.

• As the name suggests it combines autoregression (AR), differencing (I), and moving
average (MA) components. ARIMA models are capable of capturing various patterns
and dependencies in time series data.

• The basic ARIMA model has does not explicitly capture seasonality. It is more
suitable for capturing trends and dependencies in stationary time series data.

• However, ARIMA can be extended to incorporate seasonality by introducing
seasonal components, resulting in a model called SARIMA (Seasonal ARIMA), which
we will look into next.

• ARIMA has 3 parameters:
    
    1. p = non-seasonal AR order
    2. d = non-seasonal differencing
    3. q = non-seasonal MA order
### Determining the best parametric values p, d and q based on lowest AIC value:
<img width="141" alt="Screenshot 2023-12-31 at 6 12 19 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/b2401cc3-66a2-496a-b1d8-c0a2c1304778">


#### The best parameters thus obtained are p = 2, d = 1 and q = 2. For a lowest air value of 2213.509.

### Some forecast values on test data:
<img width="321" alt="Screenshot 2023-12-31 at 6 12 45 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/3b1a1185-3ef2-4b6a-a3dc-823aecfc4f99">


### ARIMA Summary Chart:
<img width="558" alt="Screenshot 2023-12-31 at 6 13 03 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/5f7d3d27-1976-454f-b25c-8cfc996ce8ce">

### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="578" alt="Screenshot 2023-12-31 at 6 13 55 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/a5f16a2b-923b-4bc5-ae54-ec58d17eb9a9">

### Model Evaluation by comparing test RMSE values from the previous models:
<img width="311" alt="Screenshot 2023-12-31 at 6 15 19 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/f4e8683b-0007-4d8c-b47b-4d4eae42068a">


### Inference:
• Since ARIMA doesnot capture seasonality, and our data has a strong seasonality
component, this model is bound to perform poorly, which is exactly what has
happened.

### Model 10: ‘SARIMA’ model based on lowest Akaike Information Criteria (AIC).
• SARIMA also known as Seasonal ARIMA, is an extension of ARIMA where 4 new
parameters are introduced to capture the seasonality component, making the total
number of parameters as 7 in the SARIMA model.

• 7 parameters of SARIMA:
        
        1. p = non-seasonal AR order
        2. d = non-seasonal differencing
        3. q = non-seasonal MA order
        4. P = seasonal AR order
        5. D = seasonal differencing
        6. Q = seasonal MA order
        7. S = time span of repeating seasonal pattern
#### Determining the best parametric values p, d and q based on lowest AIC value:
<img width="218" alt="Screenshot 2023-12-31 at 6 16 25 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/c716a743-495d-4511-9fb4-098c0b7fc09e">

The best parameters thus obtained for a lowest AIC value of 1382.347 are:
**p=1, d=1, q=2 and P=0, D=1, Q=2 and S=12.**

#### Some forecast values on test data:
<img width="319" alt="Screenshot 2023-12-31 at 6 16 49 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/0306d9de-5f17-4b5f-894e-5e32196a0e0c">

Here, ‘mean’ column gives the actual forecast values and the ‘mean_ci_lower’ and
‘mean_ci_upper’ columns give the range of confidence interval.

#### SARIMA Summary Chart:
<img width="580" alt="Screenshot 2023-12-31 at 6 17 22 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/8de172df-2e9a-4367-aef0-bd537fb63bc9">


#### Residuals diagnostic plots:
<img width="569" alt="Screenshot 2023-12-31 at 6 17 49 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/73230ba5-4ec6-4f7d-8a82-18c9a1127057">

The above 4 plots in the residuals diagnostic plots tell us:

**• Standardized residuals plot:** The top left plot shows 1-step-ahead standardized
residuals. If model is working correctly, then no pattern should be obvious in the
residuals. As we can see no such pattern is visible here.

**• Histogram plus estimated density plot:** This plot shows the distribution of the
residuals.The orange line shows a smoothed version of this histogram, and the
green line shows a normal distribution. If the model is good these two lines
should be the same. Here we see small differences between them, which
indicate that our model is doing just well enough.

**• Normal Q-Q plot:** The Q-Q plot compare the distribution of residuals to normal
distribution. If the distribution of the residuals is normal, then all the points
should lie along the red line, except for some values at the end, which is exactly
happening in this case.

**• Correlogram plot:** The correlogram plot is the ACF plot of the residuals rather
than the data. 95% of the correlations for lag >0 should not be significant (within
the blue shades). If there is a significant correlation in the residuals, it means that
there is information in the data that was not captured by the model. Here too our
model is working as expected.

#### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="566" alt="Screenshot 2023-12-31 at 6 18 23 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/bcc50169-e41a-43a3-8465-3fe409f1570c">

<img width="566" alt="Screenshot 2023-12-31 at 6 19 31 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/c66dfb62-78b3-4fa4-a0db-bdceb7fa94d3">

#### Model Evaluation by comparing test RMSE values from the previous models:
<img width="342" alt="Screenshot 2023-12-31 at 6 20 01 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/a363f03a-f7d9-4e87-9f10-bdc18e99fa3e">


#### Inference:

• Since SARIMA captures seasonality, and our data has a strong seasonality
component, as expected this model is the second best fit, falling behind only triple
exponential smoothing.

## 6. Created a data frame with all the models builtalong with their corresponding parameters and the respective RMSE values on the test data.

#### Performance metrics Table (comparison of all the models):
<img width="570" alt="Screenshot 2023-12-31 at 6 20 33 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/4f5e84eb-46a9-484d-ad05-56ea2bfe8dba">



## 7. Based on the model-building exercise, built the most optimum model(s) on the complete data and predicted 12 months into the future with appropriate confidence intervals/bands.

### Final model: The Best performing models as per Test RMSE is as follows:
<img width="365" alt="Screenshot 2023-12-31 at 6 20 59 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/d28ea268-0708-4b4d-8987-c50da865bc28">


As we can see the test rmse values for the top three models are pretty close , and the
top two models are both Triple exponential smoothing models. Therefore we will make
two final models, one for triple exponential smoothing and one for SARIMA which is
the third best performing model.

### Final Model 1: Using Brute force method for best parameters (alpha, beta and gamma)for Holt Winter's linear method with multiplicative errors

#### 12 months forecast values on the original full data:
<img width="160" alt="Screenshot 2023-12-31 at 6 21 42 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/f2a0d0aa-ee15-46d7-aff7-e80cd9e0dbf0">


#### Determining the best values for parameters alpha, beta and gamma based on the Test RMSE values :
<img width="284" alt="Screenshot 2023-12-31 at 6 21 58 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/67190b64-f71e-4c92-910d-0a006f740bce">


The values so obtained are alpha = 0.3, beta = 0.3, gamma = 0.4, for a test rmse value
of 347.614, and the same can be seen in the above figure.

#### Plotting the complete data alongwith forecasted values using brute force alpha, beta and gamma and getting RMSE value:
<img width="561" alt="Screenshot 2023-12-31 at 6 24 32 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/3c0684a1-2e7f-41eb-b676-1b28a75eae0b">


#### Model Evaluation by comparing test RMSE values from the previous models:
<img width="304" alt="Screenshot 2023-12-31 at 6 24 00 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/580c2176-2607-47f7-835b-8de3a534d015">


#### Inference:
• Here we can see that the RMSE value calculated is pretty low, although strictly
speaking it cannot be compared with all the other models build till now as the
training set has been now changed to full data, and forecast window has also been
changed to 12 months.

• But what we can do is compare the two final models based on their RMSE values to
see which one has performed the best among the two.



### Final Model 2: ‘SARIMA’ model based on lowest Akaike Information Criteria (AIC).

#### Determining the best parametric values (p,d,q) and (P,D,Q,S) based on lowest AIC value:
<img width="218" alt="Screenshot 2023-12-31 at 6 25 27 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/81d77770-0548-4b0e-8e59-86b2a147b2c7">


The best parameters thus obtained for a lowest AIC value of 2184.006 are:
**p=0, d=1, q=2 and P=0, D=1, Q=2 & S=12.**


#### 12 months forecast values on the original full data:
<img width="312" alt="Screenshot 2023-12-31 at 6 25 49 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/3daaa8c4-c3ac-4293-b43a-c829ae692181">

Here, ‘mean’ column gives the actual forecast values and the ‘mean_ci_lower’ and
‘mean_ci_upper’ columns give the range of confidence interval.

#### SARIMA Summary Chart:
<img width="567" alt="Screenshot 2023-12-31 at 6 26 18 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/5b506d07-032a-48c1-9905-58ba70442eef">


#### Residuals diagnostic plots:
<img width="567" alt="Screenshot 2023-12-31 at 6 26 40 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/fe03eb93-18f3-476f-9c9d-1fbf40a7bd8c">


As already discussed, the above 4 plots in the residuals diagnostic plots shows that
the model is behaving as it should:

**• Standardized residuals plot:** As we can see no definite pattern is visible here.

**• Histogram plus estimated density plot:** Here we see small differences between
the two lines, which indicate that our model is doing just well enough.

**• Normal Q-Q plot:** Here, the distribution of the residuals is normal, as all the
points are lying along the red line, except for some values at the end.

**• Correlogram plot:** Here, all the correlations for lag >0 are within the blue shades
meaning they are not significant. If there is a significant correlation in the
residuals, it means that there is information in the data that was not captured by
the model. Here too our model is working as expected.

### Plotting the Training data, Test data and the forecasted values and getting RMSE value:
<img width="567" alt="Screenshot 2023-12-31 at 6 27 29 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/8ff7182e-6c9a-4cf0-a4a7-07bf52b11d76">


## 8. Final Model Evaluation by comparing Model RMSE values of the above 2 best performing models:
<img width="348" alt="Screenshot 2023-12-31 at 6 27 45 PM" src="https://github.com/VivekSagarSingh/Wine-Sales-Forecasting-for-ABC-Estate-Wines/assets/153344691/3defe76c-1c0c-4911-a723-8c9a9f32c99e">

### Inference:
• Here we can see that even though SARIMA model was the third best performing
model based on the test RMSE value with our predefined training set and testing
set.

• When it came to training the model on the complete original data and forecasting
for next 12 months, SARIMA performed even better than Brute force Triple
exponential Smoothing model and that too by a large margin, given the difference
in the model RMSE values for the two final models.

**Hence, our final best performing model for forecasting 12 months into the future is SARIMA Model.**

## 9. Commenting on the most optimum model thus built and reporting the findings and suggestions that the company should be taking for future sales.
• Coming to the model predictions part we have already seen in detail how the
different models built performed with respect to the dataset provided.

• Overall Triple exponential smoothing using brute force method with multiplicative
errors performed well along with SARIMA when these models were built on the train
set and forecasting was done on the test set.

• But when we trained the same models on the complete dataset and forecasted for
12 months in future , SARIMA performed the best out of the two.

• This means that when it comes to forecasting on unknown data , SARIMA performs
better than Triple exponential smoothing models.

## 10. Some Business Insights:
• The first point to notice here is that the trend line is not linear, it first decreased then
increased slightly then there was an abrupt increase leading to slight decrease
again and then saturating.

• An important thing to notice is the sales are really low in the first 6 months of every
year, gradually increasing and reaching its peak in the month of November and
December.

• This can be used as a baseline by the production and logistics team to avoid
wastage as well as shortage of supplies.

• This also provides an opportunity for the company to provide some extra services or
discounts to the customers in the first 6 months to increase the sales. As it is quite
clear from the sales in second half of the year that there is room for increase in
sales.

• Another thing is as the sales are quite high in months of November and especially
December, company can try to capitalise on this by throwing in lucrative offers.
