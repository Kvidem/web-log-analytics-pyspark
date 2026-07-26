# Web Log Analytics with PySpark (SQL + RDD)

Big data pipeline that parses raw, unstructured web server log files and turns them into structured, queryable datasets — then runs a series of analytical queries using both Spark SQL and Spark RDDs, with results visualized using Pandas/Matplotlib.

## What it does

- Loads raw web server log files (unstructured text) into a Spark session
- Uses regex extraction to parse each log line into structured fields: host/IP, timestamp, HTTP method, URL, HTTP version, status code, content size, and message
- Converts the parsed output into a Spark DataFrame and registers it as a temp SQL view for querying
- Runs a set of Spark SQL queries, including:
  - Error rate by HTTP status code
  - Top 10 IP addresses by traffic volume
  - Average/max/min content size per request
  - Top 10 most-requested URLs
  - Top 10 IPs by total content size served
  - Unique URL counts per status code
- Runs a parallel set of analyses using raw Spark RDD operations (map/filter/reduceByKey), including:
  - Most frequently repeated URLs and their occurrence percentage
  - Day with the highest number of requests
  - Unique IP/host address counts
  - Referrer extraction from log entries
  - Log message entropy and variability analysis
  - HTTP version distribution
  - Percentage of requests within a specific byte-size range
- Visualizes query/RDD outputs using Pandas and Matplotlib

## Tech stack

- **PySpark** (Spark SQL + Spark Core/RDD API)
- **Python** (Pandas, Matplotlib, regex)
- Developed and run in a Colab/Jupyter notebook environment

## Why this project

Log files are one of the most common examples of unstructured data engineers have to work with in production. This project covers the full path from raw text to structured, query-ready data to actual analytical insight — using two different Spark paradigms (SQL and RDD) to solve the same class of problem, which was a deliberate choice to demonstrate both approaches.

## Possible improvements

- Parameterize the regex parser to handle multiple log formats (Apache/Nginx/custom)
- Move from a single log file to a partitioned, incrementally-ingested data lake (e.g. S3 + Glue/Athena)
- Add automated data quality checks on the parsed fields before downstream analysis
- Replace notebook execution with a scheduled pipeline (e.g. Airflow DAG)

## How to run

1. Install dependencies: `pip install pyspark pandas matplotlib`
2. Open the notebook and update the log file path to point to your own data
3. Run all cells in order — the notebook builds the Spark session, parses the data, then runs the SQL and RDD analyses in sequence
