# AirLife ETL Pipeline - Starter Repository

Welcome to the AirLife ETL Pipeline workshop! This repository contains the skeleton code for building a simple Extract, Transform, Load (ETL) pipeline for aircraft and airport data.

## 🎯 Workshop Goals

By the end of this 3-hour workshop, you will have:
- Extracted airport data from a CSV file
- Fetched live flight data from the OpenSky Network API
- Cleaned and transformed the data using Python/pandas
- Loaded the data into a PostgreSQL database
- Verified your pipeline works end-to-end

## 📁 Repository Structure

```
ETL-AirLife/
├── README.md                   # This file
├── requirements.txt            # Python dependencies
├── main.py                     # Main pipeline orchestrator
├── database_setup.sql          # SQL script to create tables
├── data/
│   └── airports.csv           # Sample airport data (50 airports)
└── src/
    ├── extract_data.py        # Data extraction functions
    ├── transform_data.py      # Data cleaning and transformation
    └── load_data.py           # Database loading functions
```

## 🚀 Quick Start

### 1. Prerequisites

Make sure you have installed:
- Python 3.7 or higher
- PostgreSQL 12 or higher
- Git

### 2. Setup

1. **Fork this repository** to your GitHub account
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/ETL-AirLife.git
   cd ETL-AirLife
   ```

3. **Install Python dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

4. **Create PostgreSQL database**:
   ```bash
   # Connect to PostgreSQL
   psql -U your_username -d postgres
   
   # Create database
   CREATE DATABASE airlife_db;
   
   # Exit and reconnect to new database
   \q
   psql -U your_username -d airlife_db
   
   # Create tables
   \i database_setup.sql
   ```

### 3. Configure Database Connection

Edit the database configuration in `src/load_data.py`:

```python
DATABASE_CONFIG = {
    'username': 'your_username',      # Replace with your PostgreSQL username
    'password': 'your_password',      # Replace with your PostgreSQL password
    'host': 'localhost',
    'port': '5432',
    'database': 'airlife_db'
}
```

## 🛠️ Your Tasks

The repository contains skeleton code with TODO comments. Your job is to implement the missing functionality:

### Part 1: Data Extraction (`src/extract_data.py`)
- [ ] Implement `extract_airports()` to read CSV data
- [ ] Implement `extract_flights()` to fetch data from OpenSky Network API
- [ ] Handle errors gracefully (network issues, API limits)

### Part 2: Data Transformation (`src/transform_data.py`)
- [ ] Implement `clean_airports()` to remove invalid data
- [ ] Implement `clean_flights()` to standardize API data
- [ ] Convert units (altitude meters to feet)
- [ ] Handle missing values appropriately

### Part 3: Data Loading (`src/load_data.py`)
- [ ] Implement `load_to_database()` using pandas to_sql()
- [ ] Implement `verify_data()` to check data was loaded correctly
- [ ] Update database connection configuration

### Part 4: Integration (`main.py`)
- [ ] Uncomment the function calls once each component works
- [ ] Test the full pipeline end-to-end
- [ ] Add error handling for robustness

## 🧪 Testing Your Code

Each module can be tested independently:

```bash
# Test extraction
python src/extract_data.py

# Test transformation
python src/transform_data.py

# Test loading (after implementing database config)
python src/load_data.py

# Run full pipeline
python main.py
```

## 📊 Sample Data

The `data/airports.csv` file contains 50 airports including:
- Major European airports (CDG, LHR, FRA, etc.)
- Valid coordinates and IATA codes
- Some invalid data for testing your cleaning logic

The OpenSky Network API provides real-time flight data over Europe with:
- Aircraft identifiers and callsigns
- Current positions (latitude, longitude, altitude)
- Ground speed and heading information

## ⚠️ Common Issues

**API Rate Limits**: The OpenSky Network has rate limits. If you get errors:
- Wait a few seconds between requests
- Test with smaller geographic areas first
- Use the `test_api_connection()` function to debug

**Database Connection**: If you can't connect to PostgreSQL:
- Check that PostgreSQL service is running
- Verify your username/password
- Make sure the `airlife_db` database exists
- Ensure tables are created with `database_setup.sql`

**Import Errors**: Make sure you're in the project root directory when running scripts

## 🎯 Success Criteria

Your ETL pipeline is working when:
1. ✅ `python main.py` runs without errors
2. ✅ Airport data is loaded into the `airports` table
3. ✅ Flight data (if API accessible) is loaded into the `flights` table
4. ✅ You can run SQL queries on your loaded data
5. ✅ Your code handles errors gracefully

## 🔍 Example Queries

Once your data is loaded, try these queries:

```sql
-- Count total airports
SELECT COUNT(*) FROM airports;

-- Show airports by country
SELECT country, COUNT(*) as airport_count 
FROM airports 
GROUP BY country 
ORDER BY airport_count DESC;

-- Show current flights (if any)
SELECT callsign, origin_country, altitude 
FROM flights 
WHERE altitude > 10000 
LIMIT 5;
```

## 📚 Resources

- [OpenSky Network API Documentation](https://opensky-network.org/apidoc/)
- [Pandas Documentation](https://pandas.pydata.org/docs/)
- [SQLAlchemy to_sql() Guide](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_sql.html)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)

## 🤝 Getting Help

If you're stuck:
1. Read the TODO comments carefully - they contain hints
2. Test each module individually before running the full pipeline
3. Use the test functions provided (like `test_api_connection()`)
4. Check the error messages - they usually point to the problem
5. Ask your instructor or classmates

## 🏆 Next Steps

After completing this workshop, you'll be ready for the larger AirLife project where you'll design your own startup's complete data pipeline with more advanced features like:
- Multiple data sources
- Complex transformations
- Production-ready error handling
- Data quality monitoring
- Automated scheduling

Good luck building your first ETL pipeline! 🚀


# AirLife ETL Pipeline

## What This Does
This pipeline extracts airport data from a CSV file and live flight data from an API, 
cleans the data, and loads it into a PostgreSQL database.

## How to Run It
1. Install dependencies: `pip install -r requirements.txt`
2. Set up PostgreSQL database
3. Update database connection in `src/load_data.py`
4. Run: `python main.py`

## What We Built
- **Extract:** Gets airport data from CSV and flight data from OpenSky Network API
- **Transform:** Cleans invalid coordinates and converts units
- **Load:** Puts clean data into PostgreSQL tables

## Team Members
- Octave Claich
- Alexandre Tonon
- Audrey Maurette
- Alexandre Maignan