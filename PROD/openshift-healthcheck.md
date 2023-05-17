
# Accelya - PROD OpenShift Cluster Health Check Documentation

- [Accelya - PROD OpenShift Cluster Health Check](#accelya---prod-openshift-cluster-health-check-documentation)
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

- **Cluster API Address**: https://api.nfeocpprod.accelya.local:6443
- **Infrastructure provide**: VSphere
- **OpenShift Version**: 4.9.28 (Stable 4.9) -> **Kubernetes Versoion**: v1.22.5+a36406b
- **Cluster Nodes**: 10 (3 Master, 4 Worker, 3 Infra)
- **Cluster Projects**: 132
- **Cluster Monitoring, Logging, Security and Backup tools**:
    - Monitoring: OpenShift Monitoring (Default)
    - Logging: ElasticSearch
    - Security: SentielOne & Compliance Operator
    - Backup: None

## Cluster Inventory

### Cluster Nodes

**Total no. of ndoes**: 10

|Node Type|Nodes|CPU|Memory|Disks|
|---|---|---|---|---|
|Master|vlnfeprodmaster1.nfeocpprod.cluster.adp|8 Cores| 32 GB|250GB|
|Master|vlnfeprodmaster2.nfeocpprod.cluster.adp|8 Cores| 32 GB|250GB|
|Master|vlnfeprodmaster3.nfeocpprod.cluster.adp|8 Cores| 32 GB|250GB|
|Infra|vlnfeprodinfra1.nfeocpprod.cluster.adp|8 Cores| 64 GB|250GB, 1.1TB, 500GB|
|Infra|vlnfeprodinfra2.nfeocpprod.cluster.adp|8 Cores| 64 GB|250GB, 1.1TB|
|Infra|vlnfeprodinfra3.nfeocpprod.cluster.adp|8 Cores| 64 GB|250GB, 1.1TB, 500GB|
|Worker|vlnfeprodnode1.nfeocpprod.cluster.adp|12 Cores| 51 GB|250GB, 300GB|
|Worker|vlnfeprodnode2.nfeocpprod.cluster.adp|12 Cores| 51 GB|250GB, 300GB|
|Worker|vlnfeprodnode3.nfeocpprod.cluster.adp|12 Cores| 51 GB|250GB, 50GB, 50GB|
|Worker|vlnfeprodnode4.nfeocpprod.cluster.adp|12 Cores| 51 GB|250GB|

```
NAME                                  STATUS   ROLES    AGE    VERSION
NAME                                      STATUS   ROLES    AGE    VERSION
vlnfeprodinfra1.nfeocpprod.cluster.adp    Ready    infra    264d   v1.22.5+a36406b
vlnfeprodinfra2.nfeocpprod.cluster.adp    Ready    infra    264d   v1.22.5+a36406b
vlnfeprodinfra3.nfeocpprod.cluster.adp    Ready    infra    264d   v1.22.5+a36406b
vlnfeprodmaster1.nfeocpprod.cluster.adp   Ready    master   264d   v1.22.5+a36406b
vlnfeprodmaster2.nfeocpprod.cluster.adp   Ready    master   264d   v1.22.5+a36406b
vlnfeprodmaster3.nfeocpprod.cluster.adp   Ready    master   264d   v1.22.5+a36406b
vlnfeprodnode1.nfeocpprod.cluster.adp     Ready    worker   264d   v1.22.5+a36406b
vlnfeprodnode2.nfeocpprod.cluster.adp     Ready    worker   264d   v1.22.5+a36406b
vlnfeprodnode3.nfeocpprod.cluster.adp     Ready    worker   264d   v1.22.5+a36406b
vlnfeprodnode4.nfeocpprod.cluster.adp     Ready    worker   79d    v1.22.5+a36406b
```

### Cluster Projects (Namespaces)

**Total no. of Projects**: 132

|System Projects|User Projects|Comment|
|---|---|---|
| openshift                                        | advanced-payment-management       |   |
| openshift-apiserver                              | agent-management                  |   |
| openshift-apiserver-operator                     | airline-management                |   |
| openshift-authentication                         | app-deploy-on-service-mesh        |   |
| openshift-authentication-operator                | bsp-management                    |   |
| openshift-cloud-controller-manager               | cassandra-exporter                |   |
| openshift-cloud-controller-manager-operator      | cdc-replication-job               |   |
| openshift-cloud-credential-operator              | cicd                              |   |
| openshift-cluster-csi-drivers                    | cicd-test                         |   |
| openshift-cluster-machine-approver               | csi-driver-smb                    |   |
| openshift-cluster-node-tuning-operator           | currency-management               |   |
| openshift-cluster-samples-operator               | database                          |   |
| openshift-cluster-storage-operator               | dmz                               |   |
| openshift-cluster-version                        | document-enquiry                  |   |
| openshift-compliance                             | frontend                          |   |
| openshift-config                                 | gateway                           |   |
| openshift-config-managed                         | gds-management                    |   |
| openshift-config-operator                        | globalsearch                      |   |
| openshift-console                                | grafana                           |   |
| openshift-console-operator                       | grafana-waps-monitoring           |   |
| openshift-console-user-settings                  | hot-load-document-transformer     |   |
| openshift-controller-manager                     | hot-load-evaluation-processor     |   |
| openshift-controller-manager-operator            | hot-load-file-processor           |   |
| openshift-distributed-tracing                    | hot-load-file-scheduler           |   |
| openshift-dns                                    | informix-cdc                      |   |
| openshift-dns-operator                           | internal                          |   |
| openshift-etcd                                   | istio-system                      |   |
| openshift-etcd-operator                          | kong                              |   |
| openshift-file-integrity                         | management                        |   |
| openshift-host-network                           | monitorin-grafana-waps            |   |
| openshift-image-registry                         | period-management                 |   |
| openshift-infra                                  | postgres-exporter                 |   |
| openshift-ingress                                | postgresql                        |   |
| openshift-ingress-canary                         | qualys                            |   |
| openshift-ingress-operator                       | rabbitmq                          |   |
| openshift-insights                               | redis                             |   |
| openshift-kni-infra                              | rejected-documents-file-processor |   |
| openshift-kube-apiserver                         | rejected-documents-file-scheduler |   |
| openshift-kube-apiserver-operator                | rejected-documents-management     |   |
| openshift-kube-controller-manager                | sales-query                       |   |
| openshift-kube-controller-manager-operator       | sales-query-processor             |   |
| openshift-kube-scheduler                         | sentinelone                       |   |
| openshift-kube-scheduler-operator                | servicemesh-test-1                |   |
| openshift-kube-storage-version-migrator          | servicemesh-test-2                |   |
| openshift-kube-storage-version-migrator-operator | synchronizer                      |   |
| openshift-kubevirt-infra                         | test                              |   |
| openshift-local-storage                          | test-deploy                       |   |
| openshift-logging                                | test-qa                           |   |
| openshift-machine-api                            | test-registry                     |   |
| openshift-machine-config-operator                | test-shg1 - test_shg1             |   |
| openshift-marketplace                            | testporjectkt                     |   |
| openshift-monitoring                             | user-feedback                     |   |
| openshift-multus                                 | user-management-integration       |   |
| openshift-must-gather-9zvdl                      | waps-monitoring                   |   |
| openshift-must-gather-cj5bz                      | zookeeper                         |   |
| openshift-must-gather-gjkp8                      |                                   |   |
| openshift-network-diagnostics                    |                                   |   |
| openshift-network-operator                       |                                   |   |
| openshift-node                                   |                                   |   |
| openshift-oauth-apiserver                        |                                   |   |
| openshift-openstack-infra                        |                                   |   |
| openshift-operator-lifecycle-manager             |                                   |   |
| openshift-operators                              |                                   |   |
| openshift-operators-redhat                       |                                   |   |
| openshift-ovirt-infra                            |                                   |   |
| openshift-sdn                                    |                                   |   |
| openshift-service-ca                             |                                   |   |
| openshift-service-ca-operator                    |                                   |   |
| openshift-user-workload-monitoring               |                                   |   |
| openshift-vsphere-infra                          |                                   |   |
| default                                          |                                   |   |
| kube-node-lease                                  |                                   |   |
| kube-public                                      |                                   |   |
| kube-system                                      |                                   |   |

<span style="color:red"> **Recommendation:** </span>
- Some of of the Infra related components Pods are running on worker nodes. Please use proper labeling, taints and tolerations to schedule Infra Pods on Infra Nodes to save OpenShift licensing cost.

### Cluster Resource Quotas and Limit Ranges

- Resource Quotas only defined for `openshift-host-network (default)` namespace. 

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

- ETCD encrytion is enabled and below OpenShift API server and Kubernetes API server resources are encrypted:
  - Secrets
  - Configmaps
  - Routes
  - OAuth Access Tokens
  - OAuth Authorize Tokens

```
EncryptionCompleted
All resources encrypted: routes.route.openshift.io
All resources encrypted: secrets, configmaps
All resources encrypted: oauthaccesstokens.oauth.openshift.io, oauthauthorizetokens.oauth.openshift.io
```

<span style="color:red"> **Recommendation:** </span>
- When you enable etcd encryption, encryption keys are created. These keys are rotated on a weekly basis. You must have these keys to restore from an etcd backup.
- Please make sure to take a backup of latest encryptions keys every week.

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
openshift-ingress-operator   default   383d
```

<span style="color:green"> **Recommendation:** </span>
- Create additional sharded Ingress Controller on cluster, which allows 
    - To use custom TLS certificates for Applications other than default `*.apps` certificate
    - Customization of endpoint URLs for routes 


## Cluster Storage Configuration

### Cluster CSI Nodes

```
NAME                                      DRIVERS   AGE
vlnfeprodinfra1.nfeocpprod.cluster.adp    1         264d
vlnfeprodinfra2.nfeocpprod.cluster.adp    1         264d
vlnfeprodinfra3.nfeocpprod.cluster.adp    1         264d
vlnfeprodmaster1.nfeocpprod.cluster.adp   1         264d
vlnfeprodmaster2.nfeocpprod.cluster.adp   1         264d
vlnfeprodmaster3.nfeocpprod.cluster.adp   1         264d
vlnfeprodnode1.nfeocpprod.cluster.adp     1         264d
vlnfeprodnode2.nfeocpprod.cluster.adp     1         264d
vlnfeprodnode3.nfeocpprod.cluster.adp     1         264d
vlnfeprodnode4.nfeocpprod.cluster.adp     1         79d
```

<span style="color:green"> **Recommendation:** </span>
-  Leverage equal no. of volumes and similar sizes across all CSI nodes. 

### Storage Classes

```
NAME             PROVISIONER                    RECLAIMPOLICY   VOLUMEBINDINGMODE   ALLOWVOLUMEEXPANSION   AGE
localblock-sc    no-provisioning                Retain          Immediate           true                   365d
thin (default)   kubernetes.io/vsphere-volume   Delete          Immediate           false                  383d
thin-retain      kubernetes.io/vsphere-volume   Retain          Immediate           false                  378d
vsphere-sc       kubernetes.io/vsphere-volume   Delete          Immediate           false                  265d
```

### Internal Image Registry Configuration 

```
NAME                                               READY   STATUS      RESTARTS   AGE
cluster-image-registry-operator-84c659fcbf-dgdgj   1/1     Running     0          12d
image-pruner-28068480--1-njxwz                     0/1     Completed   0          2d16h
image-pruner-28069920--1-v584j                     0/1     Completed   0          40h
image-pruner-28071360--1-xwlrs                     0/1     Completed   0          16h
image-registry-54f497dc6d-lqgd4                    1/1     Running     0          12d
node-ca-4l4mt                                      1/1     Running     7          265d
node-ca-4sfp4                                      1/1     Running     7          265d
node-ca-bb822                                      1/1     Running     9          264d
node-ca-btfwr                                      1/1     Running     10         265d
node-ca-d2h57                                      1/1     Running     7          265d
node-ca-dm4s4                                      1/1     Running     7          265d
node-ca-k4z9t                                      1/1     Running     7          265d
node-ca-pv9gm                                      1/1     Running     12         265d
node-ca-r5cmq                                      1/1     Running     1          79d
node-ca-rrfsl                                      1/1     Running     7          265d

NAME             STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
image-registry   Bound    pvc-56bf64a9-e831-4ea7-b311-f4167af51cb6   400Gi      RWO            thin-retain    264d
```

<span style="color:red"> **Recommendation:** </span>
- image registry PVC is configured under VMware `thin-retain` storage class. Currently it is in `RWO` access modes. For Production setup, it should be in `RWX` access modes.

## Cluster Security Configuration

### Default Ingress and API Certificates

- Default Ingress and API Certificates are not currently configured
- All cluster traffice for `*.apps` and `API` endpoints will be in plain text 

**Default Ingress config**
```yaml
apiVersion: operator.openshift.io/v1
kind: IngressController
metadata:
  creationTimestamp: "2023-01-11T09:11:54Z"
  finalizers:
  - ingresscontroller.operator.openshift.io/finalizer-ingresscontroller
  generation: 2
  name: default
  namespace: openshift-ingress-operator
  resourceVersion: "105780535"
  uid: c353570c-d452-422d-8e12-bd1ca5869d4d
spec:
  clientTLS:
    clientCA:
      name: ""
    clientCertificatePolicy: ""
  httpCompression: {}
  httpEmptyRequestsPolicy: Respond
  httpErrorCodePages:
    name: ""
  nodePlacement:
    nodeSelector:
      matchLabels:
        node-role.kubernetes.io/infra: ""
  replicas: 3
  tuningOptions: {}
  unsupportedConfigOverrides: null
```

**API Server config**
```yaml
apiVersion: config.openshift.io/v1
kind: APIServer
metadata:
  annotations:
    include.release.openshift.io/ibm-cloud-managed: "true"
    include.release.openshift.io/self-managed-high-availability: "true"
    include.release.openshift.io/single-node-developer: "true"
    oauth-apiserver.openshift.io/secure-token-storage: "true"
    release.openshift.io/create-only: "true"
  creationTimestamp: "2023-01-11T08:59:32Z"
  generation: 2
  name: cluster
  ownerReferences:
  - apiVersion: config.openshift.io/v1
    kind: ClusterVersion
    name: version
    uid: c913b03c-acbd-4af8-86f9-3a2468748bbc
  resourceVersion: "4721113"
  uid: 9dfa3cc7-1201-4325-9445-72620adb2aff
spec:
  audit:
    profile: Default
  encryption:
    type: aescbc
```

<span style="color:red"> **Recommendation:** </span>
- Generate two separate SSL certificates as per below and secure `*.apps` and `API` endpoint using those certificates.
  - one wild card certificate for *.apps.<cluster-name>.<base-domain> with `subjectAltName`.
  - certificate for `api.<cluster-name>.<base-domina> with `subjectAltName`.

### Identity Providers Configuration

- `htpasswd` and `LDAP` identity providers are configured for cluster and working as expected. 

<span style="color:green"> **Recommendation:** </span>


### Cluster Users, Groups, Roles and Permissions

- Cluster Users authentication and authorization are configured using `htpasswd` and `LDAP` IDP with appropriate permissions for required users. 
- Proper OpenShift roles `cluster-admin, admin, view, edit` are being used for Users and ServiceAccounts permissions.  

## OpenShift Cluster Upgrade

- OpenShift Cluster version: 4.11.20
- OpenShift Cluster 4.11.x full support ended on April 17,2023 and currently it's in Maintenance support phase till Feb 10, 2024. 
- Please upgrade this cluster to 4.12.x within 6 months. 
// add picture
