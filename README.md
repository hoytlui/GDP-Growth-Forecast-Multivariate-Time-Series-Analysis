# GDP Growth Forecast with Multivariate Time Series Analysis

*Macroeconomics affects our everyday life in all kinds of aspects. For examples, employment and unemployment, government welfare, inflation, daily goods and services, investment, housing, and more. The main goals of this project are to inform us how the economic indicators affect each other, and to provide insights of predicting how they may play out in the next 2 years.*

## 1. Data
I downloaded all datasets from Organization for Economic Co-operation and Development (OECD), which is a reliable source to provide all the data below for free.

## 2. Method
In this project, we would predict GDP growth from other variables of the U.S. using multivariate time series analysis.
We applied Augmented Dickey-Fuller and KPSS tests for stationarity, and Johansen test for cointegration. We checked their correlation relationship with heatmap. Then, we fit the data into a VAR model, selected the lag order and forecasted the results.
In the end, we evaluated the time series using impulse response analysis and forecast error variance decomposition (FEVD) before inverting them back to their original form to plot the prediction trend.


## 3. Data Wrangling

**Data collection:**
1.	Household debt to income ratio. We are all aware of what caused the subprime mortgage crisis in 2008 – right, too much debt. So, this will be the main focus.
2.	Unemployment rate. We always hear about the unemployment rate of a country, and how many workers lose their jobs in a month.
3.	Housing price to income ratio and housing price to rent ratio. Housing problem is a global concern. Everyone complains how uncontrolled the housing market is. These ratios represent a measure of affordability
4.	Government spending to GDP ratio. Does it push the GDP growth or is it correlated if the government spend more to stimulate the economy? We will find out.
5.	Inflation rate (or CPI). As long as the country is not experiencing hyperinflation, I believe inflation rate is proportional to GDP growth.
6.	Producer price indices (PPI). This is related to manufacturing price. It measures the average changes in prices received by domestic producers for their output.

**Data cleaning:**

We need to take into consideration of the followings:
-	Frequency. Do we want to work with monthly, quarterly or annual data?
-	What are the values we are comparing against? For examples, over last period or over last year?
-	What are the availabilities of our dataset? Some of them has a broad range of frequency available, e.g., monthly, quarterly and annual. While some only has annual data.


## 4. Exploratory Data Analysis

**Stationarity test:**

Stationarity tests are used to determine the presence of unit root in the series through different ways. Augmented Dickey-Fuller test is used as a difference stationarity test, while KPSS test is used as a trend stationarity test. Our goal is to make the trend to be strict stationary.

|                               |                | Augmented Dickey-Fuller test<br>(Test for difference) |                  |   |
|-------------------------------|----------------|-------------------------------------------------------|------------------|---|
|                               |                | Stationary                                            | Non-stationary   |   |
| KPSS test<br>(Test for trend) | Stationary     | Strict stationary                                     | Trend stationary |   |
|                               | Non-stationary | Difference stationary                                 | Non-stationary   |   |


Below is a snippet of the stationarity test on GDP growth, which passes both Dickey-Fuller and KPSS tests at a significant level of 95%. All the time series in this project will be passed through both tests to decide if it is needed for transformation such as differencing.

