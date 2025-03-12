## **Data Preparation (Python using pandas)**

Before working with the data in Tableau,  a series of preprocessing steps was performed with Python.

### **1. Data Importing**

```python
import kagglehub
from kagglehub import KaggleDatasetAdapter
import pandas as pd

bikes = kagglehub.load_dataset(
    KaggleDatasetAdapter.PANDAS,
    "hmavrodiev/london-bike-sharing-dataset",
    "london_merged.csv"
)

```

This code snippet imports the necessary libraries and loads the dataset directly from Kaggle using the `kagglehub` library. A pandas DataFrame called `bikes` is created, containing the data from the "london_merged.csv" file.
### **2. Data Exploration**

Exploring the dataset's structure and contents.

```python
bikes.info()
bikes.shape
bikes.head()
```

The `info()` method provided information about the column names, data types, and missing values. shape showed the number of rows and columns. `head()` displayed the first few rows to give an overview of the data.

### **3. Descriptive Statistics and Value Counts**

Examined the distribution of categorical data using value counts:

```python
# count the unique values in the weather_code column
bikes.weather_code.value_counts()

# count the unique values in the season column
bikes.season.value_counts()

```

This code helped to understand the prevalence of each weather condition and the distribution of rides across seasons.

### **4. Data Cleaning and Transformation**

Cleaned and transformed the data to prepare it for analysis:

```python
# specifying the column names to use
new_cols_dict = {
    'timestamp':'time',
    'cnt':'count',
    't1':'temp_real_C',
    't2':'temp_feels_like_C',
    'hum':'humidity_percent',
    'wind_speed':'wind_speed_kph',
    'weather_code':'weather',
    'is_holiday':'is_holiday',
    'is_weekend':'is_weekend',
    'season':'season'
}

# renaming the columns to the specified column names
bikes.rename(new_cols_dict, axis=1, inplace=True)

# changing the humidity values to percentage (i.e. a value between 0 and 1)
bikes.humidity_percent = bikes.humidity_percent / 100

# creating a season dictionary so that we can map the integers 0-3 to the actual written values
season_dict = {
    '0.0':'spring',
    '1.0':'summer',
    '2.0':'autumn',
    '3.0':'winter'
}

# creating a weather dictionary so that we can map the integers to the actual written values
weather_dict = {
    '1.0':'Clear',
    '2.0':'Scattered clouds',
    '3.0':'Broken clouds',
    '4.0':'Cloudy',
    '7.0':'Rain',
    '10.0':'Rain with thunderstorm',
    '26.0':'Snowfall'
}

# changing the seasons column data type to string
bikes.season = bikes.season.astype('str')
# mapping the values 0-3 to the actual written seasons
bikes.season = bikes.season.map(season_dict)

# changing the weather column data type to string
bikes.weather = bikes.weather.astype('str')
# mapping the values to the actual written weathers
bikes.weather = bikes.weather.map(weather_dict)

```

- The columns were renamed for better clarity.
- Humidity percentage converted from its original representation to decimal for easier calculation.
- Used the mapping to convert integer values into more meaningful values for weather condition.

### **5. Saving Data for Tableau Visualization**

```python
# writing the final dataframe to an excel file that is used for Tableau visualisations.
bikes.to_excel('london_bikes_final.xlsx', sheet_name='Data')

```

Finally, the transformed dataset was saved as an Excel file, ready for visualization in Tableau.
