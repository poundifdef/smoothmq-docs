# Python

## Boto3

``` py
import boto3

sqs = boto3.client("sqs", endpoint_url="http://localhost:3001")
```
## Celery

One note about Celery: the endpoint_url must be `/`. You cannot run the SQS endpoint
on a different path (such as `localhost:3001/sqs`).

``` py
from celery import Celery

app = Celery(
    "tasks",
    broker_url="sqs://DEV_ACCESS_KEY_ID:DEV_SECRET_ACCESS_KEY@localhost:3001",
)
```

SmoothMQ has special support for Celery. If it detects a Celery task, it will extract the
Celery task ID and task type as metadata. This means you can search for a specific ID or
task type.

[![Celery task in SmoothMQ](celery.png)](celery.png)