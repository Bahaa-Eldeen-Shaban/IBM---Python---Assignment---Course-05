# IBM---Python---Assignment---Course-05

!pip install requests beautifulsoup4 pandas

!pip install yfinance

!pip install matplotlib


# Question 1: Use yfinance to Extract Stock Data
*Reset the index, save, and display the first five rows of the tesla_data dataframe using the head function.
import yfinance as yf*

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

# Question 2: Use Webscraping to Extract Tesla Revenue Data
*Display the last five rows of the tesla_revenue dataframe using the tail function.*

import requests
from bs4 import BeautifulSoup
import pandas as pd

*# URL of Tesla's financials page*
url = 'https://companiesmarketcap.com/tesla/revenue/'

*# Send an HTTP request to the URL*
response = requests.get(url)

*# Parse the HTML content of the page*
soup = BeautifulSoup(response.content, 'html.parser')

*# Find the data table (Adjust the selector as needed based on page structure)*
tables = soup.find_all('table')

*# Assuming the relevant table is the first one; adjust index if necessary*
data_table = tables[0]  # or another index if the relevant table is different

*# Convert the table to a DataFrame*
df = pd.read_html(str(data_table))[0]

*# Rename the DataFrame for clarity*
tesla_revenue = df

*# Display the last five rows of the DataFrame*
print(tesla_revenue.tail())

# The Output
    Year  Revenue   Change
11  2013  $2.01 B  387.23%
12  2012  $0.41 B  102.34%
13  2011  $0.20 B   74.95%
14  2010  $0.11 B    4.29%
15  2009  $0.11 B      NaN
<ipython-input-11-b3fe67aa651d>:21: FutureWarning: Passing literal html to 'read_html' is deprecated and will be removed in a future version. To read from a literal string, wrap it in a 'StringIO' object.
  df = pd.read_html(str(data_table))[0]

  
# Question 3: Use yfinance to Extract Stock Data
*Reset the index, save, and display the first five rows of the gme_data dataframe using the head function.*

import yfinance as yf

*# Download historical data for GameStop (GME)*
gme_data = yf.download('GME', start='2023-01-01', end='2023-12-31')

*# Reset the index*
gme_data_reset = gme_data.reset_index()

*# Save the DataFrame to a CSV file*
gme_data_reset.to_csv('gme_data.csv', index=False)

*# Display the first five rows of the DataFrame*
print(gme_data_reset.head())

![Question 3_ Use yfinance to Extract Stock Data](https://github.com/user-attachments/assets/05a9378f-b3f7-4d8f-ba17-b22a40d7b785)


# Question 4: Use Webscraping to Extract GME Revenue Data
*Display the last five rows of the gme_revenue dataframe using the tail function.*

import requests
from bs4 import BeautifulSoup
import pandas as pd

*# URL of GME revenue data (adjust the URL if necessary)*
url = 'https://companiesmarketcap.com/gamestop/revenue/'

*# Send an HTTP request to the URL*
response = requests.get(url)

*# Check if the request was successful*
if response.status_code == 200:
    # Parse the HTML content of the page
    
    soup = BeautifulSoup(response.content, 'html.parser')

    # Find the table with revenue data (adjust the class name as necessary)
    
    table = soup.find('table', {'class': 'table'})  # Adjust class name based on actual page structure

    # Convert the table to a DataFrame
    
    df = pd.read_html(str(table))[0]

    # Rename the DataFrame for clarity
    
    gme_revenue = df

    # Display the last five rows of the DataFrame
    
    print(gme_revenue.tail())
else:
    print(f"Failed to retrieve data. Status code: {response.status_code}")

![Question 4_ Use Webscraping to Extract GME Revenue Data](https://github.com/user-attachments/assets/d388b959-513a-42e1-b1dd-efc21500e74c)


#Question 5: Plot Tesla Stock Graph
*Use the make_graph function to graph the Tesla Stock Data, also provide a title for the graph.*

import yfinance as yf
import matplotlib.pyplot as plt

*# Download historical data for Tesla (TSLA)*
tesla_data = yf.download('TSLA', start='2023-01-01', end='2023-12-31')

*# Define a function to plot the stock data*
def make_graph(data):

    plt.figure(figsize=(10, 6))
    
    plt.plot(data.index, data['Close'], label='Closing Price', color='blue')

    plt.title('Tesla (TSLA) Stock Price')
    
    plt.xlabel('Date')
    
    plt.ylabel('Closing Price (USD)')
    
    plt.legend()
    
    plt.grid(True)
    
    plt.show()

*# Plot the Tesla stock data*

make_graph(tesla_data)

![Question 5_ Plot Tesla Stock Graph](https://github.com/user-attachments/assets/be1fccb3-e304-43e6-9344-3345c3234cee)


# Question 6: Plot GameStop Stock Graph
*Use the make_graph function to graph the GameStop Stock Data, also provide a title for the graph.*

import yfinance as yf
import matplotlib.pyplot as plt

*# Download historical data for GameStop (GME)*
gme_data = yf.download('GME', start='2023-01-01', end='2023-12-31')

*# Define a function to plot the stock data*
def make_graph(data):

    plt.figure(figsize=(10, 6))
    plt.plot(data.index, data['Close'], label='Closing Price', color='red')
    plt.title('GameStop (GME) Stock Price')
    plt.xlabel('Date')
    plt.ylabel('Closing Price (USD)')   
    plt.legend()    
    plt.grid(True)
    plt.show()

*# Plot the GameStop stock data*

make_graph(gme_data)

![Question 6_ Plot GameStop Stock Graph](https://github.com/user-attachments/assets/d76d3914-9f1d-4b1c-a32a-b81386463479)

