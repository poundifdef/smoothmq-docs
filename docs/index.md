# Getting Started

## Install

Download SmoothMQ from GitHub 

``` bash
$ git clone https://github.com/poundifdef/smoothmq.git
```

## Run

To run the server, run:

``` bash
$ go run . server
```

This will run the SmoothMQ server. The default SQS credentials are
`DEV_ACCESS_KEY_ID` / `DEV_SECRET_ACCESS_KEY`

### Dashboard
The dashboard is available at http://localhost:3000

### SQS
The SQS API endpoint is http://localhost:3001

You can connect to it using any SQS-compatible library. Here's an example for how to connect
using Python:

``` py
import boto3

sqs = boto3.client("sqs", endpoint_url="http://localhost:3001")
```

### Metrics

Prometheus metrics are available at http://localhost:2112/metrics