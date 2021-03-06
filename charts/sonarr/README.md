# sonarr televsion show download client

This is a helm chart for [sonarr](https://github.com/sonarr/sonarr/) leveraging the [Linuxserver.io image](https://hub.docker.com/r/linuxserver/sonarr/)

## TL;DR;

```shell
$ helm repo add billimek https://billimek.com/billimek-charts/
$ helm install billimek/sonarr
```

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm install --name my-release billimek/sonarr
```

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete my-release --purge
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the Sentry chart and their default values.

| Parameter                                   | Description                                                                                  | Default                                        |
|---------------------------------------------|----------------------------------------------------------------------------------------------|------------------------------------------------|
| `image.repository`                          | Image repository                                                                             | `linuxserver/sonarr`                           |
| `image.tag`                                 | Image tag. Possible values listed [here](https://hub.docker.com/r/linuxserver/sonarr/tags/). | `2.0.0.5344-ls60`                              |
| `image.pullPolicy`                          | Image pull policy                                                                            | `IfNotPresent`                                 |
| `strategyType`                              | Specifies the strategy used to replace old Pods by new ones                                  | `Recreate`                                     |
| `timezone`                                  | Timezone the instance should run as, e.g. 'America/New_York'                                 | `UTC`                                          |
| `puid`                                      | process userID the instance should run as                                                    | `1001`                                         |
| `pgid`                                      | process groupID the instance should run as                                                   | `1001`                                         |
| `exportarr.enabled`                         | Enable Prometheus monitoring with [Exportarr](https://github.com/onedr0p/exportarr)          | `false`                                        |
| `exportarr.image.repository`                | Exportarr image repository                                                                   | `onedr0p/exportarr`                            |
| `exportarr.image.tag`                       | Exportarr image tag                                                                          | `v0.3.0`                                       |
| `exportarr.image.pullPolicy`                | Exportarr image pullPolicy                                                                   | `IfNotPresent`                                 |
| `exportarr.port`                            | Prometheus scrape port                                                                       | `9707`                                         |
| `exportarr.url`                             | Sonarr's URL                                                                                 | `http://sonarr.default.svc.cluster.local:8989` |
| `exportarr.apikey`                          | Sonarr's API Key                                                                             |                                                |
| `exportarr.enableEpisodeQualityMetrics`     | Enable episode quality metrics gathering                                                     | `false`                                        |
| `exportarr.serviceMonitor.enabled`          | Enable Prometheus Operator ServiceMonitor monitoring                                         | `false`                                        |
| `exportarr.serviceMonitor.namespace`        | Define namespace where to deploy the ServiceMonitor resource                                 | (namespace where you are deploying)            |
| `exportarr.serviceMonitor.path`             | Prometheus scrape path                                                                       | `/metrics`                                     |
| `exportarr.serviceMonitor.interval`         | Prometheus scrape interval                                                                   | `4m`                                           |
| `exportarr.serviceMonitor.scrapeTimeout`    | Prometheus scrape timeout                                                                    | `90s`                                          |
| `exportarr.serviceMonitor.additionalLabels` | Add custom labels to ServiceMonitor                                                          | {}                                             |
| `probes.liveness.initialDelaySeconds`       | Specify liveness `initialDelaySeconds` parameter for the deployment                          | `60`                                           |
| `probes.liveness.failureThreshold`          | Specify liveness `failureThreshold` parameter for the deployment                             | `5`                                            |
| `probes.liveness.timeoutSeconds`            | Specify liveness `timeoutSeconds` parameter for the deployment                               | `10`                                           |
| `probes.readiness.initialDelaySeconds`      | Specify readiness `initialDelaySeconds` parameter for the deployment                         | `60`                                           |
| `probes.readiness.failureThreshold`         | Specify readiness `failureThreshold` parameter for the deployment                            | `5`                                            |
| `probes.readiness.timeoutSeconds`           | Specify readiness `timeoutSeconds` parameter for the deployment                              | `10`                                           |
| `service.type`                              | Kubernetes service type for the GUI                                                          | `ClusterIP`                                    |
| `service.port`                              | Kubernetes port where the GUI is exposed                                                     | `8989`                                         |
| `service.annotations`                       | Service annotations for the GUI                                                              | `{}`                                           |
| `service.labels`                            | Custom labels                                                                                | `{}`                                           |
| `service.loadBalancerIP`                    | Loadbalancer IP for the GUI                                                                  | `{}`                                           |
| `service.loadBalancerSourceRanges`          | List of IP CIDRs allowed access to load balancer (if supported)                              | None                                           |
| `ingress.enabled`                           | Enables Ingress                                                                              | `false`                                        |
| `ingress.annotations`                       | Ingress annotations                                                                          | `{}`                                           |
| `ingress.labels`                            | Custom labels                                                                                | `{}`                                           |
| `ingress.path`                              | Ingress path                                                                                 | `/`                                            |
| `ingress.hosts`                             | Ingress accepted hostnames                                                                   | `chart-example.local`                          |
| `ingress.tls`                               | Ingress TLS configuration                                                                    | `[]`                                           |
| `persistence.config.enabled`                | Use persistent volume to store configuration data                                            | `true`                                         |
| `persistence.config.size`                   | Size of persistent volume claim                                                              | `1Gi`                                          |
| `persistence.config.existingClaim`          | Use an existing PVC to persist data                                                          | `nil`                                          |
| `persistence.config.storageClass`           | Type of persistent volume claim                                                              | `-`                                            |
| `persistence.config.accessMode`             | Persistence access mode                                                                      | `ReadWriteOnce`                                |
| `persistence.config.skipuninstall`          | Do not delete the pvc upon helm uninstall                                                    | `false`                                        |
| `persistence.downloads.enabled`             | Use persistent volume for downloads                                                          | `true`                                         |
| `persistence.downloads.size`                | Size of persistent volume claim                                                              | `10Gi`                                         |
| `persistence.downloads.existingClaim`       | Use an existing PVC to persist data                                                          | `nil`                                          |
| `persistence.downloads.storageClass`        | Type of persistent volume claim                                                              | `-`                                            |
| `persistence.downloads.accessMode`          | Persistence access mode                                                                      | `ReadWriteOnce`                                |
| `persistence.downloads.skipuninstall`       | Do not delete the pvc upon helm uninstall                                                    | `false`                                        |
| `persistence.tv.enabled`                    | Use persistent volume for tv show persistence                                                | `true`                                         |
| `persistence.tv.size`                       | Size of persistent volume claim                                                              | `10Gi`                                         |
| `persistence.tv.existingClaim`              | Use an existing PVC to persist data                                                          | `nil`                                          |
| `persistence.tv.storageClass`               | Type of persistent volume claim                                                              | `-`                                            |
| `persistence.tv.accessMode`                 | Persistence access mode                                                                      | `ReadWriteOnce`                                |
| `persistence.tv.skipuninstall`              | Do not delete the pvc upon helm uninstall                                                    | `false`                                        |
| `persistence.extraExistingClaimMounts`      | Optionally add multiple existing claims                                                      | `[]`                                           |
| `resources`                                 | CPU/Memory resource requests/limits                                                          | `{}`                                           |
| `nodeSelector`                              | Node labels for pod assignment                                                               | `{}`                                           |
| `tolerations`                               | Toleration labels for pod assignment                                                         | `[]`                                           |
| `affinity`                                  | Affinity settings for pod assignment                                                         | `{}`                                           |
| `podAnnotations`                            | Key-value pairs to add as pod annotations                                                    | `{}`                                           |
| `deploymentAnnotations`                     | Key-value pairs to add as deployment annotations                                             | `{}`                                           |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install --name my-release \
  --set timezone="America/New York" \
    billimek/sonarr
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install --name my-release -f values.yaml stable/sonarr
```

---
**NOTE**

If you get `Error: rendered manifests contain a resource that already exists. Unable to continue with install: existing resource conflict: ...` it may be because you uninstalled the chart with `skipuninstall` enabled, you need to manually delete the pvc or use `existingClaim`.

---

Read through the [values.yaml](https://github.com/billimek/billimek-charts/blob/master/charts/sonarr/values.yaml) file. It has several commented out suggested values.
