# Desctiption

The chart consists of

- secrets
- a cron job with secrets injected as env

All parameters can be specified in a single cron job. Root parameters are used as defaults.

# Values example

```yaml
schedule: "*/5 * * * *" # Once in 5 minutes
successfulJobsHistoryLimit: 0
failedJobsHistoryLimit: 0
concurrencyPolicy: Forbid
activeDeadlineSeconds: 160
container_name: example-name
container_image: some-image
secretsVersion: "1.0.0" # update this number to trigger secrets redeploy

cronjobs:
  job1-name:
    activeDeadlineSeconds: 100
    env:
      - name: "S3__ServiceUrl"
        value: "https://s3.domain.net"
    secrets:
      - key: "S3__AccessKey"
        value: "#{S3__AccessKey}"
      - key: "S3__SecretAccessKey"
        value: "#{S3__SecretAccessKey}"
  job2-name:
    overrided_container_image: another-image
    env:
      - name: "S3__ServiceUrl"
        value: "https://myawesomesite.blob.core.windows.net"
    secrets:
      - key: "S3__ConnectionString"
        value: "#{S3__ConnectionString}"
```