![3 18 stationarity test gdp](https://user-images.githubusercontent.com/36130927/128287953-fb1ac095-e361-49b0-a2a8-493813100483.png)


**Correlation heatmap:**

We also looked at correlation heatmap to have a preliminary idea of how correlated each variable is against each other.

![3 20 heatmap](https://user-images.githubusercontent.com/36130927/128288132-f07c45d6-91d6-4480-851e-4464d8db349b.png)


**Cointegration test:**

Time series that are cointegrated with each other suggests that they will follow the same long-run path since they presumably have some common factor. Johansen test is used to check the cointegration up to a maximum of 12 time series, estimating long-run equilibrium between variables.

The trace statistics below tells us whether the sum of the eigenvalues is 0. At r ≤ 5, we can reject the null hypothesis at 95% confidence level and accept the alternate hypothesis, suggesting the series are cointegrated.

![4 0a trace stat](https://user-images.githubusercontent.com/36130927/128289525-d828adcc-a991-4f96-a42a-0357855650e6.png)

The eigen statistics below tells us how strongly cointegrated the series are or how strong is the tendency to mean revert. At r ≤ 5, we can reject the null hypothesis at 95% confidence level and accept the alternate hypothesis, which means the series are cointegrated.

![4 0b eigen stat](https://user-images.githubusercontent.com/36130927/128289527-ad792565-007d-4d37-82cc-f8008c254cd2.png)


## 5. Modeling

We used Vector Autoregression (VAR) for multivariate time series analysis because it is able to understand and use the relationship between several variables, which is particularly useful for describing the dynamic behavior of the data and also provides better forecasting results.

**Lag order selection:**

We chose lag = 12 because it returns the lowest AIC between in the range of 1 to 12 without returning errors.

![4 1 var model summary](https://user-images.githubusercontent.com/36130927/128289491-232c1834-3aa4-4083-9eb0-be9b671eea58.png)


**Forecasting:**

We forecasted 8 steps ahead for each variable with 12 lags length, along with 2 asymptotic standard errors.

![4 4 forecasting](https://user-images.githubusercontent.com/36130927/128289466-b04d0dc4-c1a8-4cc9-b804-7aa89a5d14f7.png)


## 6. Evaluation/Structural Analysis

**Impulse response analysis:**

We want to know the response of one variable to an impulse in another variable in this analysis.

![4 5 impulse response analysis](https://user-images.githubusercontent.com/36130927/128289454-2ca662dc-7bf5-4eb4-a8c9-388d2d58f389.png)


**Forecast error variance decomposition:**

It indicates how much of the forecast error variance of each variable can be explained by the exogenous shocks to the other variables in each of the steps in the forecast.

![5 2 fevd](https://user-images.githubusercontent.com/36130927/128289436-7952fd9f-09d4-4df9-b720-b0f9883940cb.png)


**Inverting:**

Finally, the graphs below are the prediction of each time series after being inverted back to their original form.

![5 4 gdp growth prediction](https://user-images.githubusercontent.com/36130927/128289118-85412664-9216-483e-a81a-8d1ebd7c9c9c.png)

![5 5 govt spending to gdp prediction](https://user-images.githubusercontent.com/36130927/128289245-325a92bf-f272-4177-b48a-1f46c265b257.png)

![5 6 unemployment rate prediction](https://user-images.githubusercontent.com/36130927/128289246-b6560c3b-9dda-4532-90d8-7a9616e5b17b.png)

![5 7 rent to income prediction](https://user-images.githubusercontent.com/36130927/128289247-a32854c5-26ca-4b75-bd5f-e9160d3c84e1.png)

![5 8 inflation prediction](https://user-images.githubusercontent.com/36130927/128289250-60a74adb-55d8-440a-95d7-e8518ad1a340.png)

![5 9 ppi prediction](https://user-images.githubusercontent.com/36130927/128289251-98cd1656-5b9c-4ddc-85d0-77f71ea6bd7d.png)


## 7. Takeaways

In a nutshell, this project tells us few key takeaways:
-	As shown in the heatmap, unemployment rate has the highest correlation with GDP growth, whereas rent to income ratio has the lowest correlation with GDP growth.
-	From impulse response analysis, rent to income ratio has a huge effect on GDP growth.
-	From FEVD, standard error of GDP growth forecast most likely won't be contributed by PPI, meaning it has little effect on the forecast.
-	From Johansen test, we may only need 2 variables from our dataset to make the existing time series cointegrated to provide sufficient predictive power.


## 8. Further Work

-	Based on the results we obtained from Johansen test for cointegration, we can eliminate all columns but 1-2 most significant ones along with the GDP growth, which is our target variable. This would in turn have less unnecessary effect or noise for our prediction.
-	We can replace the most insignificant variables with other variables to see the new predictive power, as we have already found out some of them have little effect on GDP growth.
-	Going forward, we can also use the same approach to test the other countries of our choice. We may even find surprising results and get signals prior to a potential market crash.


## 9. Business Recommendation

The essence of this model is to show us the dynamic relationship between the variables, the number of time series used to be sufficient enough to make prediction, the ideal lag order to forecast, the portion of the error variance can be explained by which variable, etc. Knowing this will help us select more variables or remove existing variables, and fine-tune our parameters for better forecasting results.

This model was demonstrated to project GDP growth. However, we can use the same approach to project unemployment rate, inflation rate, or any other variables used in this project. We can also add other variables such as foreign investment, country current account balance, household spending, just to name a few, into our prediction. In trading and investing environment, we can change our variables into other types like stocks, interest rate, currencies or commodities to find their dynamic relationship using multivariate time series analysis.


