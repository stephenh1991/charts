OpenEBS
=======

[OpenEBS](https://github.com/openebs/openebs) is an open source storage platform that provides persistent and containerized block storage for DevOps and container environments.

OpenEBS can be deployed on any Kubernetes cluster - either in cloud, on-premise or developer laptop (minikube). OpenEBS itself is deployed as just another container on your cluster, and enables storage services that can be designated on a per pod, application, cluster or container level.

Introduction
------------

This chart bootstraps OpenEBS deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

## Prerequisites
- Kubernetes 1.7.5+ with RBAC enabled
- iSCSI PV support in the underlying infrastructure

## Installing OpenEBS
```
helm install --namespace openebs stable/openebs
```

## Installing OpenEBS with the release name `my-release`:
```
helm install --name `my-release` --namespace openebs stable/openebs
```

## To uninstall/delete the `my-release` deployment:
```
helm ls --all
helm delete `my-release`
```


## Configuration

The following table lists the configurable parameters of the OpenEBS chart and their default values.

| Parameter                               | Description                                   | Default                                   |
| ----------------------------------------| --------------------------------------------- | ----------------------------------------- |
| `rbac.create`                           | Enable RBAC Resources                         | `true`                                    |
| `image.pullPolicy`                      | Container pull policy                         | `IfNotPresent`                            |
| `apiserver.image`                       | Image for API Server                          | `quay.io/openebs/m-apiserver`             |
| `apiserver.imageTag`                    | Image Tag for API Server                      | `0.9.0`                                   |
| `apiserver.replicas`                    | Number of API Server Replicas                 | `1`                                       |
| `apiserver.sparse.enabled`              | Create Sparse Pool based on Sparsefile        | `false`                                   |
| `provisioner.image`                     | Image for Provisioner                         | `quay.io/openebs/openebs-k8s-provisioner` |
| `provisioner.imageTag`                  | Image Tag for Provisioner                     | `0.9.0`                                   |
| `provisioner.replicas`                  | Number of Provisioner Replicas                | `1`                                       |
| `localProvisioner.image`                | Image for localProvisioner                    | `quay.io/openebs/provisioner-localpv`     |
| `localProvisioner.imageTag`             | Image Tag for localProvisioner                | `0.9.0`                                   |
| `localProvisioner.replicas`             | Number of localProvisioner Replicas           | `1`                                       |
| `localProvisioner.basePath`             | BasePath for hostPath volumes on Nodes        | `/var/openebs/local`                                       |
| `webhook.image`                         | Image for admision server                     | `quay.io/openebs/admission-server`        |
| `webhook.imageTag`                      | Image Tag for admission server                | `0.9.0`                                   |
| `webhook.replicas`                      | Number of admission server Replicas           | `1`                                       |
| `snapshotOperator.provisioner.image`    | Image for Snapshot Provisioner                | `quay.io/openebs/snapshot-provisioner`    |
| `snapshotOperator.provisioner.imageTag` | Image Tag for Snapshot Provisioner            | `0.9.0`                                   |
| `snapshotOperator.controller.image`     | Image for Snapshot Controller                 | `quay.io/openebs/snapshot-controller`     |
| `snapshotOperator.controller.imageTag`  | Image Tag for Snapshot Controller             | `0.9.0`                                   |
| `snapshotOperator.replicas`             | Number of Snapshot Operator Replicas          | `1`                                       |
| `ndm.image`                             | Image for Node Disk Manager                   | `quay.io/openebs/node-disk-manager-amd64` |
| `ndm.imageTag`                          | Image Tag for Node Disk Manager               | `v0.3.5`                                  |
| `ndm.sparse.path`                       | Directory where Sparse files are created      | `/var/openebs/sparse`                     |
| `ndm.sparse.size`                       | Size of the sparse file in bytes              | `10737418240`                             |
| `ndm.sparse.count`                      | Number of sparse files to be created          | `1`                                       |
| `ndm.filters.excludeVendors`            | Exclude devices with specified vendor         | `CLOUDBYT,OpenEBS`                        |
| `ndm.filters.excludePaths`              | Exclude devices with specified path patterns  | `loop,fd0,sr0,/dev/ram,/dev/dm-,/dev/md`  |
| `ndm.filters.includePaths`              | Include devices with specified path patterns  | `""`                                      |
| `jiva.image`                            | Image for Jiva                                | `quay.io/openebs/jiva`                    |
| `jiva.imageTag`                         | Image Tag for Jiva                            | `0.9.0`                                   |
| `jiva.replicas`                         | Number of Jiva Replicas                       | `3`                                       |
| `cstor.pool.image`                      | Image for cStor Pool                          | `quay.io/openebs/cstor-pool`              |
| `cstor.pool.imageTag`                   | Image Tag for cStor Pool                      | `0.9.0`                                   |
| `cstor.poolMgmt.image`                  | Image for cStor Pool  Management              | `quay.io/openebs/cstor-pool-mgmt`         |
| `cstor.poolMgmt.imageTag`               | Image Tag for cStor Pool Management           | `0.9.0`                                   |
| `cstor.target.image`                    | Image for cStor Target                        | `quay.io/openebs/cstor-istgt`             |
| `cstor.target.imageTag`                 | Image Tag for cStor Target                    | `0.9.0`                                   |
| `cstor.volumeMgmt.image`                | Image for cStor Volume  Management            | `quay.io/openebs/cstor-volume-mgmt`       |
| `cstor.volumeMgmt.imageTag`             | Image Tag for cStor Volume Management         | `0.9.0`                                   |
| `policies.monitoring.image`             | Image for Prometheus Exporter                 | `quay.io/openebs/m-exporter`              |
| `policies.monitoring.imageTag`          | Image Tag for Prometheus Exporter             | `0.9.0`                                   |
| `analytics.enabled`                     | Enable sending stats to Google Analytics      | `true`                                    |
| `analytics.pingInterval`                | Duration(hours) between sending ping stat     | `24h`                                     |
| `HealthCheck.initialDelaySeconds`       | Delay before liveness probe is initiated      | `30`                                      |                              | 30                                                          |
| `HealthCheck.periodSeconds`             | How often to perform the liveness probe       | `60`                                      |                            | 10                                                          |

Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`.

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```shell
helm install --name `my-release` -f values.yaml stable/openebs
```

> **Tip**: You can use the default [values.yaml](values.yaml)
