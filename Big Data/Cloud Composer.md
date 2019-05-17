# Google Cloud Composer

* Based on Apache Airflow
* It is a manged Apache Airflow service
* Create, schedule, monitor and manage workflows

## Documentation
* https://airflow.apache.org/
* https://airflow.apache.org/start.html
* https://cloud.google.com/composer/docs/

## What is Apache Airflow
* Open source
* programmatically author, schedule and montior workflows
* Based on python
* Setup non trivial (without using Cloud Composer)


## Composer / Airflow
Support of built-in services thise services are supported by **operators**.
* BigQuery
* GCS
* Pub/Sub
* Dataflow

Composer provides Operators to communicated with those services.

## DAG 
* Directed Acyclic Graph, which means nothing else then we should not have cycles in our workflows. 

## Compose Environment
* Each environment has its own Cloud Storage

Environments can be created via:
* Google Cloud SDK
* Google Cloud Platform Console
* Google Cloud Composer APIs

## Example
A typical workflow also called DAG would look like
* Look for new HDFS files
* Copy the data to Cloud Storage
* Looking for new data load them into bigquery
* Transform the data
* Extract information
* Notify slack

## Write a Workflow / Airflow DAG
A workflow is pythong file with 5 main sections

### Import
import dependencies needed for the workflow.
```
import datetime
from airflow import DAG
from airflow import models
```

### Arguments
construct default arguments argruments. 
```
default_dag_args= {
    'retries':1
}

# other global variables which we want to use in our DAG
bg_dataset_name : 'datasetname'
output_file: 'gs://test/folder'
```
### Setup
Setup our DAG by giving it a name, setup a interval and give it our arguments
```
dag = DAG(
    'name',
    scheduler_interval = datetime.timedelta(days =1)
    default_args = default_dag_args
)
```

* schedule interval cannot be set in the default args
### Tasks
Tasks is the job itself which should run in the DAG.
Multiple tasks are possible. For example

1. Run a BigQuer query that eports the results to a new dataset
2. Export the new dataset to Cloud Storage

```
# perform a biquery operation
bigquery_operator.BigQueryOperator(
    task:id = 'big_query_query'
)

#export the query results
bigquery_to_gcs.BigQueryToCloudStorageOperator(
    task:id = 'export_to_gcs'
)
```

detailed description can be found here https://cloud.google.com/composer/docs/how-to/using/writing-dags#pythonoperator

### Ordering
define in which order the Tasks are executed. We want to run the query first before we save the results to gcs.
```
big_query_query >> export_to_gcs
```

## Security
* IAM support
* To access the airflow special permissions are required

## How to deploy a DAG
Each composer environment has a dedicated Google Cloud Storage DOG folder. The deployment is very simple we just upload the DAG to this DAGs folder. 

We simply uplado the DAG File which is a .py file. After uploading it, it takaes a few minutes until Airflow picks up the DAG.

After that the DAG should be listed in the Airflow UI.

## Web UI
Google provies a link to the Airflow Web UI.

## PYPI
Packages can be installed via the composer UI.
Add packages and version directly in the Composer UI.

## cloud scheduler vs cloud composer


## Notes from the web
Now let's say your CSV file is overwritten at 01:00 UTC every day, and you want to run the same Dataflow job to process it every time when its overwritten. If you don't want to manually run the job exactly at 01:00 UTC regardless of weekends and holidays, you need a thing to periodically run the job for you (in our example, at 01:00 UTC every day). Cloud Composer can help you in this case. You can provide a config to Cloud Composer, which includes what jobs to run (operators), when to run (specify a job start time) and run in what frequency (can be daily, weekly or even yearly).

It seems cool already, however, what if the CSV file is overwritten not at 01:00 UTC, but anytime in a day, how will you choose the daily running time? Cloud Composer provides sensors, which can monitor a condition (in this case, the CSV file modification time). Cloud Composer can guarantee that it kicks off a job only if the condition is satisfied.

Google Cloud Composer is a big step up from Cloud Dataflow. Cloud Composer is a cross platform orchestration tool that supports AWS, Azure and GCP (and more) with management, scheduling and processing abilities.

Cloud Dataflow handles tasks. Cloud Composer manages entire processes coordinating tasks that may involve BigQuery, Dataflow, Dataproc, Storage, on-premises, etc.