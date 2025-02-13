# Spotify End-to-End Data Engineering Project Using Snowflake  

### 📌 Project Overview  

This project builds an efficient ETL (Extract, Transform, Load) pipeline using AWS and Snowflake to collect, process, and analyze music data from Spotify. Using the Spotipy library, we extract details about the **Top 50 Global Songs** in JSON format. The data is then cleaned, transformed, and loaded into Snowflake's Data Warehouse using **Snowpipe** for real-time ingestion. This end-to-end pipeline provides valuable insights into global music trends, empowering organizations to make data-driven decisions.  

### ⚙️ Architecture Overview  
![spotify-etl-using-snowflake-architecture-diagram](https://github.com/user-attachments/assets/6795d614-1c52-4384-b6d4-6dbde19e48fe)

The ETL pipeline is designed as follows:  
1. **Data Extraction**: A scheduled **AWS Lambda** function uses Spotipy to fetch data from Spotify's Top 50 Global playlist.  
2. **Raw Data Storage**: The extracted JSON data is saved in an **AWS S3** bucket.  
3. **Data Transformation**: Another Lambda function processes the raw data to make it analysis-ready, storing the transformed data in a separate S3 bucket.  
4. **Data Loading with Snowpipe**: **Snowpipe** automatically detects new data in the S3 bucket and loads it into Snowflake's Data Warehouse.  
5. **Data Analysis**: Once in **Snowflake**, the data can be queried to uncover insights about global music consumption trends.  

### 📊 About the Data  

This project leverages data from the **Spotify API** using the **Spotipy** library. Specifically, it extracts the **Top 50 Global Songs** in JSON format, providing rich information about each track, including:  
- Artist details  
- Album information  
- Popularity metrics  
- Audio features (e.g., danceability, energy, valence)  

This dataset allows for in-depth analysis of global music trends and listener behavior.  

### 🛠️ Services Used  

- **AWS S3**: For scalable and secure object storage of raw and transformed data.  
- **AWS Lambda**: A serverless computing service to run ETL code triggered by events.  
- **AWS CloudWatch**: Monitors the ETL pipeline, tracking logs and metrics, and sending alerts.  
- **Snowflake**: A cloud-based data warehousing platform for efficient data storage and analysis.  
- **Snowpipe**: Automates the loading of transformed data from S3 into Snowflake tables in real time.  

### 📦 Installed Packages  

To run this ETL pipeline, the following Python packages are required:  
```
pip install spotipy
pip install pandas
```
### Project Execution Flow

Lambda Trigger (every week) -> Run spotify_api_data_extract code (Extract Data from Spotify Top 50 - Global Playlist using spotipy library) -> Stores Raw Data in AWS S3 -> Trigger Transform Function -> Run spotify_transformation_load_function code (Transforms the data) -> Stores Transformed Data in AWS S3 (Which then sends event notification to snowpipe) -> Triggers the Snowpipe which then extracts the data from transformation buckets and loads them in respective tables in Snowflake -> Data stored in Snowflake can be queried for Analysis.
