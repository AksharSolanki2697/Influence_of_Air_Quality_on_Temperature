# Influence-of-Air-Quality-on-Temperature
## Motivation 
Air pollution refers to the release of pollutants into the air that are
detrimental to human health and the planet as a whole. It has been proven through
studies that air pollution directly affects the temperature of a location. Energy production
and transportation are one of the major causes of air pollution. The burning of fossil
fuels leads to release of various harmful and hazardous chemicals into the atmosphere.
These chemicals along with pressure, wind, altitude and oceanic movement affect the
temperature of a specific location. The main aim of this project is to analyze the relation between
temperature and concentration of some of these pollutants in the
atmosphere. Moreover, this project also emphasizes on the importance of Feature Creation in Data Mining.

## Objective
The main objective of this project is to analyze whether concentration of
pollutants in the atmosphere has an effect on the temperature

## Data Collection
Source - https://archive.ics.uci.edu/ml/datasets/Beijing+Multi-Site+Air-Quality+Data#

The data attributes are as follows :
1. No - Row Number
2. Year - year of measurement
3. Month - month of measurement
4. Day - day of measurement
5. Hour - hour of measurement
6. PM2.5 - concentration of PM2.5 (μg/m3)
7. PM10 - concentration of PM10 (μg/m3)
8. SO2 - concentration of SO2 (μg/m3)
9. NO2 - concentration NO2 (μg/m3)
10.CO - concentration of CO (μg/m3)
11.O3 - concentration of O3 (μg/m3)
12.TEMP - temperature (degree Celsius)
13.PRES - pressure (hPa)
14.DEWP - dew point temperature (degree Celsius)
15.RAIN - precipitation (mm)
16.Wd - wind direction
17.WSPM - wind speed (m/s)
18.Station - name of the city/air-quality monitoring site

Size of the Dataset:
1. Number of attributes (columns) = 18
2. Number of data samples (rows) / region = 35064
3. Number of Regions: 12
Total Instances = 18 * 35064 * 12 = 7,573,824

## Data Preprocessing
### Appending Data
The data was given in form of 12 excel files. We used pandas to
merge these 12 files into one dataframe and gave column names wherever necessary.
### Null Data
These types of data are not tolerable for applying any kind of machine
learning models. Analysis of a dataset which contains such data will result in prediction
with high error and very less accuracy. Hence, null data entities are found out and are
replaced by the mean value of the respective attribute values. By doing so, the entire
data set will remain balanced.
### Wind Direction Attribute
To process and analyze data, we require the data to be a
numeric value and not a string. Hence, the Wind Direction (N, S, E, W, etc.) attributes
are converted to 360 degree value format.
### Measurement Unit Conversion
All the pollutants were given in microgram/m^3.
However, every pollutant has a different concentration range at which they affect the
atmospheric temperature and human life. To calculate the AQI for individual pollutants,
SO2, NO2, and O3 were converted to parts per billion(ppb) while CO was converted to
parts per million(ppm).

### Concentration to Air Quality Index Calculation

The Air Quality Index was created for the 6 pollutants using the below given formula : 

Air Quality Index(P) = ((I(hi) - I(lo)) / BP(hi) - BP(lo))* (C(P) - BP(lo)) + I(lo)

where,

I(P) = The index for pollutant P

I(hi) = The AQI value corresponding to BP(hi)

I(lo) = The AQI value corresponding to BP(lo)

BP(hi) = The breakpoint greater than or equal to C(P)

BP(lo) = The breakpoint lower than or equal to C(P)

C(P) = The Concentration of pollutant P

AQI | 0-50 | 50-100 | 100-150 | 150-200 | 200-300 | 300-500
--- | ---- | ------ | ------- | ------- | ------- | -------
Air Pollution Level | Good | Moderate | Unhealthy for sensitive individuals | Unhealthy | Very Unhealthy | Hazardous

Converting all the pollutants to their respective AQI made sure that scaling was not
required since all the pollutants were in the same range.


## Analysis of Results

I have used R^2 score to evaluate the models.  R^2 Score is the proportion of the variance in the dependent variable that is predictable from the independent variable

There are 3 models created in order to depict the importance of feature creation and influence of air quality on temperature. 

Feature1 : Uses Pressure, Rain, and Wind speed in order to predict the temperature.

Feature2 : Uses the 4 Pollutant concentration and 2 particle sizes concentration along with the previous 3 features to predict temperature.

Feature3 : Uses the created features (Air quality indices of 6 pollutants) along with the previous 3 features to predict the temperature.

The influence of Air Quality on temperature can be judged by comparing the models with Feature1. The other two models show a better R^2 score which means that the models
with the air quality features fit better. 

The importance of feature creation can be judged by comparing the Feature2 and Feature3. Feature3 uses the created Air Quality Index values while,
Feature2 uses the concentration of the pollutants. Except for decision tree, all the other three models show a better R^2 Score thus proving the effectiveness
of feature creation.



Model | R^2 Score for Feature1 | R^2 Score for Feature2 | R^2 Score for Feature3
----- | ---------------------- | ---------------------- | ---------------------- |
DecisionTree Regression | 0.7226228398476233 | 0.7255236235567473 | 0.7254002902689967
Ridge Regression | 0.668813412604142 | 0.7502428511220475 | 0.7507785142635952
Lasso Regression | 0.6632206984150215 | 0.7437820410345286 | 0.7502508124379266
ElastiNet Regression | 0.6660343309393048 | 0.7439282443449935 | 0.7504926807317898
