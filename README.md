README for Stock Trading Simulation with Forex Conversion
Overview
This Python script simulates stock purchases at different intervals (hourly, daily, weekly, and monthly) over a specified time period. It converts EUR to USD using real-time Forex data and calculates the average cost of stock purchases. The results are visualized, and purchase details can be exported to CSV files.

Key Features
Stock and Forex Data Retrieval: Uses yfinance to retrieve historical stock and Forex data.
EUR to USD Conversion: Converts EUR to USD using Forex data at specific timestamps.
Simulated Purchases: Simulates stock purchases at hourly, daily, weekly, and monthly intervals.
Average Cost Calculation: Computes the average cost per share for each purchase frequency.
Data Visualization: Plots the stock price and calculated average costs.
CSV Export: Option to export purchase details to CSV files.
Total Shares Calculation: Calculates the total number of shares purchased for each frequency.
Requirements
Python 3.x
yfinance (pip install yfinance)
pandas (pip install pandas)
matplotlib (pip install matplotlib)
How It Works
Stock and Forex Data Retrieval: The get_data() function retrieves historical stock or Forex data between a specified start and end date using yfinance. It ensures that the timestamps are in UTC for consistency.

EUR to USD Conversion: The convert_eur_to_usd() function takes the EUR amount, a timestamp, and Forex data, and returns the equivalent USD amount based on the exchange rate at the given timestamp.

Simulated Purchases:

The calculate_average_cost() function simulates hourly, daily, weekly, and monthly stock purchases.
For each purchase, it calculates the number of shares based on the amount to be invested and the stock price at that moment.
It supports time ranges and assumptions such as the market being open from 9 AM to 4 PM (New York Time).
Average Cost Calculation: After simulating purchases, the script calculates the average cost for each type of purchase using the calculate_avg() function.

Plotting the Results: The plot_results() function visualizes the stock prices along with the average costs for each purchase frequency.

CSV Export: The export_purchases_to_csv() function allows exporting purchase details (timestamp, shares, and price) for each frequency (hourly, daily, weekly, monthly) to CSV files. Set export_flag = 1 to enable export.

Total Shares Calculation: The script calculates the total number of shares purchased for each frequency and prints them.

Usage
Main Execution
To run the script, specify:

The stock ticker (e.g., "NVDA").
The Forex ticker (e.g., "EURUSD=X").
The start and end dates for the data retrieval.
The amount of EUR to be spent (total capital for the year).
Example:

python
Copy code
ticker = "NVDA"  # Stock ticker
forex_ticker = "EURUSD=X"  # Forex ticker for EUR to USD conversion
start_date = "2023-01-08"
end_date = "2023-12-31"
time_length = 365  # Total time period in days
spend_eur = time_length * 100  # Total EUR to spend over the year
After the purchases are calculated, the script outputs:

Average costs for hourly, daily, weekly, and monthly purchases.
Total shares purchased for each frequency.
Plots showing the stock price and the average cost lines.
CSV files with purchase details (if enabled).
Exporting Data to CSV
The script can export the purchase data to CSV files. To enable export, set the export_flag to 1:

python
Copy code
export_purchases_to_csv(
    hourly_purchases, 
    daily_purchases, 
    weekly_purchases, 
    monthly_purchases, 
    "path/to/output/directory", 
    1  # Set to 1 to enable export
)
Example Output
yaml
Copy code
Average Costs:
Hourly: $XXX.XX
Daily: $XXX.XX
Weekly: $XXX.XX
Monthly: $XXX.XX

Total shares purchased (Hourly): XXX.XX
Total shares purchased (Daily): XXX.XX
Total shares purchased (Weekly): XXX.XX
Total shares purchased (Monthly): XXX.XX
Dependencies
yfinance: For retrieving stock and Forex data.
pandas: For handling data frames and timestamps.
matplotlib: For plotting stock prices and average costs.
License
This project is open-source. Feel free to use and modify it for personal or commercial purposes.
