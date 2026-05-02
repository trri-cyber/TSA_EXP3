# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 02-05-2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load CSV
file_path = "C:/Users/admin/OneDrive/Desktop/index_1.csv"

data = pd.read_csv("/content/global_inflation_post_covid.csv")

data.columns = data.columns.str.strip().str.lower().str.replace(" ", "_")

data = data[data['country'] == 'USA']

data['date'] = pd.to_datetime(data['date'])

data = data.groupby('date')['food_price_index'].mean().reset_index()

data.set_index('date', inplace=True)

# Use 'money' column
data = data['food_price_index'].values

# Number of lags
lags = range(35)

autocorr_values = []

# Mean and variance
mean_data = np.mean(data)
variance_data = np.var(data)
N = len(data)

# Calculate autocorrelation
for lag in lags:
    
    if lag == 0:
        autocorr_values.append(1)
        
    else:
        auto_cov = np.sum(
            (data[:-lag] - mean_data) *
            (data[lag:] - mean_data)
        ) / N
        
        autocorr = auto_cov / variance_data
        
        autocorr_values.append(autocorr)

# Plot graph
plt.figure(figsize=(10,6))

plt.stem(lags, autocorr_values)

plt.axhline(y=0, color='red', linestyle='--')

plt.title('Inflation of food pricing index post covid')

plt.xlabel('Lag')

plt.ylabel('Autocorrelation')

plt.grid(True)

plt.show()
```

### OUTPUT:
<img width="1065" height="668" alt="image" src="https://github.com/user-attachments/assets/344c28d0-b4fb-4abe-a756-c53f99b0a1cf" />

### RESULT:
        Thus we have successfully implemented the auto correlation function in python.
