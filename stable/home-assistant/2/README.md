# Home Assistant

This is a helm chart for [Home Assistant](https://www.home-assistant.io/)

## TL;DR;

```console
$ helm install stable/home-assistant
```

## Introduction

This code is adopted for [the official home assistant docker image](https://hub.docker.com/r/homeassistant/home-assistant/)

## Installing the Chart

To install the chart with the release name `my-release`:

```console
$ helm install --name my-release stable/home-assistant
```
## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
$ helm delete my-release --purge
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables lists the configurable parameters of the Sentry chart and their default values.

| Parameter                  | Description                         | Default                                                 |
|----------------------------|-------------------------------------|---------------------------------------------------------|
| `image.repository`         | Image repository | `homeassistant/home-assistant` |
| `image.tag`                | Image tag. Possible values listed [here](https://hub.docker.com/r/jacobalberty/home-assistant/tags/).| `0.72.1`|
| `image.pullPolicy`         | Image pull policy | `IfNotPresent` |
| `service.type`             | Kubernetes service type for the home-assistant GUI | `ClusterIP` |
| `service.port`             | Kubernetes port where the home-assistant GUI is exposed| `8123` |
| `service.annotations`      | Service annotations for the home-assistant GUI | `{}` |
| `service.clusterIP`   | Cluster IP for the home-assistant GUI | `` |
| `service.externalIPs`   | External IPs for the home-assistant GUI | `[]` |
| `service.loadBalancerIP`   | Loadbalancer IP for the home-assistant GUI | `` |
| `service.loadBalancerSourceRanges`   | Loadbalancer client IP restriction range for the home-assistant GUI | `[]` |
| `hostNetwork`              | Enable hostNetwork - might be needed for discovery to work | `false` |
| `service.nodePort`   | nodePort to listen on for the home-assistant GUI | `` |
| `ingress.enabled`              | Enables Ingress | `false` |
| `ingress.annotations`          | Ingress annotations | `{}` |
| `ingress.path`                 | Ingress path | `/` |
| `ingress.hosts`                | Ingress accepted hostnames | `chart-example.local` |
| `ingress.tls`                  | Ingress TLS configuration | `[]` |
| `persistence.enabled`      | Use persistent volume to store data | `true` |
| `persistence.size`         | Size of persistent volume claim | `5Gi` |
| `persistence.existingClaim`| Use an existing PVC to persist data | `nil` |
| `persistence.storageClass` | Type of persistent volume claim | `-` |
| `persistence.accessMode`  | Persistence access modes | `ReadWriteMany` |
| `extraEnv`          | Extra ENV vars to pass to the home-assistant container | `{}` |
| `configurator.enabled`     | Enable the optional [configuration UI](https://github.com/danielperna84/hass-configurator) | `false` |
| `configurator.image.repository`         | Image repository | `billimek/hass-configurator-docker` |
| `configurator.image.tag`                | Image tag | `x86_64-0.3.0`|
| `configurator.image.pullPolicy`         | Image pull policy | `IfNotPresent` |
| `configurator.hassApiUrl`               | Home Assistant API URL (e.g. 'http://home-assistant:8123/api/') - will auto-configure to proper URL if not set | ``|
| `configurator.hassApiPassword`          | Home Assistant API Password | `` |
| `configurator.basepath`                 | Base path of the home assistant configuration files | `/config` |
| `configurator.enforceBasepath`          | If set to true, will prevent navigation to other directories in the configurator UI | `true` |
| `configurator.username`                 | If this and password (below) are set, will require basic auth to access the configurator UI  | `` |
| `configurator.password`                 | If this and username (above) are set, will require basic auth to access the configurator UI. password is in the format of a sha256 hash (e.g. "test" would be "{sha256}9f86d081884c7d659a2feaa0c55ad015a3bf4f1b2b0b822cd15d6c15b0f00a08")  | `` |
| `configurator.extraEnv`                 | Extra ENV vars to pass to the configuration UI | `{}` |
| `configurator.ingress.enabled`          | Enables Ingress for the configurator UI | `false` |
| `configurator.ingress.annotations`      | Ingress annotations for the configurator UI | `{}` |
| `configurator.ingress.hosts`            | Ingress accepted hostnames for the configurator UI | `chart-example.local` |
| `configurator.ingress.tls`              | Ingress TLS configuration for the configurator UI | `[]` |
| `configurator.strategy.type`            | hass-configurator Deployment Strategy type | `` |
| `configurator.tolerations`              | Toleration labels for pod assignment for the configurator UI | `[]` |
| `configurator.nodeSelector`             | Node labels for pod assignment for the configurator UI | `{}` |
| `configurator.schedulerName`            | Use an alternate scheduler, e.g. "stork" for the configurator UI | `` |
| `configurator.podAnnotations`           | Affinity settings for pod assignment for the configurator UI | `{}` |
| `configurator.replicaCount`             | Number of replicas for the configurator UI | `1` |
| `configurator.resources`                | CPU/Memory resource requests/limits for the configurator UI | `{}` |
| `configurator.securityContext`          | Security context to be added to hass-configurator pods for the configurator UI | `{}` |
| `configurator.service.type`             | Kubernetes service type for the configurator UI | `ClusterIP` |
| `configurator.service.port`             | Kubernetes port where the configurator UI is exposed| `3218` |
| `configurator.service.nodePort`         | nodePort to listen on for the configurator UI | `` |
| `configurator.service.annotations`      | Service annotations for the configurator UI | `{}` |
| `configurator.service.labels`           | Service labels to use for the configurator UI | `{}` |
| `configurator.service.clusterIP`        | Cluster IP for the configurator UI | `` |
| `configurator.service.externalIPs`      | External IPs for the configurator UI | `[]` |
| `configurator.service.loadBalancerIP`   | Loadbalancer IP for the configurator UI | `` |
| `configurator.service.loadBalancerSourceRanges`   | Loadbalancer client IP restriction range for the configurator UI | `[]` |
| `resources`                | CPU/Memory resource requests/limits or the home-assistant GUI | `{}` |
| `nodeSelector`             | Node labels for pod assignment or the home-assistant GUI | `{}` |
| `tolerations`              | Toleration labels for pod assignment or the home-assistant GUI | `[]` |
| `affinity`                 | Affinity settings for pod assignment or the home-assistant GUI | `{}` |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install --name my-release \
  --set configurator.hassApiPassword="$HASS_API_PASSWORD" \
    stable/home-assistant
```

Alternatively, a YAML file that specifies the values for the above parameters can be provided while installing the chart. For example,

```console
helm install --name my-release -f values.yaml stable/home-assistant
```

Read through the [values.yaml](values.yaml) file. It has several commented out suggested values.

## Regarding configuring home assistant

Much of the home assistant configuration occurs inside the various files persisted to the `/config` directory.  This will require external access to the persistent storage location where the home assistant configuration data is stored.

Because this may be a limitation, the [Home Assistant Configurator UI](https://github.com/danielperna84/hass-configurator) is added to the chart as an option to provide a webUI for editing the various configuration files.
