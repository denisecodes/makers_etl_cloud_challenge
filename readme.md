<h1 align="center">
    ETL process for Netflix 🎬
</h1>

<p align="center">
This project aims to use the Extract, Transform, Load (ETL) process with Netflix data hosted on AWS in the Cloud. It was completed as part of the Makers Academy Bootcamp during Week 4 of the Data Engineering stream. The goal is to make the data more accessible and useful, ready to be used by a wider audience, both technical and non-technical.
</p>

## 🏡 The scenario

I was tasked with find the most visited URL per country per day during a week of your choice (e.g. 2018-04-01 until 2018-04-08).

## 📊 Expected output

### Requirements
* A detailed diagram of the entire system. This should show how the cloud (AWS) and your local machine (Python, Jupyter Notebook, Postgres) communicate and connect to each other.

### Optional
* Code snippets.
* Screenshots of outputs from AWS or your local machine.

## 🚀 Tech Stack 

 <img src="https://img.shields.io/badge/Amazon_AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=white"><img src="https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54"> <img src="https://img.shields.io/badge/Made%20with-Jupyter-orange?style=for-the-badge&logo=Jupyter"><img src="https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white">

 ## 👷‍♀️ Infrastructure

 ### Cloud
 * A Database hosted in the Cloud using AWS Glue.
 * A folder to store query results in an S3 bucket.
 * An S3 bucket containing the Netflix dataset.
 * A crawler via AWS Glue to set up the table, linked to the S3 bucket containing the Netflix dataset.

### Local Machine
* A Jupyter Notebook using AWS SDK to connect to the database in the Cloud using valid AWS credentials,
* A local PostgreSQL database with a table ready to load the data.

 ## 🖼️ Diagram

 The following is a diagram I created using [Excalidraw](https://excalidraw.com/) to demonstrate the infrastructure I created on the Cloud and the set up I had on my Local Machine that allowed me to Extract, Transform and Load Data from the Cloud to my machine. 

 ![A diagram showing how the ETL process was implemented. It shows a detailed diagram of how the Cloud and my local machine interacts.](./diagrams/etl_process_with_aws_diagram.png)

## 🔄 ETL Process

You can find the code and full ETL process in my [Jupyter Notebook](./etl_cloud_db_challenge.ipynb).

### Understand the Data
While attempting to complete this challenge, I made a plan on how to use Athena to understand the data before doing extraction, transformation, loading (ETL). You can find my plan in the following:
1. Understand the data using Athena i.e. what the column names mean, what kind of values and data types.
2. Choose which columns would be useful - i.e. `country_code`, `url_visited`, `date`.
3. Test queries out step by step with the following to try out:
    * `COUNT(date)` to count how many url per country per day.
    * Filter the dates: `BETWEEN 2018-04-01 AND 2018-04-08`.
    * Use `GROUP BY on country_code, date`.
    * Do some research to find out how we could get the url that is most visited on the url column.
4. Repeat testing until the query performs as expected and gives the output I am looking for.

This plan really helped me to test, refine and optimise the SQL query to be used for extraction and in the Jupyer notebook. In the notebook, you can find my step by step process to changing the SQL query and the outputs returned from Athena. 

### Extract the data

Once I have found the SQL query I needed to extract the data, I created a variable called `sql_query` to stored the query to be used for extraction. Then, I set up AWS SDK in my Jupyter Notebook using Python and Boto3 library,

I created an Athena Client using Boto3 in order to interact with the Database and the S3 bucket folder to store the query results. To validate that I have access to the database and S3 bucket, I used my AWS credentials to validate my identity. 

After the Athena Client was set up, I initiated the SQL query and stored the results to be used for transforming and loading the data.

### Transform and Load the Data

Before transforming and loading the data, I created a table in my local PostgreSQL database to store the data. 

Then I went through each row of the extracted data and ensured none of the columns contained empty values before inserting it into the table I created. 

### Check the data has been loaded

Lastly, I used the sql magic to check that the data has been loaded to my table successfully.


<!-- ## ✅ Benefits of ETL
*  -->

<!-- ## 💻 Running the notebook -->


