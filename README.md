# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 30-09-2025
### Name: K MADHAVA REDDY
### Register No: 212223240064

### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load the dataset
data = pd.read_csv('/content/avocado.csv', parse_dates=['Date'], index_col='Date')
data.sort_index(inplace=True)

# --- FIRST FIVE ROWS ---
print("FIRST FIVE ROWS:")
print(data.head())

# Aggregate data to create a single time series
# The original dataset has multiple entries for the same date for different regions.
# We will take the mean of 'AveragePrice' for each date.
data_agg = data.groupby('Date')['AveragePrice'].mean().reset_index()
data_agg.set_index('Date', inplace=True)

# Resample to weekly frequency to ensure a consistent time series
data_resampled = data_agg.resample('W').mean()

# Drop any NaN values that may have been introduced during resampling
data_resampled.dropna(inplace=True)

# Perform seasonal decomposition
# We use a period of 52 because the data is weekly, and we want to capture yearly seasonality.
decomposition = seasonal_decompose(data_resampled['AveragePrice'], model='additive', period=52)

# Plot the decomposition
plt.figure(figsize=(12, 12))

plt.subplot(411)
plt.plot(data_resampled['AveragePrice'], label='Avocado Average Price')
plt.legend(loc='upper left')
plt.title('Avocado Average Price')

plt.subplot(412)
plt.plot(decomposition.trend, label='Trend', color='orange')
plt.legend(loc='upper left')
plt.title('Trend Plot')

plt.subplot(413)
plt.plot(decomposition.seasonal, label='Seasonal', color='green')
plt.legend(loc='upper left')
plt.title('Seasonality Plot')

plt.subplot(414)
plt.plot(decomposition.resid, label='Residual', color='red')
plt.legend(loc='upper left')
plt.title('Residual Plot')

plt.tight_layout()
plt.show()
```
















### OUTPUT:
### FIRST FIVE ROWS:
<img width="623" height="421" alt="image" src="https://github.com/user-attachments/assets/498a56a4-191f-4ec6-8922-7e58d2148cf7" />


<img width="1326" height="321" alt="image" src="https://github.com/user-attachments/assets/d156cb72-98d4-4bf8-9a3e-e8b8c71c8451" />

<img width="1329" height="326" alt="image" src="https://github.com/user-attachments/assets/3f064ea4-27f4-441a-af82-60e21b0384f8" />
<img width="1320" height="650" alt="image" src="https://github.com/user-attachments/assets/7235875a-5a1c-465d-a0fd-65a8b807c19e" />


### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
