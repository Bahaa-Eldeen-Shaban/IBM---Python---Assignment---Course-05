# IBM---Python---Assignment---Course-05

!pip install requests beautifulsoup4 pandas

!pip install yfinance

!pip install matplotlib

import yfinance as yf

*# Download Tesla stock data*

tesla_data = yf.download('TSLA', start='2023-01-01', end='2023-09-14')

*# Reset the index of the DataFrame*

tesla_data_reset = tesla_data.reset_index()

*# Save the DataFrame to a CSV file*

tesla_data_reset.to_csv('tesla_stock_data.csv', index=False)

*# Display the first five rows of the DataFrame*

print(tesla_data_reset.head())

# output
[*********************100%***********************]  1 of 1 completed        Date        Open        High         Low       Close   Adj Close  \
0 2023-01-03  118.470001  118.800003  104.639999  108.099998  108.099998   
1 2023-01-04  109.110001  114.589996  107.519997  113.639999  113.639999   
2 2023-01-05  110.510002  111.750000  107.160004  110.339996  110.339996   
3 2023-01-06  103.000000  114.389999  101.809998  113.059998  113.059998   
4 2023-01-09  118.959999  123.519997  117.110001  119.769997  119.769997   

      Volume  
0  231402800  
1  180389000  
2  157986300  
3  220911100  
4  190284000  

