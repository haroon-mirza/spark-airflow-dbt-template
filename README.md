PySpark & Iceberg - Data Engineering Template
template for modern data engineering projects. Contained in docker. 

Core Technologies
This template comes pre-configured with the following industry-standard tools:

Containerization: Docker & Docker Compose

Compute Engine: Apache Spark

Storage Layer: Minio as a backup

Table Format: Apache Iceberg

Orchestration: Apache Airflow

Transformation: dbt

Interactive Development: JupyterLab

Data Visualization: Metabase

Set Up Your Project

Add your custom data extraction/transformation logic in Python scripts.

Place your interactive analysis code in the notebooks/ directory.

Develop your SQL-based transformations as dbt models inside airflow/dbt_project/models/.

How to Use This Template
This environment is split into two primary components that can be run independently: the interactive Spark environment and the automated Airflow/dbt environment.

1. Interactive Development (Spark & JupyterLab)
Use this mode for data exploration, prototyping pipelines, and interactive analysis.

Start the Services:
From the project's root directory, run:

docker compose up -d

Access JupyterLab:
Open your browser and navigate to http://localhost:8888. The notebooks/ folder in this repository is mapped as your workspace.

Stop the Services:

docker compose down

2. Automation & Transformation (Airflow & dbt)
Use this mode to schedule and run production-grade data pipelines and transformations.

Important: Ensure the Spark/Jupyter services are stopped first (docker compose down).

Start the Services:
Navigate to the airflow directory and use the provided Makefile shortcuts:

cd airflow
make restart

Access Airflow UI:
Open your browser and navigate to http://localhost:8080. Log in with the username airflow and password airflow.

Develop dbt Models:
The dbt project is located in airflow/dbt_project/. Develop your models following the best-practice structure:

models/staging/: For initial data cleaning and casting.

models/marts/core/: For foundational, company-wide data models.

models/marts/...: For business-specific data marts.

Stop the Services:
From within the airflow directory:

make down
