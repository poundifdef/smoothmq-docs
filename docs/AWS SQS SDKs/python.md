# Python

## Boto

``` py
import boto3

sqs = boto3.client("sqs", endpoint_url="http://localhost:3001")
```
## Celery

``` py
from celery import Celery

app = Celery(
    "tasks",
    broker_url="sqs://DEV_ACCESS_KEY_ID:DEV_SECRET_ACCESS_KEY@localhost:3001",
)
```