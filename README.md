# radiantone-argocd-helm

This example application demonstrates how an OTS (off-the-shelf) helm chart can be retrieved and pinned to a specific helm sem version from an upstream helm repository, and customized using a custom values.yaml in the private git repository.

In this example, the radiantone/fid application is pulled from the stable helm repo, and pinned to v1.0.0:

```yaml
dependencies:
- name: fid
  version: 1.0.0
```

A custom values.yaml is used to customize the parameters of the radiantone/fid helm chart:

```yaml
fid:
  fullnameOverride: fid
  image:
    tag: "7.3.28"
  replicaCount: 2
  service:
    type: NodePort
  fid:
    rootPassword: "<random password>"
    license: "<license key>"
  dependencies:
    zookeeper:
      enabled: true
  resources:
    limits:
      cpu: 2
      memory: 2Gi
    requests:
      cpu: 1
      memory: 1Gi
  persistence:
    enabled: true
    storageClass: gp3
    size: 50Gi

  zookeeper:
    fullnameOverride: zookeeper
    persistence:
      enabled: true
      storageClass: gp3
      size: 10Gi
```
