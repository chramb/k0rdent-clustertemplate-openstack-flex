# k0rdent OpenStack ClusterTemplate

Chart that allows for customization of any CAPI object

Based off upstream k0rdent openstack-standalone-cp 1.0.6 template

## Installation instructions

Apply these two manifests

```yml
---
apiVersion: source.toolkit.fluxcd.io/v1
kind: GitRepository
metadata:
  name: k0rdent-clustertemplate-openstack-flex
  namespace: kcm-system
  labels:
    k0rdent.mirantis.com/managed: "true"
spec:
  interval: 5m0s
  url: https://github.com/chramb/k0rdent-clustertemplate-openstack-flex
  ref:
    branch: dev
---
apiVersion: k0rdent.mirantis.com/v1alpha1
kind: ClusterTemplate
metadata:
  name: openstack-flex-1-0-6
  namespace: kcm-system
spec:
  helm:
    chartSpec:
      chart: ./
      interval: 10m0s
      reconcileStrategy: ChartVersion
      sourceRef:
        kind: GitRepository
        name: k0rdent-clustertemplate-openstack-flex
      version: 1.0.6
```


