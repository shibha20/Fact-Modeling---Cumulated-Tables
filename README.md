# Fact-Modeling---Cumulated-Tables

User Activity Cumulative Tracking and Bitwise Encoding
This SQL script manages and compresses user activity data over time by storing cumulative active dates and generating compact bitwise representations of daily activity.
Overview
1. Managing Cumulative User Activity (users_cumulated Table)
Table Creation:
The table users_cumulated stores:
user_id (TEXT): Identifier of the user.
dates_active (DATE[]): An array of all dates on which the user was active.
date (DATE): Snapshot date representing the state of cumulative activity.
The primary key is (user_id, date).
Data Aggregation and Insertion:
Extracts user activity from the events table for a specific date (2023-01-01 in the example).
Joins with the previous snapshot (2022-12-31) to combine existing active dates with today's new activity.
Inserts updated records reflecting cumulative active dates.
2. Generating Bitwise Representations of User Activity
Date Series Generation:
Generates a series of dates for a month (2023-01-01 to 2023-01-31).
Bitwise Encoding Logic:
For each user and each day in the series:
Checks if the user was active on that day (dates_active array contains the date).
If active, calculates a 32-bit integer with one bit set, where the bit position encodes how far the active day is from the user's reference date.
If not active, sets the value to zero.
Converts this number to a 32-bit binary string.
Aggregation:
Sums the 32-bit integers per user, resulting in a compressed integer that encodes multiple days of activity in a single value.
This approach facilitates efficient storage and compression of activity data.
Usage Notes
Modify the snapshot dates (2022-12-31, 2023-01-01) and series dates as required for different periods.
The events table is expected to contain user_id and event_time columns.
Bitwise encoding assumes activity data fits within 32 days from the reference date.
Dropping the users_cumulated table before running the script ensures a clean start.

<img width="753" height="422" alt="Screenshot 2025-08-11 at 12 31 01 PM" src="https://github.com/user-attachments/assets/4141cbe0-842c-439a-92a9-529665a17c7d" />


<img width="407" height="381" alt="Screenshot 2025-08-11 at 12 30 30 PM" src="https://github.com/user-attachments/assets/a653bde0-51b3-409f-a049-ffbd564c61ee" />



