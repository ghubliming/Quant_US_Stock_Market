Powered by ChatGPT and Claude.

# Stock_trading.ipynb

# README for Stock Trading Simulation with Forex Conversion

## Overview
This Python script simulates stock purchases at different intervals (hourly, daily, weekly, and monthly) over a specified time period. It converts EUR to USD using real-time Forex data and calculates the average cost of stock purchases. The results are visualized, and purchase details can be exported to CSV files.

## Key Features
1. **Stock and Forex Data Retrieval**: Uses `yfinance` to retrieve historical stock and Forex data.
2. **EUR to USD Conversion**: Converts EUR to USD using Forex data at specific timestamps.
3. **Simulated Purchases**: Simulates stock purchases at hourly, daily, weekly, and monthly intervals.
4. **Average Cost Calculation**: Computes the average cost per share for each purchase frequency.
5. **Data Visualization**: Plots the stock price and calculated average costs.
6. **CSV Export**: Option to export purchase details to CSV files.
7. **Total Shares Calculation**: Calculates the total number of shares purchased for each frequency.

## Requirements
- Python 3.x
- `yfinance` (`pip install yfinance`)
- `pandas` (`pip install pandas`)
- `matplotlib` (`pip install matplotlib`)

## How It Works

1. **Stock and Forex Data Retrieval**:
   The `get_data()` function retrieves historical stock or Forex data between a specified start and end date using `yfinance`. It ensures that the timestamps are in UTC for consistency.

2. **EUR to USD Conversion**:
   The `convert_eur_to_usd()` function takes the EUR amount, a timestamp, and Forex data, and returns the equivalent USD amount based on the exchange rate at the given timestamp.

3. **Simulated Purchases**:
   - The `calculate_average_cost()` function simulates hourly, daily, weekly, and monthly stock purchases.
   - For each purchase, it calculates the number of shares based on the amount to be invested and the stock price at that moment.
   - It includes a flag mechanism that checks whether stock data is available for a given timestamp. If data for the current day or time is missing (e.g., on a holiday or non-trading day), the flag triggers a search for the next available data point, ensuring that the simulation continues smoothly without breaking.
   - The hardcoding of market hours (9 AM to 4 PM) is aimed at aligning with typical New York Stock Exchange (NYSE) trading times to fetch accurate timestamps from the `yfinance` package, which may otherwise return unexpected values outside of trading hours.


4. **Average Cost Calculation**:
   After simulating purchases, the script calculates the average cost for each type of purchase using the `calculate_avg()` function.

5. **Plotting the Results**:
   The `plot_results()` function visualizes the stock prices along with the average costs for each purchase frequency.

6. **CSV Export**:
   The `export_purchases_to_csv()` function allows exporting purchase details (timestamp, shares, and price) for each frequency (hourly, daily, weekly, monthly) to CSV files. Set `export_flag = 1` to enable export.

7. **Total Shares Calculation**:
   The script calculates the total number of shares purchased for each frequency and prints them.

## Usage

### Main Execution
To run the script, specify:
- The stock ticker (e.g., `"NVDA"`).
- The Forex ticker (e.g., `"EURUSD=X"`).
- The start and end dates for the data retrieval.
- The amount of EUR to be spent (total capital for the year).

Example:
```python
ticker = "NVDA"  # Stock ticker
forex_ticker = "EURUSD=X"  # Forex ticker for EUR to USD conversion
start_date = "2023-01-08"
end_date = "2023-12-31"
time_length = 365  # Total time period in days
spend_eur = time_length * 100  # Total EUR to spend over the year
```

After the purchases are calculated, the script outputs:
- Average costs for hourly, daily, weekly, and monthly purchases.
- Total shares purchased for each frequency.
- Plots showing the stock price and the average cost lines.
- CSV files with purchase details (if enabled).

### Exporting Data to CSV
The script can export the purchase data to CSV files. To enable export, set the `export_flag` to `1`:
```python
export_purchases_to_csv(
    hourly_purchases, 
    daily_purchases, 
    weekly_purchases, 
    monthly_purchases, 
    "path/to/output/directory", 
    1  # Set to 1 to enable export
)
```

