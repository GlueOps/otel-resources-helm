# otel-resources

![Version: 0.2.0](https://img.shields.io/badge/Version-0.2.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)

OpenTelemetry Collector resources

## Install

```sh
helm install otel-resources oci://ghcr.io/glueops/otel-resources-helm/otel-resources --version 0.2.0
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| captain_domain | string | `""` |  |
| collector.memoryLimitMiB | int | `512` | container memory limit of each collector pod (DaemonSet). memory_limiter and GOMEMLIMIT are derived from it. |
| collector.resources.requests.cpu | string | `"50m"` |  |
| collector.resources.requests.memory | string | `"256Mi"` |  |
| collector.spanmetrics.aggregationCardinalityLimit | int | `1000` | max unique span-metric dimension combinations tracked per service, in each collector pod; extra combinations go to an otel.metric.overflow="true" series. 0 disables the limit. |
