# Introduction to SQL

Below are my notes for the [Intro to SQL](https://www.kaggle.com/learn/intro-to-sql) course.

## Using Google BigQuery

BigQuery is a data warehouse that lets you work with huge datasets. You can query the data using the SQL programming language.

To import BigQuery in Python, use:

```
from google.cloud import bigquery
```

The first step in the workflow is to then create a Client object. This object is a central part of the whole process.

```
client = bigquery.Client()
```

To connect to a specific dataset you must create a reference to the dataset and then use an API request to fetch it.

```
dataset_ref = client.dataset("hacker_news", project="bigquery-public-data")

dataset = client.get_dataset(dataset_ref)
```

You can list all of the tables within a dataset with `list_tables(dataset)`. Retrieving a table is similar to retrieving a dataset.

```
table_ref = dataset_ref.table("full")

table = client.get_table(table_ref)
```

Alternatively, you can just run a query:

```
result = client.query(sql_query).to_dataframe()
```

This returns a Pandas dataframe.

### Limiting Data Usage On BigQuery

There are many reasons why you might need to limit the amount of data returned from queries:
 - Memory or storage constraints
 - Cost
 - Time constraints
 - Third-party platform limits

You can estimate the size of a query by performing a dry run.

```
dry_run_config = bigquery.QueryJobConfig(dry_run=True)

dry_run_query_job = client.query(query, job_config=dry_run_config)
```

`dry_run_query_job.total_bytes_processed` will be an estimate in bytes.

You can also limit the maximum number of bytes for a query by setting the `maximum_bytes_billed` parameter within `QueryJobConfig`. For example:

```
ONE_MB = 1000 * 1000
safe_config = bigquery.QueryJobConfig(maximum_bytes_billed=ONE_MB)

safe_query_job = client.query(query, job_config=safe_config)

result = safe_query_job.to_dataframe()
```

## Basic Query

A basic SQL query is made up of three parts:

```
SELECT [columns]
FROM [table]
WHERE [filter]
```

SELECT and FROM are mandatory clauses whereas WHERE is not required (although it is almost always used).