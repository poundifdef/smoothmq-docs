# Deploy

SmoothMQ deploys as a single binary. Here are configurations for common cases.

It is important that only 1 machine is provisioned. Everything else 
(volume size, server size) can be tweaked.

## Fly.io

Copy the following and run `fly launch`

``` toml title="fly.toml"
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

Here is a Render blueprint:

``` yaml title="render.yaml"
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