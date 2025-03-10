# Prometheus Operator

[Prometheus Operator](https://github.com/coreos/prometheus-operator/) provides easy monitoring definitions for Kubernetes services and deployment and management of Prometheus instances.

## TL;DR;

```bash
$ helm repo add bitnami https://charts.bitnami.com/bitnami
$ helm install bitnami/prometheus-operator
```

## Introduction

This chart bootstraps [Prometheus Operator](https://github.com/bitnami/bitnami-docker-prometheus-operator) on [Kubernetes](http://kubernetes.io) using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters.

## Prerequisites

- Kubernetes 1.12+
- Helm 2.11+ or Helm 3.0-beta3+

## Installing the Chart

Add the `bitnami` charts repo to Helm:

```bash
$ helm repo add bitnami https://charts.bitnami.com/bitnami
```

To install the chart with the release name `my-release`:

```bash
$ helm install --name my-release bitnami/prometheus-operator
```

The command deploys Prometheus Operator on the Kubernetes cluster in the default configuration. The [configuration](#configuration) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` release:

```bash
$ helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release. Use the flag `--purge` to delete all history too.

## Parameters

The following table lists the configurable parameters of the Prometheus Operator chart and their default values.

### Global Parameters

|         Parameter         |                                                  Description                                                   |                         Default                         |
|---------------------------|----------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| `global.imageRegistry`    | Global Docker image registry                                                                                   | `nil`                                                   |
| `global.imagePullSecrets` | Global Docker registry secret names as an array                                                                | `[]` (does not add image pull secrets to deployed pods) |
| `global.storageClass`     | Global storage class for dynamic provisioning                                                                  | `nil`                                                   |
| `global.labels`           | Additional labels to apply to all resource                                                                     | `{}`                                                    |
| `nameOverride`            | String to partially override `prometheus-operator.name` template with a string (will prepend the release name) | `nil`                                                   |
| `fullnameOverride`        | String to fully override `prometheus-operator.fullname` template with a string                                 | `nil`                                                   |
| `rbac.create`             | Wether to create & use RBAC resources or not                                                                   | `true`                                                  |
| `rbac.apiVersion`         | Version of the RBAC API                                                                                        | `v1beta1`                                               |
| `rbac.pspEnabled`         | PodSecurityPolicy                                                                                              | `true`                                                  |

### Prometheus Operator Parameters

|                       Parameter                       |                                     Description                                      |                               Default                                |
|-------------------------------------------------------|--------------------------------------------------------------------------------------|----------------------------------------------------------------------|
| `operator.enabled`                                    | Deploy Prometheus Operator to the cluster                                            | `true`                                                               |
| `operator.image.registry`                             | Prometheus Operator image registry                                                   | `docker.io`                                                          |
| `operator.image.repository`                           | Prometheus Operator Image name                                                       | `bitnami/prometheus-operator`                                        |
| `operator.image.tag`                                  | Prometheus Operator Image tag                                                        | `{TAG_NAME}`                                                         |
| `operator.image.pullPolicy`                           | Prometheus Operator image pull policy                                                | `IfNotPresent`                                                       |
| `operator.image.pullSecrets`                          | Specify docker-registry secret names as an array                                     | `[]` (does not add image pull secrets to deployed pods)              |
| `operator.serviceAccount.create`                      | Specify whether to create a ServiceAccount for Prometheus Operator                   | `true`                                                               |
| `operator.serviceAccount.name`                        | The name of the ServiceAccount to create                                             | Generated using the `prometheus-operator.operator.fullname` template |
| `operator.schedulerName`                              | Name of the k8s scheduler (other than default)                                       | `nil`                                                                |
| `operator.securityContext.enabled`                    | Enable security context                                                              | `true`                                                               |
| `operator.securityContext.fsGroup`                    | Group ID for the container filesystem                                                | `1001`                                                               |
| `operator.securityContext.runAsUser`                  | User ID for the container                                                            | `1001`                                                               |
| `operator.service.type`                               | Kubernetes service type                                                              | `ClusterIP`                                                          |
| `operator.service.port`                               | Prometheus Operator service port                                                     | `8080`                                                               |
| `operator.service.clusterIP`                          | Specific cluster IP when service type is cluster IP. Use `None` for headless service | `nil`                                                                |
| `operator.service.nodePort`                           | Kubernetes Service nodePort                                                          | `nil`                                                                |
| `operator.service.loadBalancerIP`                     | `loadBalancerIP` if service type is `LoadBalancer`                                   | `nil`                                                                |
| `operator.service.loadBalancerSourceRanges`           | Address that are allowed when svc is `LoadBalancer`                                  | `[]`                                                                 |
| `operator.service.annotations`                        | Additional annotations for Prometheus Operator service                               | `{}`                                                                 |
| `operator.serviceMonitor.enabled`                     | Creates a ServiceMonitor to monitor Prometheus Operator                              | `true`                                                               |
| `operator.serviceMonitor.interval`                    | Scrape interval (use by default, falling back to Prometheus' default)                | `nil`                                                                |
| `operator.serviceMonitor.metricRelabelings`           | Metric relabeling                                                                    | `[]`                                                                 |
| `operator.serviceMonitor.relabelings`                 | Relabel configs                                                                      | `[]`                                                                 |
| `operator.resources`                                  | CPU/Memory resource requests/limits for node                                         | `{}`                                                                 |
| `operator.podAnnotations`                             | Pod annotations                                                                      | `{}`                                                                 |
| `operator.nodeAffinity`                               | Node Affinity (this value is evaluated as a template)                                | `{}`                                                                 |
| `operator.podAntiAffinity`                            | Pod anti-affinity policy                                                             | `soft`                                                               |
| `operator.podAffinity`                                | Affinity, in addition to antiAffinity (this value is evaluated as a template)        | `{}`                                                                 |
| `operator.nodeSelector`                               | Node labels for pod assignment (this value is evaluated as a template)               | `{}`                                                                 |
| `operator.tolerations`                                | List of node taints to tolerate (this value is evaluated as a template)              | `[]`                                                                 |
| `operator.livenessProbe.enabled`                      | Turn on and off liveness probe                                                       | `true`                                                               |
| `operator.livenessProbe.initialDelaySeconds`          | Delay before liveness probe is initiated                                             | `120`                                                                |
| `operator.livenessProbe.periodSeconds`                | How often to perform the probe                                                       | `10`                                                                 |
| `operator.livenessProbe.timeoutSeconds`               | When the probe times out                                                             | `5`                                                                  |
| `operator.livenessProbe.failureThreshold`             | Minimum consecutive failures for the probe                                           | `6`                                                                  |
| `operator.livenessProbe.successThreshold`             | Minimum consecutive successes for the probe                                          | `1`                                                                  |
| `operator.readinessProbe.enabled`                     | Turn on and off readiness probe                                                      | `true`                                                               |
| `operator.readinessProbe.initialDelaySeconds`         | Delay before readiness probe is initiated                                            | `30`                                                                 |
| `operator.readinessProbe.periodSeconds`               | How often to perform the probe                                                       | `10`                                                                 |
| `operator.readinessProbe.timeoutSeconds`              | When the probe times out                                                             | `5`                                                                  |
| `operator.readinessProbe.failureThreshold`            | Minimum consecutive failures for the probe                                           | `6`                                                                  |
| `operator.readinessProbe.successThreshold`            | Minimum consecutive successes for the probe                                          | `1`                                                                  |
| `operator.logLevel`                                   | Log Level                                                                            | `info`                                                               |
| `operator.logFormat`                                  | Log Format                                                                           | `logfmt`                                                             |
| `operator.kubeletService.enabled`                     | Whether to maintain a service for scraping kubelets                                  | `true`                                                               |
| `operator.kubeletService.namespace`                   | Namespace to deploy the kubelet service                                              | `kube-system`                                                        |
| `operator.configmapReload.image.registry`             | ConfigMap Reload image registry                                                      | `docker.io`                                                          |
| `operator.configmapReload.image.repository`           | ConfigMap Reload Image name                                                          | `bitnami/configmap-reload`                                           |
| `operator.configmapReload.image.tag`                  | ConfigMap Reload Image tag                                                           | `{TAG_NAME}`                                                         |
| `operator.configmapReload.image.pullPolicy`           | ConfigMap Reload image pull policy                                                   | `IfNotPresent`                                                       |
| `operator.configmapReload.image.pullSecrets`          | Specify docker-registry secret names as an array                                     | `[]` (does not add image pull secrets to deployed pods)              |
| `operator.prometheusConfigReloader.image.registry`    | Prometheus Config Reloader image registry                                            | `docker.io`                                                          |
| `operator.prometheusConfigReloader.image.repository`  | Prometheus Config Reloader Image name                                                | `bitnami/configmap-reload`                                           |
| `operator.prometheusConfigReloader.image.tag`         | Prometheus Config Reloader Image tag                                                 | `{TAG_NAME}`                                                         |
| `operator.prometheusConfigReloader.image.pullPolicy`  | Prometheus Config Reloader image pull policy                                         | `IfNotPresent`                                                       |
| `operator.prometheusConfigReloader.image.pullSecrets` | Specify docker-registry secret names as an array                                     | `[]` (does not add image pull secrets to deployed pods)              |

### Prometheus Parameters

|                   Parameter                   |                                     Description                                      |                                Default                                 |
|-----------------------------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| `prometheus.enabled`                          | Deploy Prometheus to the cluster                                                     | `true`                                                                 |
| `prometheus.image.registry`                   | Prometheus image registry                                                            | `docker.io`                                                            |
| `prometheus.image.repository`                 | Prometheus Image name                                                                | `bitnami/prometheus`                                                   |
| `prometheus.image.tag`                        | Prometheus Image tag                                                                 | `{TAG_NAME}`                                                           |
| `prometheus.image.pullSecrets`                | Specify docker-registry secret names as an array                                     | `[]` (does not add image pull secrets to deployed pods)                |
| `prometheus.serviceAccount.create`            | Specify whether to create a ServiceAccount for Prometheus                            | `true`                                                                 |
| `prometheus.serviceAccount.name`              | The name of the ServiceAccount to create                                             | Generated using the `prometheus-operator.prometheus.fullname` template |
| `prometheus.securityContext.enabled`          | Enable security context                                                              | `true`                                                                 |
| `prometheus.securityContext.fsGroup`          | Group ID for the container filesystem                                                | `1001`                                                                 |
| `prometheus.securityContext.runAsUser`        | User ID for the container                                                            | `1001`                                                                 |
| `prometheus.podDisruptionBudget.enabled`      | Create a pod disruption budget for Prometheus                                        | `true`                                                                 |
| `prometheus.podDisruptionBudget.minAvailable` | Minimum number / percentage of pods that should remain scheduled                     | `1`                                                                    |
| `prometheus.podDisruptionBudget.minAvailable` | Maximum number / percentage of pods that may be made unavailable                     | `nil`                                                                  |
| `prometheus.service.type`                     | Kubernetes service type                                                              | `ClusterIP`                                                            |
| `prometheus.service.port`                     | Prometheus service port                                                              | `9090`                                                                 |
| `prometheus.service.clusterIP`                | Specific cluster IP when service type is cluster IP. Use `None` for headless service | `nil`                                                                  |
| `prometheus.service.nodePort`                 | Kubernetes Service nodePort                                                          | `nil`                                                                  |
| `prometheus.service.loadBalancerIP`           | `loadBalancerIP` if service type is `LoadBalancer`                                   | `nil`                                                                  |
| `prometheus.service.loadBalancerSourceRanges` | Address that are allowed when svc is `LoadBalancer`                                  | `[]`                                                                   |
| `prometheus.service.annotations`              | Additional annotations for Prometheus service                                        | `{}`                                                                   |
| `prometheus.serviceMonitor.interval`          | Scrape interval (use by default, falling back to Prometheus' default)                | `nil`                                                                  |
| `prometheus.serviceMonitor.metricRelabelings` | Metric relabeling                                                                    | `[]`                                                                   |
| `prometheus.serviceMonitor.relabelings`       | Relabel configs                                                                      | `[]`                                                                   |
| `prometheus.ingress.enabled`                  | Enable ingress controller resource                                                   | `false`                                                                |
| `prometheus.ingress.certManager`              | Add annotations for cert-manager                                                     | `false`                                                                |
| `prometheus.ingress.annotations`              | Ingress annotations                                                                  | `[]`                                                                   |
| `prometheus.ingress.hosts[0].name`            | Hostname to your Prometheus installation                                             | `prometheus.local`                                                     |
| `prometheus.ingress.hosts[0].path`            | Path within the url structure                                                        | `/`                                                                    |
| `prometheus.ingress.tls[0].hosts[0]`          | TLS hosts                                                                            | `prometheus.local`                                                     |
| `prometheus.ingress.tls[0].secretName`        | TLS Secret (certificates)                                                            | `prometheus.local-tls`                                                 |
| `prometheus.resources`                        | CPU/Memory resource requests/limits for node                                         | `{}`                                                                   |
| `prometheus.nodeAffinity`                     | Node Affinity (this value is evaluated as a template)                                | `{}`                                                                   |
| `prometheus.podAntiAffinity`                  | Pod anti-affinity policy                                                             | `soft`                                                                 |
| `prometheus.podAffinity`                      | Affinity, in addition to antiAffinity (this value is evaluated as a template)        | `{}`                                                                   |
| `prometheus.nodeSelector`                     | Node labels for pod assignment (this value is evaluated as a template)               | `{}`                                                                   |
| `prometheus.tolerations`                      | List of node taints to tolerate (this value is evaluated as a template)              | `[]`                                                                   |
| `prometheus.replicaCount`                     | Number of Prometheus replicas desired                                                | `1`                                                                    |
| `prometheus.logLevel`                         | Log level for Prometheus                                                             | `info`                                                                 |
| `prometheus.logFormat`                        | Log format for Prometheus                                                            | `logfmt`                                                               |
| `prometheus.podMetadata`                      | Standard object’s metadata                                                           | `{}`                                                                   |
| `prometheus.scrapeInterval`                   | Interval between consecutive scrapes                                                 | ``                                                                     |
| `prometheus.evaluationInterval`               | Interval between consecutive evaluations                                             | ``                                                                     |
| `prometheus.listenLocal`                      | ListenLocal makes the Prometheus server listen on loopback                           | `false`                                                                |
| `prometheus.enableAdminAPI`                   | Enable Prometheus adminitrative API                                                  | `false`                                                                |
| `prometheus.alertingEndpoints`                | Alertmanagers to which alerts will be sent                                           | `[]`                                                                   |
| `prometheus.externalLabels`                   | External labels to add to any time series                                            | `{}`                                                                   |
| `prometheus.replicaExternalLabelName`         | Name of the external label used to denote replica name                               | ``                                                                     |
| `prometheus.replicaExternalLabelNameClear`    | Clear external label used to denote replica name                                     | `false`                                                                |
| `prometheus.prometheusExternalLabelName`      | Name of the external label used to denote Prometheus instance name                   | ``                                                                     |
| `prometheus.prometheusExternalLabelNameClear` | Clear external label used to denote Prometheus instance name                         | `false`                                                                |
| `prometheus.secrets`                          | Secrets that should be mounted into the Prometheus Pods                              | `[]`                                                                   |
| `prometheus.configMaps`                       | ConfigMaps that should be mounted into the Prometheus Pods                           | `[]`                                                                   |
| `prometheus.querySpec`                        | The query command line flags when starting Prometheus                                | `{}`                                                                   |
| `prometheus.ruleNamespaceSelector`            | Namespaces to be selected for PrometheusRules discovery                              | `{}`                                                                   |
| `prometheus.ruleSelector`                     | PrometheusRules to be selected for target discovery                                  | `{}`                                                                   |
| `prometheus.serviceMonitorSelector`           | If {}, select all ServiceMonitors                                                    | `{}`                                                                   |
| `prometheus.serviceMonitorNamespaceSelector`  | Namespaces to be selected for ServiceMonitor discovery                               | `{}`                                                                   |
| `prometheus.retention`                        | Metrics retention days                                                               | `10d`                                                                  |
| `prometheus.retentionSize`                    | Maximum size of metrics                                                              | ``                                                                     |
| `prometheus.walCompression`                   | Enable compression of the write-ahead log using Snappy                               | `false`                                                                |
| `prometheus.paused`                           | If true, the Operator won't process any Prometheus configuration changes             | `false`                                                                |
| `prometheus.remoteRead`                       | The remote_read spec configuration for Prometheus                                    | `[]`                                                                   |
| `prometheus.remoteWrite`                      | The remote_write spec configuration for Prometheus                                   | `[]`                                                                   |
| `prometheus.storageSpec`                      | Prometheus StorageSpec for persistent data                                           | `{}`                                                                   |
| `prometheus.priorityClassName`                | Priority class assigned to the Pods                                                  | ``                                                                     |
| `prometheus.containers`                       | Containers allows injecting additional containers                                    | `[]`                                                                   |
| `prometheus.additionalScrapeConfigsExternal`  | Enable additional scrape configs that are managed externally to this chart           | `false`                                                                |

### Alertmanager Parameters

|                    Parameter                    |                                                    Description                                                     |                                                                                                                       Default                                                                                                                       |
|-------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `alertmanager.enabled`                          | Deploy Alertmanager to the cluster                                                                                 | `true`                                                                                                                                                                                                                                              |
| `alertmanager.image.registry`                   | Prometheus image registry                                                                                          | `docker.io`                                                                                                                                                                                                                                         |
| `alertmanager.image.repository`                 | Prometheus Image name                                                                                              | `bitnami/alertmanager`                                                                                                                                                                                                                              |
| `alertmanager.image.tag`                        | Prometheus Image tag                                                                                               | `{TAG_NAME}`                                                                                                                                                                                                                                        |
| `alertmanager.image.pullSecrets`                | Specify docker-registry secret names as an array                                                                   | `[]` (does not add image pull secrets to deployed pods)                                                                                                                                                                                             |
| `alertmanager.serviceAccount.create`            | Specify whether to create a ServiceAccount for Alertmanager                                                        | `true`                                                                                                                                                                                                                                              |
| `alertmanager.serviceAccount.name`              | The name of the ServiceAccount to create                                                                           | Generated using the `prometheus-operator.alertmanager.fullname` template                                                                                                                                                                            |
| `alertmanager.securityContext.enabled`          | Enable security context                                                                                            | `true`                                                                                                                                                                                                                                              |
| `alertmanager.securityContext.fsGroup`          | Group ID for the container filesystem                                                                              | `1001`                                                                                                                                                                                                                                              |
| `alertmanager.securityContext.runAsUser`        | User ID for the container                                                                                          | `1001`                                                                                                                                                                                                                                              |
| `alertmanager.podDisruptionBudget.enabled`      | Create a pod disruption budget for Alertmanager                                                                    | `true`                                                                                                                                                                                                                                              |
| `alertmanager.podDisruptionBudget.minAvailable` | Minimum number / percentage of pods that should remain scheduled                                                   | `1`                                                                                                                                                                                                                                                 |
| `alertmanager.podDisruptionBudget.minAvailable` | Maximum number / percentage of pods that may be made unavailable                                                   | `nil`                                                                                                                                                                                                                                               |
| `alertmanager.service.type`                     | Kubernetes service type                                                                                            | `ClusterIP`                                                                                                                                                                                                                                         |
| `alertmanager.service.port`                     | Alertmanager service port                                                                                          | `9093`                                                                                                                                                                                                                                              |
| `alertmanager.service.clusterIP`                | Specific cluster IP when service type is cluster IP. Use `None` for headless service                               | `nil`                                                                                                                                                                                                                                               |
| `alertmanager.service.nodePort`                 | Kubernetes Service nodePort                                                                                        | `nil`                                                                                                                                                                                                                                               |
| `alertmanager.service.loadBalancerIP`           | `loadBalancerIP` if service type is `LoadBalancer`                                                                 | `nil`                                                                                                                                                                                                                                               |
| `alertmanager.service.loadBalancerSourceRanges` | Address that are allowed when svc is `LoadBalancer`                                                                | `[]`                                                                                                                                                                                                                                                |
| `alertmanager.service.annotations`              | Additional annotations for Alertmanager service                                                                    | `{}`                                                                                                                                                                                                                                                |
| `alertmanager.serviceMonitor.interval`          | Scrape interval (use by default, falling back to Prometheus' default)                                              | `nil`                                                                                                                                                                                                                                               |
| `alertmanager.serviceMonitor.metricRelabelings` | Metric relabeling                                                                                                  | `[]`                                                                                                                                                                                                                                                |
| `alertmanager.serviceMonitor.relabelings`       | Relabel configs                                                                                                    | `[]`                                                                                                                                                                                                                                                |
| `alertmanager.ingress.enabled`                  | Enable ingress controller resource                                                                                 | `false`                                                                                                                                                                                                                                             |
| `alertmanager.ingress.certManager`              | Add annotations for cert-manager                                                                                   | `false`                                                                                                                                                                                                                                             |
| `alertmanager.ingress.annotations`              | Ingress annotations                                                                                                | `[]`                                                                                                                                                                                                                                                |
| `alertmanager.ingress.hosts[0].name`            | Hostname to your Alertmanager installation                                                                         | `alertmanager.local`                                                                                                                                                                                                                                |
| `alertmanager.ingress.hosts[0].path`            | Path within the url structure                                                                                      | `/`                                                                                                                                                                                                                                                 |
| `alertmanager.ingress.tls[0].hosts[0]`          | TLS hosts                                                                                                          | `alertmanager.local`                                                                                                                                                                                                                                |
| `alertmanager.ingress.tls[0].secretName`        | TLS Secret (certificates)                                                                                          | `alertmanager.local-tls`                                                                                                                                                                                                                            |
| `alertmanager.resources`                        | CPU/Memory resource requests/limits for node                                                                       | `{}`                                                                                                                                                                                                                                                |
| `alertmanager.nodeAffinity`                     | Node Affinity (this value is evaluated as a template)                                                              | `{}`                                                                                                                                                                                                                                                |
| `alertmanager.podAntiAffinity`                  | Pod anti-affinity policy                                                                                           | `soft`                                                                                                                                                                                                                                              |
| `alertmanager.podAffinity`                      | Affinity, in addition to antiAffinity (this value is evaluated as a template)                                      | `{}`                                                                                                                                                                                                                                                |
| `alertmanager.nodeSelector`                     | Node labels for pod assignment (this value is evaluated as a template)                                             | `{}`                                                                                                                                                                                                                                                |
| `alertmanager.tolerations`                      | List of node taints to tolerate (this value is evaluated as a template)                                            | `[]`                                                                                                                                                                                                                                                |
| `alertmanager.config`                           | Alertmanager configuration directive                                                                               | `{"global":{"resolve_timeout":"5m"},"route":{"group_by":["job"],"group_wait":"30s","group_interval":"5m","repeat_interval":"12h","receiver":"null","routes":[{"match":{"alertname":"Watchdog"},"receiver":"null"}]},"receivers":[{"name":"null"}]}` |
| `alertmanager.replicaCount`                     | Number of Alertmanager replicas desired                                                                            | `1`                                                                                                                                                                                                                                                 |
| `alertmanager.logLevel`                         | Log level for Alertmanager                                                                                         | `info`                                                                                                                                                                                                                                              |
| `alertmanager.logFormat`                        | Log format for Alertmanager                                                                                        | `logfmt`                                                                                                                                                                                                                                            |
| `alertmanager.podMetadata`                      | Standard object’s metadata                                                                                         | `{}`                                                                                                                                                                                                                                                |
| `alertmanager.secrets`                          | Secrets that should be mounted into the Alertmanager Pods                                                          | `[]`                                                                                                                                                                                                                                                |
| `alertmanager.configMaps`                       | ConfigMaps that should be mounted into the Alertmanager Pods                                                       | `[]`                                                                                                                                                                                                                                                |
| `alertmanager.retention`                        | Metrics retention days                                                                                             | `10d`                                                                                                                                                                                                                                               |
| `alertmanager.storageSpec`                      | Alertmanager StorageSpec for persistent data                                                                       | `{}`                                                                                                                                                                                                                                                |
| `alertmanager.paused`                           | If true, the Operator won't process any Alertmanager configuration changes                                         | `false`                                                                                                                                                                                                                                             |
| `alertmanager.listenLocal`                      | ListenLocal makes the Alertmanager server listen on loopback                                                       | `false`                                                                                                                                                                                                                                             |
| `alertmanager.containers`                       | Containers allows injecting additional containers                                                                  | `[]`                                                                                                                                                                                                                                                |
| `alertmanager.priorityClassName`                | Priority class assigned to the Pods                                                                                | ``                                                                                                                                                                                                                                                  |
| `alertmanager.additionalPeers`                  | AdditionalPeers allows injecting a set of additional Alertmanagers to peer with to form a highly available cluster | `[]`                                                                                                                                                                                                                                                |

The above parameters map to the env variables defined in [bitnami/prometheus-operator](http://github.com/bitnami/bitnami-docker-prometheus-operator). For more information please refer to the [bitnami/prometheus-operator](http://github.com/bitnami/bitnami-docker-prometheus-operator) image documentation.

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```bash
$ helm install --name my-release \
  --set operator.logLevel=debug \
  --set prometheus.replicaCount=5 \
    bitnami/prometheus-operator
```

The above command sets the Prometheus Operator `logLevel` to `debug`. Additionally it sets the `prometheus.replicaCount` to `5`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```bash
$ helm install --name my-release -f values.yaml bitnami/prometheus-operator
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Configuration and installation details

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

### Production configuration

This chart includes a `values-production.yaml` file where you can find some parameters oriented to production configuration in comparison to the regular `values.yaml`. You can use this file instead of the default one.

- Modify the Log level for Prometheus Operator:

```diff
-   logLevel: info
+   logLevel: error
```

- Increase the number of days to retain metrics:

```diff
-   retention: 10d
+   retention: 30d
```

- Increase the number of Alertmanager replicas:

```diff
-   replicaCount: 1
+   replicaCount: 3
```

- Modify the Log level for Alertmanager:

```diff
-   logLevel: info
+   logLevel: error
```

- Increase the number of Prometheus replicas:

```diff
-   replicaCount: 1
+   replicaCount: 3
```

- Modify the Log level for Prometheus:

```diff
-   logLevel: info
+   logLevel: error
```

## Upgrading

```bash
$ helm upgrade my-release bitnami/prometheus-operator
```
