# Desctiption

The chart consists of

- nginx deployment
- nginx prometheus exporter
- service for nginx
- service monitor
- hpa (optional)
- prometheus rules (optional)

By default a simple nginx reverse proxy config is implemented. But you can override config setting `.Values.config` variable.

# Values example

```yaml
name: nginx-proxy
replicas: 3
packageVersion: 1 # change it to trigger config redeploy

hpa:
  enabled: true
  resource: cpu
  averageUtilization: 30
  minReplicas: 5
  maxReplicas: 15
resources:
  requests:
    memory: "128Mi"
    cpu: "150m"
  limits:
    memory: "256Mi"
    cpu: "250m"

proxy:
  protocol: https
  workerProcesses: auto

prometheusRules: 
  enabled: true
```

---
Tags: helm, chart, nginx, reverse proxy, kubernetes, k8s
