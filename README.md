
# US-Accidents-Exploratory-Data-Analysis

US Accidents EDA using Python, Pandas and python visualization libraries





## Steps to follow

- I am using the US Accidents Data from Kaggle for this EDA project https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents
- Read the data using pandas
- Remove the columns that has morethan 50% of missign values
- Check how many Numeric and Categorical fields we have
- Use matplotlib and seaborn for visualization
- Use folium for visualize the latitude and longitude data on map



## Download Data

To download the data in csv use this code

```
import opendatasets as od
url = 'https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents'
od.download(url)
```

## Data Preparation and Cleaning
- Load the file using Pandas
- Look at some information about the data and the fields
- Fix missing and incorrect values

```python
import pandas as pd

data_filename = './us-accidents/US_Accidents_Dec21_updated.csv'
df = pd.read_csv(data_filename)

# to describe the data use the below command
df.describe()
```

### Find all numeric columns in the dataframe
```
numerics = ['int16', 'int32', 'int64', 'float16', 'float32', 'float64']
numeric_df = df.select_dtypes(include=numerics)

print("There are " + str(len(numeric_df.columns)) + " numeric columns")
```

### Percentage of missing values per column
```
missing_perc = round(df.isna().sum().sort_values(ascending=False)/len(df)*100, 2)
missing_perc = missing_perc[missing_perc!=0]
missing_perc
```
```
output:

Number                   61.29
Precipitation(in)        19.31
Wind_Chill(F)            16.51
Wind_Speed(mph)           5.55
Wind_Direction            2.59
Humidity(%)               2.57
Weather_Condition         2.48
Visibility(mi)            2.48
Temperature(F)            2.43
Pressure(in)              2.08
Weather_Timestamp         1.78
Airport_Code              0.34
Timezone                  0.13
Nautical_Twilight         0.10
Civil_Twilight            0.10
Sunrise_Sunset            0.10
Astronomical_Twilight     0.10
Zipcode                   0.05
dtype: float64
```

#### Visualize the percentage of missing value columns
```
missing_perc.plot(kind='barh')
```
![App Screenshot](https://drive.google.com/file/d/115vjtsaQEi_qPXAEMxentBcknQM7vCB0)


## Select columns for analysis and visualization
There are 45 columns are there to this data, so selecting only  columns to analyze for now. We can select other columns and try the analysis with same steps
- City
- Start Time
- Start Lat, Start Lng
- Temperature
- Weather Condition

## Summary and Conclusion
### Insights:
- Less than 5% of cities have more than 1000 yearly accidents.
- Over 1100 cities have reported only one accident
