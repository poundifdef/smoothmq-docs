# Python

## Boto3

``` py
import boto3

sqs = boto3.client("sqs", endpoint_url="http://localhost:3001")
```
## Celery

SmoothMQ has special support for Celery.

!!! note
    The endpoint_url must be `/`. You cannot run the SQS endpoint
    on a different path (such as `localhost:3001/sqs`).

``` py
from celery import Celery

app = Celery(
    "tasks",
    broker_url="sqs://DEV_ACCESS_KEY_ID:DEV_SECRET_ACCESS_KEY@localhost:3001",
)
```

### Schedule Tasks 

To schedule a task in the future, add the `DelaySeconds` parameter:

``` py
@app.task
def hello():
    print('hello world')

# Schedules the task for 1 hour from now
hello.apply_async(DelaySeconds=3600)
```

### Monitor Specific Tasks

If SmoothMQ detects a Celery task, it will extract the
Celery task ID and task type as metadata. This means you can search for a specific ID or
task type.

!!! note
    Celery transmits the message as base64-encoded JSON

[![Celery task in SmoothMQ](celery.png)](celery.png)