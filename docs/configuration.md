# Configuration

SmoothMQ is highly configurable. Most configurations can be set via a command-line
flag and environment variable.

## Server

```
Usage: smoothmq server [flags]

Run queue server

Flags:
  -h, --help                                                    Show context-sensitive help.
      --config=CONFIG-FLAG                                      Configuration file
      --log-pretty                                              ($LOG_PRETTY)
      --log-level="info"                                        Log level ($LOG_LEVEL)

      --sqs-enabled                                             Enable SQS protocol for queue ($Q_SQS_ENABLED)
      --sqs-port=3001                                           HTTP port for SQS protocol ($Q_SQS_PORT)
      --sqs-keys=DEV_ACCESS_KEY_ID:DEV_SECRET_ACCESS_KEY,...    ($Q_SQS_KEYS)
      --sqs-parse-celery                                        Parse Celery messages. Lets you search by celery message ID and task type ($Q_SQS_PARSE_CELERY).
      --sqs-max-request-size=1048576                            Max size of SQS request in bytes ($Q_SQS_MAX_REQUEST_SIZE)
      --dashboard-enabled                                       Enable web dashboard ($Q_DASHBOARD_ENABLED)
      --dashboard-port=3000                                     HTTP port for dashboard ($Q_DASHBOARD_PORT)
      --dashboard-dev                                           Run dashboard in dev mode, refresh templates from local ($Q_DASHBOARD_DEV)
      --dashboard-user=""                                       Username for auth ($Q_DASHBOARD_USER)
      --dashboard-pass=""                                       Pass for auth ($Q_DASHBOARD_PASS)
      --sqlite-path="smoothmq.sqlite"                           Path of SQLite file ($Q_SQLITE_PATH)
      --metrics-prometheus-enabled                              ($Q_METRICS_PROMETHEUS_ENABLED)
      --metrics-prometheus-port=2112                            ($Q_METRICS_PROMETHEUS_PORT)
      --metrics-prometheus-path="/metrics"                      ($Q_METRICS_PROMETHEUS_PATH)
      --use-single-port                                         Enables having all HTTP services run on a single port with different endpoints ($Q_SERVER_USE_SINGLE_PORT)
      --port=8080                                               If use-single-port is enabled, this is the port number for the server ($PORT)
```