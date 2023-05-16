
# Accelya - UAT OpenShift Cluster Health Check Documentation

- [Accelya - UAT OpenShift Cluster Health Check](#accelya---uat-openshift-cluster-health-check-documentation)
    - [Cluster Overview](#cluster-overview)
    - [Cluster Inventory](#cluster-inventory)
        - [Cluster Nodes](#cluster-nodes)
        - [Cluster Projects](#cluster-projects-namespaces)
        - [Cluster Resource Quotas and Limit Ranges](#cluster-resource-quotas-and-limit-ranges)
        - [Installed Operators](#installed-operators)
        - [ETCD encryption](#etcd-encryption)
    - [Cluster Network Configuration](#cluster-network-configuration)
        - [Cluster Network& Service CIDR, Network Provider](#cluster-network--service-cidr-network-provider)
        - [OpenShift Ingress Controller and Route Configuration](#openshift-ingress-controller-and-route-configuration)
    - [Cluster Storage Configuration](#cluster-storage-configuration)
        - [Cluster CSI Nodes](#cluster-csi-nodes)
        - [Storage Classes](#storage-classes)
        - [Internal Image Registry Configuration](#internal-image-registry-configuration)
    - [Cluster Security Configuration](#cluster-security-configuration)

## Cluster Overview 

- **Cluster API Address**: https://api.nfeocpuat.accelya.local:6443
- **Infrastructure provide**: VSphere
- **OpenShift Version**: 4.11.20 (Stable 4.11) -> **Kubernetes Versoion**: v1.24.6+5658434
- **Cluster Nodes**: 10 (3 Master, 4 Worker, 3 Infra)
- **Cluster Projects**: 134
- **Cluster Monitoring, Logging, Security and Backup tools**:
    - Monitoring: OpenShift Monitoring (Default)
    - Logging: ElasticSearch
    - Security: SentielOne **(No resources found)** & Compliance Operator
    - Backup: None

## Cluster Inventory

### Cluster Nodes

**Total no. of ndoes**: 10

|Node Type|Nodes|CPU|Memory|Disks|
|---|---|---|---|---|
|Master|vlnfeuatmast1.nfeocpuat.cluster.adp|8 Cores| 32 GB|250GB|
|Master|vlnfeuatmast2.nfeocpuat.cluster.adp|8 Cores| 32 GB|250GB|
|Master|vlnfeuatmast3.nfeocpuat.cluster.adp|8 Cores| 32 GB|250GB|
|Infra|vlnfeuatinf1.nfeocpuat.cluster.adp|8 Cores| 64 GB|250GB, 1.1TB, 500GB|
|Infra|vlnfeuatinf2.nfeocpuat.cluster.adp|8 Cores| 64 GB|250GB, 1.1TB|
|Infra|vlnfeuatinf3.nfeocpuat.cluster.adp|8 Cores| 64 GB|250GB, 1.1TB, 500GB|
|Worker|vlnfeuatwrk1.nfeocpuat.cluster.adp|12 Cores| 51 GB|250GB, 300GB|
|Worker|vlnfeuatwrk2.nfeocpuat.cluster.adp|12 Cores| 51 GB|250GB, 300GB|
|Infra|vlnfeuatwrk3.nfeocpuat.cluster.adp|12 Cores| 51 GB|250GB, 50GB, 50GB|
|Infra|vlnfeuatwrk4.nfeocpuat.cluster.adp|12 Cores| 51 GB|250GB|

```
NAME                                  STATUS   ROLES    AGE    VERSION
vlnfeuatinf1.nfeocpuat.cluster.adp    Ready    infra    124d   v1.24.6+5658434
vlnfeuatinf2.nfeocpuat.cluster.adp    Ready    infra    124d   v1.24.6+5658434
vlnfeuatinf3.nfeocpuat.cluster.adp    Ready    infra    124d   v1.24.6+5658434
vlnfeuatmast1.nfeocpuat.cluster.adp   Ready    master   124d   v1.24.6+5658434
vlnfeuatmast2.nfeocpuat.cluster.adp   Ready    master   124d   v1.24.6+5658434
vlnfeuatmast3.nfeocpuat.cluster.adp   Ready    master   124d   v1.24.6+5658434
vlnfeuatwrk1.nfeocpuat.cluster.adp    Ready    worker   124d   v1.24.6+5658434
vlnfeuatwrk2.nfeocpuat.cluster.adp    Ready    worker   124d   v1.24.6+5658434
vlnfeuatwrk3.nfeocpuat.cluster.adp    Ready    worker   124d   v1.24.6+5658434
vlnfeuatwrk4.nfeocpuat.cluster.adp    Ready    worker   124d   v1.24.6+5658434
```

### Cluster Projects (Namespaces)

**Total no. of Projects**: 134

|System Projects|User Projects|Comment|
|---|---|---|
| openshift                                        | advanced-payment-management       |   |
| openshift-apiserver                              | agent-management                  |   |
| openshift-apiserver-operator                     | airline-management                |   |
| openshift-authentication                         | asd-stock-request                 |   |
| openshift-authentication-operator                | batch-migration-processor         |   |
| openshift-cloud-controller-manager               | bsp-management                    |   |
| openshift-cloud-controller-manager-operator      | cassandra-exporter                |   |
| openshift-cloud-credential-operator              | cdc-replication-job               |   |
| openshift-cloud-network-config-controller        | cicd                              |   |
| openshift-cluster-csi-drivers                    | currency-management               |   |
| openshift-cluster-machine-approver               | database                          |   |
| openshift-cluster-node-tuning-operator           | demo-sm                           |   |
| openshift-cluster-samples-operator               | dmz                               |   |
| openshift-cluster-storage-operator               | document-enquiry                  |   |
| openshift-cluster-version                        | elastic-cloud                     |   |
| openshift-compliance                             | elasticsearch7-exporter           |   |
| openshift-config                                 | fop-authentication-service        |   |
| openshift-config-managed                         | fop-risk-monitoring               |   |
| openshift-config-operator                        | frontend                          |   |
| openshift-console                                | gateway                           |   |
| openshift-console-operator                       | gds-management                    |   |
| openshift-console-user-settings                  | globalsearch                      |   |
| openshift-controller-manager                     | grafana                           |   |
| openshift-controller-manager-operator            | hot-load-document-transformer     |   |
| openshift-distributed-tracing                    | hot-load-evaluation-processor     |   |
| openshift-dns                                    | hot-load-file-processor           |   |
| openshift-dns-operator                           | hot-load-file-scheduler           |   |
| openshift-etcd                                   | informix-cdc                      |   |
| openshift-etcd-operator                          | istio-system                      |   |
| openshift-file-integrity                         | kong                              |  Any Appliction using Kong API |
| openshift-host-network                           | management                        |   |
| openshift-image-registry                         | monitoring-service                |   |
| openshift-infra                                  | notification-management           |   |
| openshift-ingress                                | notification-processor            |   |
| openshift-ingress-canary                         | pbd-management                    |   |
| openshift-ingress-operator                       | period-management                 |   |
| openshift-insights                               | postgres-exporter                 |   |
| openshift-kni-infra                              | postgresql                        |   |
| openshift-kube-apiserver                         | qualys                            |   |
| openshift-kube-apiserver-operator                | rabbitmq                          |   |
| openshift-kube-controller-manager                | redis                             |   |
| openshift-kube-controller-manager-operator       | rejected-documents-file-processor |   |
| openshift-kube-scheduler                         | rejected-documents-file-scheduler |   |
| openshift-kube-scheduler-operator                | rejected-documents-management     |   |
| openshift-kube-storage-version-migrator          | sales-query                       |   |
| openshift-kube-storage-version-migrator-operator | sales-query-processor             |   |
| openshift-logging                                | sentinelone                       |   |
| openshift-machine-api                            | test                              |   |
| openshift-machine-config-operator                | test-shg                          |   |
| openshift-marketplace                            | testshg - test_shg                |   |
| openshift-monitoring                             | sales-query-processor             |   |
| openshift-multus                                 | ticketing-authority               |   |
| openshift-network-diagnostics                    | tsimon-ns1                        |   |
| openshift-network-operator                       | tsimon-ns2                        |   |
| openshift-node                                   | user-feedback                     |   |
| openshift-nutanix-infra                          | user-management-integration       |   |
| openshift-oauth-apiserver                        | wechat-management                 |   |
| openshift-openstack-infra                        | zookeeper                         |   |
| openshift-operator-lifecycle-manager             | user-feedback                     |   |
| openshift-operators                              | user-management-integration       |   |
| openshift-operators-redhat                       | wechat-management                 |   |
| openshift-ovirt-infra                            | zookeeper                         |   |
| openshift-route-controller-manager               |                                   |   |
| openshift-sdn                                    |                                   |   |
| openshift-service-ca                             |                                   |   |
| openshift-service-ca-operator                    |                                   |   |
| openshift-user-workload-monitoring               |                                   |   |
| openshift-vsphere-infra                          |                                   |   |
| default                                          |                                   |   |
| audit                                            |                                   |   |
| kube-node-lease                                  |                                   |   |
| kube-public                                      |                                   |   |
| kube-system                                      |                                   |   |

<span style="color:red"> **Recommendation:** </span>
- Some of of the Infra related components Pods are running on worker nodes. Please use proper labeling, taints and tolerations to schedule Infra Pods on Infra Nodes to save OpenShift licensing cost.

### Cluster Resource Quotas and Limit Ranges

- Resource Quotas only defined for `openshift-host-network` namespace. 

<span style="color:red"> **Recommendation:** </span>
- Define Cluser Resource Quotas and Limit Ranges for above mentioned User Projects for better utilization of Cluster CPU and Memory resources. Also, proper settings of Quotas and Ranges will help identify overall cluster utilization and costing. 

### Installed Operators

|Installed Operator|Namespace|Managed Namespace|
|---|---|---|
|Red Hat OpenShift Logging|openshift-logging|openshift-logging|
|Compliance Operator|openshift-compliance|All Namespaces|
|OpenShift ElasticSearch Operator|openshift-operators-redhat|All Namespaces|
|file-integrity-operator|openshift-file-integrity|none|
|Red Hat OpenShift distributed tracing platform|openshift-distributed-tracing|All Namespaces|
|Kiali Operator|openshift-operators|All Namespaces|
|Red Hat OpenShift Service Mesh|openshift-operators|All Namespaces|

### ETCD encryption

- Currenlty not enabled

<span style="color:green"> **Recommendation:** </span>
- Please follow provided link to enable ETCD encryption if require. https://docs.openshift.com/container-platform/4.11/security/encrypting-etcd.html

## Cluster Network Configuration

### Cluster Network & Service CIDR, Network Provider

```yaml
Spec:
  Cluster Network:
    Cidr:         10.128.0.0/14
    Host Prefix:  24
  External IP:
    Policy:
  Network Type:  OpenShiftSDN
  Service Network:
    172.30.0.0/16
Status:
  Cluster Network:
    Cidr:               10.128.0.0/14
    Host Prefix:        24
  Cluster Network MTU:  1450
  Network Type:         OpenShiftSDN
  Service Network:
    172.30.0.0/16
```
<span style="color:green"> **Recommendation:** </span>
- Current **Cluster Network Type** is `OpenShiftSDN`. Starting from OpenShift versoin 4.12.x, default **Cluster Network Type** will be `OVN-Kubernetes` for new cluster installation. 

### OpenShift Ingress Controller and Route Configuration

- Currently cluster uses default Ingress Controller to create new routes and exposes deployed Applications.

```
NAMESPACE                    NAME      AGE
openshift-ingress-operator   default   125d
```

<span style="color:green"> **Recommendation:** </span>
- Create additional sharded Ingress Controller on cluster, which allows 
    - To use custom TLS certificates for Applications other than default `*.apps` certificate
    - Customization of endpoint URLs for routes 


## Cluster Storage Configuration

### Cluster CSI Nodes

```
NAME                                  DRIVERS   AGE
vlnfeuatinf1.nfeocpuat.cluster.adp    1         125d
vlnfeuatinf2.nfeocpuat.cluster.adp    1         125d
vlnfeuatinf3.nfeocpuat.cluster.adp    1         125d
vlnfeuatmast1.nfeocpuat.cluster.adp   1         125d
vlnfeuatmast2.nfeocpuat.cluster.adp   1         125d
vlnfeuatmast3.nfeocpuat.cluster.adp   1         125d
vlnfeuatwrk1.nfeocpuat.cluster.adp    1         125d
vlnfeuatwrk2.nfeocpuat.cluster.adp    1         125d
vlnfeuatwrk3.nfeocpuat.cluster.adp    1         125d
vlnfeuatwrk4.nfeocpuat.cluster.adp    1         125
```

<span style="color:green"> **Recommendation:** </span>
-  Leverage equal no. of volumes and similar sizes across all CSI nodes. 

### Storage Classes

```
NAME              PROVISIONER                    RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
nfs-non-dynamic   kubernetes.io/no-provisioner   Retain          Immediate              true                   119d
thin (default)    kubernetes.io/vsphere-volume   Delete          Immediate              false                  124d
thin-csi          csi.vsphere.vmware.com         Delete          WaitForFirstConsumer   true                   124d
thin-csi-retain   csi.vsphere.vmware.com         Retain          WaitForFirstConsumer   true                   122d
```

### Internal Image Registry Configuration 

```
NAME                                               READY   STATUS      RESTARTS   AGE
cluster-image-registry-operator-6c9b8647c6-j668w   1/1     Running     0          117d
image-pruner-28067040-fmbgs                        0/1     Completed   0          2d2h
image-pruner-28068480-k5gr9                        0/1     Completed   0          26h
image-pruner-28069920-kqpg5                        0/1     Completed   0          162m
image-registry-6b9b7844bb-c5hfl                    1/1     Running     0          117d
image-registry-6b9b7844bb-psj7p                    1/1     Running     0          117d
node-ca-2c8pn                                      1/1     Running     3          124d
node-ca-4bgcz                                      1/1     Running     4          124d
node-ca-hwzj6                                      1/1     Running     3          124d
node-ca-lzmpt                                      1/1     Running     4          124d
node-ca-rhqjb                                      1/1     Running     4          124d
node-ca-s7qbd                                      1/1     Running     4          124d
node-ca-tsl58                                      1/1     Running     4          124d
node-ca-wbpvh                                      1/1     Running     3          124d
node-ca-z7hsp                                      1/1     Running     3          124d
node-ca-ztk9z                                      1/1     Running     4          124d

NAME                 STATUS   VOLUME                  CAPACITY   ACCESS MODES   STORAGECLASS      AGE
image-registry-pvc   Bound    image-registry-volume   500Gi      RWX            nfs-non-dynamic   119d
```

<span style="color:red"> **Recommendation:** </span>
- Use VMware or any third party CSI for registry storage instead of nfs-provisioner for support compatibility and performance.

## Cluster Security Configuration

