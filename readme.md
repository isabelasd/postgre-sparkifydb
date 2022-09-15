# Data Modeling with Postgres - Project 1

This is the first project of the Nanodegree Data Engineer from Udacity. The goal here is to create a Postgres Database for a music app called Sparkify.
The purpose of this project is to create a star-schema database and ETL pipeline for this analysis. 

The previous datasets were stored as multiple JSON files contaning:
- metadata for songs
- log files on user activity

The query that should be optimized is for song play analysis.

## Schema Design for Song Play Analysis

The star-schema includes the following tables:

### Fact Table

1. **songplays** - records in log data associated with song plays i.e. records with page NextSong

songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

### Dimension Tables

2. **users** - users in the app
user_id, first_name, last_name, gender, level

3. **songs** - songs in music database
song_id, title, artist_id, year, duration

4. **artists** - artists in music database
artist_id, name, location, latitude, longitude

5. **time** - timestamps of records in songplays broken down into specific units
start_time, hour, day, week, month, year, weekday

## Information about the files

### **sql_queries.py**
  
The SQL queries are defined in sql_queries.py file (```DROP```, ```CREATE```, ```INSERT``` and ```SELECT```). 

### **create_tables.py**
After writing the queries, the create_tables.py generates the star-schema database as defined in sql_queries.py. 
To verify if the tables are created correctly, please use test.ipynb. 

### **test.ipynb**
Here you can validate if the tables are populated and are designed correctly.

### **etl.ipynb**
This is the Extract, Transform, Load (ETL) pipeline which opens the original dataset (JSON files) and insert them in the correct table. 

- data/song_data is used for songs and artists tables.
- datalog_data is used for time and users tables.

For filling the Fact Table (songplays table), a ```SELECT``` query was defined (in sql_queries.py) to find the song ID and artist ID based on the title, artist name, and duration of a song.

### **etl.py**
Same content of etl.ipynb, but in a separate python script. 

## How to run
On a terminal, first run create_tables.py to create the database. Afte that, please run etl.py to fill the database with the data.
To verify if the data is populated correctly, please go back to test.ipynb and run the first cells.
Also make sure to restart the kernel after running test.ipynb.

## Example queries for Song Play

- How many users paid users are there
```sql
SELECT count(level) FROM users WHERE level='paid';
```

- What is the average duration of songs?
```sql
SELECT AVG(duration) FROM songs;
```

- How many users are there in the database?
```sql
SELECT COUNT(user_id) FROM users;
```