### Example Output
```
Average Costs:
Hourly: $XXX.XX
Daily: $XXX.XX
Weekly: $XXX.XX
Monthly: $XXX.XX

Total shares purchased (Hourly): XXX.XX
Total shares purchased (Daily): XXX.XX
Total shares purchased (Weekly): XXX.XX
Total shares purchased (Monthly): XXX.XX
```

## Dependencies
- `yfinance`: For retrieving stock and Forex data.
- `pandas`: For handling data frames and timestamps.
- `matplotlib`: For plotting stock prices and average costs.


## License
This project is open-source. Feel free to use and modify it for personal or commercial purposes.



# Rating

### 1. **Functionality: 6/10**

   **Strengths**: 
   - The code successfully retrieves data, converts currencies, and calculates average stock costs. It supports multiple scenarios (hourly, daily, weekly, and monthly purchases) and adapts dynamically when market data for the current day is unavailable by fetching data from the next available day.
   
   **Areas for Improvement**: 
   - The current setup could be made more flexible to accommodate different purchase schedules or stock market conditions. For instance, while the code correctly handles missing data by looking for the next available timestamp, allowing more dynamic customization of purchase days and times (e.g., user-defined trading windows) would be beneficial.
   - Expanding the flexibility for different markets or custom market hours could further enhance the usability, especially for global markets or partial holidays.

   
   ### 2. **Code Structure: 5/10**
   - **Strengths**: 
     - Functions are somewhat modular, making it easier to follow.
   
   - **Areas for Improvement**: 
     - Relying on **global variables** (`hourly_purchases`, etc.) is bad practice, as it makes the code harder to maintain and debug. It’s better to encapsulate everything in functions and return those values rather than using global state.
     - The `calculate_average_cost()` function is doing too much, and breaking it into smaller functions would make it easier to test, maintain, and understand.
     - The code is not structured in a way that allows easy extension. Adding new functionality, such as additional types of purchases or customization of trading hours, would require significant refactoring.
   
   ### 3. **Error Handling: 4/10**
   - **Strengths**: 
     - There's an implicit assumption that the data retrieved from `yfinance` is always correct.
   
   - **Areas for Improvement**: 
     - No handling of potential issues like missing data, incomplete data for a given date range, or invalid tickers. If `yfinance` fails to fetch data, the program will break.
     - Currency conversion assumes the Forex data is always available at the required timestamps, which might not always be the case. More robust error-checking is needed for cases where the data does not align perfectly.
   
   ### 4. **Efficiency: 5/10**
   - **Strengths**: 
     - Some use of Pandas for date handling is efficient.
   
   - **Areas for Improvement**:
     - The code does many individual operations in loops (e.g., converting timezones and looping through dates one by one). This could be made more efficient by vectorizing these operations using Pandas instead of looping.
     - Checking for each hour's timestamp within the main loop could be expensive with large datasets. This could be optimized by filtering or preprocessing the timestamps in bulk.
   
   ### 5. **Documentation: 3/10**
   - **Strengths**: 
     - Function names are relatively descriptive, which helps a bit.
   
   - **Areas for Improvement**: 
     - The code lacks meaningful comments explaining what each section does or why certain decisions were made. Someone unfamiliar with the code might struggle to follow the logic.
     - More detail in the docstrings for each function (describing input parameters, expected outputs, and potential edge cases) would make it easier for others to understand and maintain.
     - There’s no high-level explanation of how the different components fit together, which makes it harder to grasp the overall purpose at a glance.
   
   ### 6. **Readability: 5/10**
   - **Strengths**: 
     - Variable names are clear for the most part, so the code can be read without too much confusion.
   
   - **Areas for Improvement**: 
     - Long, dense functions like `calculate_average_cost()` are difficult to read and understand. Breaking them up would help.
     - Code could benefit from more consistent formatting, such as better use of whitespace and logical grouping of operations.
     - The reliance on global variables makes it harder to trace where data is coming from and where it’s being used.
   
   ---
   
   ### Revised Overall Rating: **4.7/10**
   
   While the code works for its intended purpose, it lacks flexibility, efficiency, and error-handling. It could also be made much more readable and maintainable with a clearer structure and more documentation. With refactoring, improved efficiency, and better error-handling, this project could significantly improve.
   
   This rating is based on the assumption that you're aiming for higher standards like production-level code or something that could be shared publicly or used at scale. For a personal project or a quick solution, it's still a solid effort!
