# AWS CLI

Make sure you have the `AWS_ACCESS_KEY` and `AWS_SECRET_ACCESS_KEY` env vars
set.

From there, add the `--endpoint-url` to any CLI command. For example, 
to list queues, run:

```
$ aws sqs list-queues --endpoint-url http://localhost:3001
```