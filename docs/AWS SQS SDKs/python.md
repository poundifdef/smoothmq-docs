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