# otel-resources

![Version: 0.1.2](https://img.shields.io/badge/Version-0.1.2-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)

OpenTelemetry Collector resources

## Install

```sh
helm install otel-resources oci://ghcr.io/glueops/otel-resources-helm/otel-resources --version 0.1.2
```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| captain_domain | string | `""` |  |
| collector.cardinalityGuard.dropAttributeKeysRegex | string | `"(?i)^(.*[._-])?(user|session|request|trace|span|order|customer|cart|transaction|correlation|message)[._-]?id$|^(url\\.(full|path|query)|http\\.(url|target))$"` | data points with an attribute key matching this are dropped: per-entity IDs and raw URLs as labels |
| collector.cardinalityGuard.maxAttributeValueLength | int | `256` | attribute values are cut to this many characters |
| collector.cardinalityGuard.maxAttributes | int | `20` | data points with more attributes than this are dropped |
| collector.memoryLimitMiB | int | `512` | container memory limit of each collector pod (DaemonSet). memory_limiter and GOMEMLIMIT are derived from it. |
| collector.remoteWriteEndpoints | list | `["http://prometheus-glueops-core-kps-prometheus-0.prometheus-operated.glueops-core-monitoring.svc:9090/api/v1/write","http://prometheus-glueops-core-kps-prometheus-1.prometheus-operated.glueops-core-monitoring.svc:9090/api/v1/write"]` | Prometheus remote-write endpoints; every metric is written to each one. One per kube-prometheus-stack replica (pod DNS through the operator's headless prometheus-operated Service), so both replicas hold the full data. |
| collector.resources.requests.cpu | string | `"50m"` |  |
| collector.resources.requests.memory | string | `"256Mi"` |  |
| collector.spanmetrics.aggregationCardinalityLimit | int | `5000` | max unique span-metric dimension combinations tracked per service, in each collector pod; extra combinations go to an otel.metric.overflow="true" series. 0 disables the limit. |
| collector.spanmetrics.seriesExpiration | string | `"5m"` | a dimension combination with no spans for this long is dropped, which frees its slot under aggregationCardinalityLimit and stops it being re-exported. Active combinations never expire. 0 keeps them until the pod restarts. |
