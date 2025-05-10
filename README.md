# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
### Date: 10/05/25


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.

### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
```
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the power consumption data from a CSV file
file_path = '/mnt/data/powerconsumption.csv'
data = pd.read_csv(file_path)

# Convert 'Datetime' to datetime format and set it as the index
data['Datetime'] = pd.to_datetime(data['Datetime'], format='%m/%d/%Y %H:%M')
data.set_index('Datetime', inplace=True)

# Use data for Zone 1 Power Consumption
data = data[['PowerConsumption_Zone1']]

# Display the shape and the first 20 rows of the dataset
print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

# Moving Average
# Perform rolling average transformation with a window size of 10
rolling_mean_10 = data['PowerConsumption_Zone1'].rolling(window=10).mean()

# Plot Moving Average
plt.figure(figsize=(12, 6))
plt.plot(data['PowerConsumption_Zone1'], label='Original Data', color='blue')
plt.plot(rolling_mean_10, label='Moving Average (window=10)', color='orange')
plt.title('Moving Average of Power Consumption')
plt.xlabel('Date')
plt.ylabel('Power Consumption (kWh)')
plt.legend()
plt.grid()
plt.show()

# Plot Transform Dataset
plt.figure(figsize=(12, 6))
plt.plot(data['PowerConsumption_Zone1'], label='Original Data', color='blue')
plt.title('Transform Dataset (Power Consumption)')
plt.xlabel('Date')
plt.ylabel('Power Consumption (kWh)')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
model = ExponentialSmoothing(data['PowerConsumption_Zone1'], trend='add', seasonal=None)
model_fit = model.fit()

# Make predictions for the next 30 periods
predictions = model_fit.predict(start=len(data), end=len(data) + 30)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
plt.plot(data['PowerConsumption_Zone1'], label='Original Data', color='blue')
plt.plot(predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions')
plt.xlabel('Date')
plt.ylabel('Power Consumption (kWh)')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
```
### OUTPUT:
![image](https://github.com/user-attachments/assets/9612225d-bd6c-46ac-8f78-8c9db93d353e)


## Moving Average:

![image](https://github.com/user-attachments/assets/8ca64207-219a-40f4-94fa-042bb85305c4)





## Plot Transform Dataset:

![image](https://github.com/user-attachments/assets/af8c1bb4-ca5e-4b25-86a0-c6ecaaea9c73)


## Exponential Smoothing

![image](https://github.com/user-attachments/assets/cecea8da-39cf-428b-960c-acb3aedf26c6)




### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
