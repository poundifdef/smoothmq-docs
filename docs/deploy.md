# Deploy

SmoothMQ deploys as a single binary. Here are configurations for common cases.

It is important that only 1 machine is provisioned. Everything else 
(volume size, server size) can be tweaked.

## Fly.io

Copy the following and run `fly launch`

``` toml title="fly.toml"
[build]

[env]
  Q_SQLITE_PATH = '/data/smoothmq.sqlite'

[[mounts]]
  source = 'smoothmq_data'
  destination = '/data'
  initial_size = '1gb'
  processes = ['app']

[http_service]
  internal_port = 3000
  force_https = true
  auto_stop_machines = 'stop'
  auto_start_machines = true
  min_machines_running = 0
  processes = ['app']

[[services]]
  protocol = 'tcp'
  internal_port = 3001

  [[services.ports]]
    port = 3001
    handlers = ['tls']

[[services]]
  protocol = 'tcp'
  internal_port = 2112

  [[services.ports]]
    port = 2112
    handlers = ['tls']

[[vm]]
  size = 'shared-cpu-1x'

[[metrics]]
  port = 2112
  path = '/metrics'
```

## Koyeb.com

Koyeb supports "one-click" deploys from git repositories. The following URL will
kick off a deployment:

```
https://app.koyeb.com/deploy?name=smoothmq&type=git&builder=dockerfile&repository=github.com/poundifdef/smoothmq&branch=main&ports=8080;http;/&env[Q_SERVER_USE_SINGLE_PORT]=true
```

## Railway.app

There is a Railway template to automatically deploy: https://railway.app/template/AJv-64

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