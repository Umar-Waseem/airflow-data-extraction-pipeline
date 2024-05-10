# Airflow Data Extraction Pipeline
This project automates a data extraction lifecycle from extracting data, transforming it, saving it to versioning the data with dvc and code with git.

## How To Run?
- Install the necessary libraries from `requirements.txt` file
- Run `pip install apache-airflow` to install airflow
- Run `export AIRFLOW_HOME="root of this cloned repo"`
- Run `airflow db init` to initialize airflow database
- Run `airflow scheduler` in a seperate terminal which tracks changes in dags
- Run `airflow webserver -p 8080` and open airflow user interface at `http://localhost:8080`
- Find the dag with the name specified in the code and toggle the pause button to activate the dag
- Click play button on top right to manually trigger the dag run.

## Points To Note
- Place all/any dags in the /dags folder for airflow to detect
- Run `airflow dags list` to check if airflow properly picks up dags from the dagbag (dag folder which contains all dags)
  
