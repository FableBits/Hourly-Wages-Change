# OECD Hourly Wages Analysis

An SQL-based analysis of hourly wage changes across European countries using OECD data from 2000 to 2024.

## Overview

This project analyzes real hourly wage trends in European countries by combining OECD data on:
- Annual average wages (adjusted for inflation using PPP)
- Hours worked per year

The analysis calculates hourly wages and tracks percentage changes across different time periods, providing insights into wage growth patterns and country rankings.

## Key Features

- **Data Processing**: Cleans and standardizes OECD wage and hours data
- **Hourly Wage Calculation**: Derives hourly wages from annual wages and hours worked
- **Trend Analysis**: Tracks wage changes across multiple time periods (2000-2024, 2007-2024, etc.)
- **Country Rankings**: Provides percentile rankings and ranking changes over time
- **European Focus**: Filters data to include only European countries

## Data Sources

The analysis uses OECD data tables:

### Primary Data
- **Annual Average Wages**: [OECD.Stat - Average annual wages](https://stats.oecd.org/index.aspx?DataSetCode=AV_AN_WAGE)
  - Source table: `oecd_annual_average_wages`
  - Includes wages adjusted for inflation using PPP (Purchasing Power Parity)
  
- **Hours Worked**: [OECD.Stat - Hours worked](https://stats.oecd.org/index.aspx?DataSetCode=ANHRS)
  - Source table: `oecd_hours_worked` 
  - Annual hours worked per employee by country
  - **Note**: Data filtered to include only dependent workers (employees)

### Reference Data
- `the_countries`: Reference table for European country classification
  - Used to filter analysis to European countries only

### Data Collection
To reproduce this analysis:
1. Download the CSV files from the OECD links above
2. Import them into your MySQL/MariaDB database
3. Run the `wages_2.sql` script

## Key Time Periods Analyzed

- **2000-2024**: Long-term wage growth
- **2007-2024**: Post-financial crisis period
- **2008-2024**: Financial crisis impact
- **2010-2024**: Post-recession recovery
- **2014-2024**: Recent decade

## Database Schema

### Main Tables Created

1. **`oecd_hours`**: Cleaned hours worked data
   - `country_code`, `country`, `year`, `hours_worked`, `hours`

2. **`oecd_wages`**: Cleaned wage data (constant prices, USD PPP)
   - `country_code`, `country`, `unit_measure`, `price_base`, `avg_wage`, `year`, `avg_wage_int`

3. **`oecd_hourly_wage`**: Combined hourly wage calculations
   - `country`, `year`, `avg_wage`, `hours`, `hourly_wage`

4. **`oecd_hw_change`**: Wage changes across time periods
   - Historical hourly wages for key years
   - Percentage changes between periods

5. **`oecd_hw_change_with_pr`**: Rankings and percentile analysis
   - Percentile rankings for different years
   - Ranking changes over time

## Usage

1. **Prerequisites**: MySQL/MariaDB database with OECD source tables
2. **Data Setup**: Download CSV files from the OECD links above and import into your database
3. **Execution**: Run the SQL script `wages_2.sql` in your database
4. **Output**: Creates analysis tables for further querying and visualization

**Note**: Raw data files (CSV) are not included in this repository to keep it lightweight and ensure users get the most current data from OECD sources.

## Key Data Transformations

- **Currency Standardization**: Converts all wages to USD PPP (constant prices)
- **Data Cleaning**: Handles decimal formatting and country name standardization
- **European Filter**: Excludes non-European countries (except Turkey and OECD totals)
- **Missing Data Handling**: Uses different scaling for countries with limited PPP data (Bulgaria, Romania, Croatia)

## Results

The analysis provides:
- Hourly wage trends for European countries
- Percentage changes in real wages across different periods
- Country rankings and ranking mobility over time
- Insights into economic performance and wage growth patterns

## Author

Created by FableBits

## License

This project is open source and available under the MIT License.
