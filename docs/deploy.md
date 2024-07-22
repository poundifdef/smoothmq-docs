# Deploy

SmoothMQ deploys as a single binary. Here are configurations for common cases.

## Fly.io

Copy the following fly.toml and run `fly launch`

``` toml
# This is a default configuration to launch on fly.io. It does the following:
#
# 1. Provisions a single machine as the message queue. 
# 2. Creates a 1 GB volume to store data (such as queue messages)
# 3. Exposes the following endpoints:
#       Dashboard: https://your-app.fly.dev/
#       SQS Endpoint: https://your-app.fly.dev/sqs
#       Prometheus metrics: https://your-app.fly.dev/metrics
#
# It is important that only 1 machine is provisioned. Everything else 
# (volume size, server size) can be tweaked.

[build]

[env]
  PORT = '8080'
  Q_SERVER_USE_SINGLE_PORT = 'true'
  Q_SQLITE_PATH = '/data/smoothmq.sqlite'

[[mounts]]
  source = 'smoothmq_data'
  destination = '/data'
  initial_size = '1gb'
  processes = ['app']

[http_service]
  internal_port = 8080
  force_https = true
  auto_stop_machines = true
  auto_start_machines = true
  min_machines_running = 0
  processes = ['app']

[[vm]]
  size = 'shared-cpu-1x'

[[metrics]]
  port = 8080
  path = '/metrics'
```

## Render.com

Here is a `render.yaml` blueprint:

``` yaml
services:
  - type: web
    runtime: docker
    name: smoothmq
    repo: https://github.com/poundifdef/smoothmq.git
    healthCheckPath: /
    envVars:
      - key: PORT
        value: 8080
      - key: Q_SERVER_USE_SINGLE_PORT
        value: true
      - key: Q_SQLITE_PATH
        value: '/data/smoothmq.sqlite'
    disk:
      name: smoothmq-data
      mountPath: /data
      sizeGB: 1
```