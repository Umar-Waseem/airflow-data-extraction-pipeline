# Airflow Data Extraction Pipeline
This project automates a data extraction lifecycle from extracting data, transforming it, saving it while versioning the data with dvc and code with git.

## How To Run?
- Install the necessary libraries from `requirements.txt` file
- Run followiung to install airflow in python virtual environment
```
pip install apache-airflow
```

- Run following to set airflow environment variable
```
export AIRFLOW_HOME="root of this cloned repo"
```

- Run following to initialize airflow database
```
airflow db init
```

- Run following in a seperate console which tracks changes in dags
```
airflow scheduler
```

- Run follwing in a seperate console and open airflow user interface at `http://localhost:8080`
```
airflow webserver -p 8080
```

- Find the dag with the name specified in the code and toggle the pause button to activate the dag
- Click play button on top right to manually trigger the dag run.

## Dag Documentation

### Extract Task:
Extracts data from a list of URLs (urls) using the extract_data function. Each URL is processed sequentially, and the extracted data is combined.

### Preprocess Task:
Preprocesses the extracted data using the clean_data function. This task ensures that the text data is cleaned and formatted consistently.

### Save Task:
Saves the preprocessed data to a CSV file specified by filename. The data is saved in the format of 'id', 'title', 'description', and 'source' columns.

### DVC Push Task:
Adds the CSV file (data/extracted.csv) to the DVC repository using dvc add command and pushes the changes to the remote gdrive storage using dvc push.

### Git Push Task:
Performs Git operations to push the changes made to the Git repository. It includes commands to pull changes, add files, commit changes, and push to the remote repository.

## DAG Execution Order
The tasks are executed sequentially in the following order:

`extract_task >> preprocess_task >> save_task >> dvc_push_task >> git_push_task`

The DAG is configured to run manually (schedule=None) and does not have a specific schedule for automatic execution.

## Encountered Challenges
#### Challenge: Chnaging the airflow configuration to detect dags present in locations other than airflow folder
Solution: Make a dags directory in your current folder, places dags there and set envionment variable `export AIRFLOW_HOME="current folder"`

#### Challenge: How to automate git and dvc commands?
Solution: Use python os library

#### Challenge: Installing airflow in python virtual environment.
Solution: `pip install apache-airflow`

#### Challenge: Dataset not being saved using airflow
Solution: Use absolute path for dataset

## Points To Note
- Place all/any dags in the /dags folder for airflow to detect
- Run `airflow dags list` to check if airflow properly picks up dags from the dagbag (dag folder which contains all dags)
  
