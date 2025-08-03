# **Movie Analytics Pipeline: A Scalable Data Engineering Case Study**

This project is a case study for a startup focused on personalized movie recommendations and data-driven analysis of factors contributing to movie success. The objective is to build a robust data pipeline that performs Extract, Transform, and Load (ETL) on raw movie datasets and provides actionable insights for business decision-making.

Business Questions Answered
	•	What is the highest-rated movie of all time?
	•	Which genres are most popular among users?
	•	Do release times (month/quarter) influence box office earnings?
	•	Which genres generate the highest inflation-adjusted revenues?

Datasets Used

	1.	Movies Metadata – From Kaggle MovieLens Dataset (26M ratings, 270K users, 45K movies).
	2.	CPI Data – From St. Louis FRED, used to normalize revenue across time.

⸻

<img width="593" height="331" alt="architecture" src="https://github.com/user-attachments/assets/2be23ac1-e590-4f10-be8d-b5f9ca097df3" />

⸻

Technical Architecture

Ingestion

	•	Kaggle API + wget for CPI
	•	Python scripts executed on an AWS EC2 instance
	•	Files transferred to AWS S3 using AWS CLI

Transformation

	•	Spark jobs on a scalable cluster
	•	CPI normalization logic and revenue calculations
	•	Movie/genre insights aggregated at different time resolutions

Orchestration

	•	Apache Airflow DAGs manage ingestion, transformation, and loading steps
	•	Modular DAGs designed for future scheduling

Storage

	•	Transformed data is loaded into Amazon Redshift for querying
	•	Star/snowflake schemas for efficient BI consumption

Visualization (Optional)

	•	Power BI dashboards to visualize KPIs like top genres, quarterly trends, and inflation-adjusted revenue

⸻

Technologies Used

	•	Cloud & Infrastructure: AWS (S3, EC2, Redshift, Glue)
	•	Processing & Orchestration: Apache Spark, Apache Airflow
	•	Transformation: DBT, Pandas
	•	Orchestration Enhancements: Shell scripting, cron scheduling (option for Airflow scheduling)
	•	Containers & Deployment: Docker
	•	Visualization: Power BI (optional)

⸻

Data Modeling Approach

	•	Data is normalized for efficient updates and deletion
	•	Fact and dimension tables created for:
	•	Movies
	•	Genres
	•	Ratings
	•	CPI (Consumer Price Index)

⸻
 
<img width="868" height="700" alt="data_model" src="https://github.com/user-attachments/assets/534ca281-8ac3-46e8-b175-9c78a78b0a76" />

⸻

ETL Workflow Summary

	1.	Trigger ingestion scripts from EC2 using Airflow
	2.	Download raw datasets using APIs (Kaggle + FRED)
	3.	Upload raw files to AWS S3
	4.	Spark jobs process raw files into transformed tables
	5.	Load final data into Amazon Redshift
	6.	Run data quality checks (e.g., non-null IDs, row counts > 0)

⸻

Scalability & Improvements

	•	High Volume? Scale Spark cluster and partition input
	•	Frequent Runs? Schedule DAGs in Airflow (daily/weekly)
	•	Increased Query Load? Use sort keys and pre-aggregated tables in Redshift
	•	Pipeline Reliability? Implement CeleryExecutor and SLA alerts in Airflow
	•	Dockerization? Ensures environment consistency across machines

⸻

Conclusion

This project demonstrates how modern data engineering tools can be used to build scalable, maintainable, and insightful analytics pipelines for media startups. It addresses both current business questions and is flexible enough to scale with increased data volume and usage.
