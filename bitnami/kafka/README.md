# Kafka

[Kafka](https://kafka.apache.org/) is a distributed streaming platform used for building real-time data pipelines and streaming apps. It is horizontally scalable, fault-tolerant, wicked fast, and runs in production in thousands of companies.

## TL;DR

```console
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-release bitnami/kafka
```

## Introduction

This chart bootstraps a [Kafka](https://github.com/bitnami/bitnami-docker-kafka) deployment on a [Kubernetes](http://kubernetes.io) cluster using the [Helm](https://helm.sh) package manager.

Bitnami charts can be used with [Kubeapps](https://kubeapps.com/) for deployment and management of Helm Charts in clusters. This Helm chart has been tested on top of [Bitnami Kubernetes Production Runtime](https://kubeprod.io/) (BKPR). Deploy BKPR to get automated TLS certificates, logging and monitoring for your applications.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.1.0
- PV provisioner support in the underlying infrastructure

## Installing the Chart

To install the chart with the release name `my-release`:

```console
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-release bitnami/kafka
```

These commands deploy Kafka on the Kubernetes cluster in the default configuration. The [Parameters](#parameters) section lists the parameters that can be configured during installation.

> **Tip**: List all releases using `helm list`

## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete my-release
```

The command removes all the Kubernetes components associated with the chart and deletes the release.

## Parameters

### Global parameters

| Name                      | Description                                     | Value |
| ------------------------- | ----------------------------------------------- | ----- |
| `global.imageRegistry`    | Global Docker image registry                    | `""`  |
| `global.imagePullSecrets` | Global Docker registry secret names as an array | `[]`  |
| `global.storageClass`     | Global StorageClass for Persistent Volume(s)    | `""`  |


### Common parameters

| Name                     | Description                                                                             | Value           |
| ------------------------ | --------------------------------------------------------------------------------------- | --------------- |
| `nameOverride`           | String to partially override kafka.fullname                                             | `""`            |
| `fullnameOverride`       | String to fully override kafka.fullname                                                 | `""`            |
| `clusterDomain`          | Default Kubernetes cluster domain                                                       | `cluster.local` |
| `commonLabels`           | Labels to add to all deployed objects                                                   | `{}`            |
| `commonAnnotations`      | Annotations to add to all deployed objects                                              | `{}`            |
| `extraDeploy`            | Array of extra objects to deploy with the release                                       | `[]`            |
| `diagnosticMode.enabled` | Enable diagnostic mode (all probes will be disabled and the command will be overridden) | `false`         |
| `diagnosticMode.command` | Command to override all containers in the deployment                                    | `["sleep"]`     |
| `diagnosticMode.args`    | Args to override all containers in the deployment                                       | `["infinity"]`  |


### Kafka parameters

| Name                                       | Description                                                                                                                                          | Value                               |
| ------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| `image.registry`                           | Kafka image registry                                                                                                                                 | `docker.io`                         |
| `image.repository`                         | Kafka image repository                                                                                                                               | `bitnami/kafka`                     |
| `image.tag`                                | Kafka image tag (immutable tags are recommended)                                                                                                     | `2.8.1-debian-10-r0`                |
| `image.pullPolicy`                         | Kafka image pull policy                                                                                                                              | `IfNotPresent`                      |
| `image.pullSecrets`                        | Specify docker-registry secret names as an array                                                                                                     | `[]`                                |
| `image.debug`                              | Set to true if you would like to see extra information on logs                                                                                       | `false`                             |
| `config`                                   | Configuration file for Kafka. Auto-generated based on other parameters when not specified (see [below](                                              | `""`                                |
| `existingConfigmap`                        | ConfigMap with Kafka Configuration                                                                                                                   | `""`                                |
| `log4j`                                    | An optional log4j.properties file to overwrite the default of the Kafka brokers.                                                                     | `""`                                |
| `existingLog4jConfigMap`                   | The name of an existing ConfigMap containing a log4j.properties file.                                                                                | `""`                                |
| `heapOpts`                                 | Kafka's Java Heap size                                                                                                                               | `-Xmx1024m -Xms1024m`               |
| `deleteTopicEnable`                        | Switch to enable topic deletion or not                                                                                                               | `false`                             |
| `autoCreateTopicsEnable`                   | Switch to enable auto creation of topics. Enabling auto creation of topics not recommended for production or similar environments                    | `true`                              |
| `logFlushIntervalMessages`                 | The number of messages to accept before forcing a flush of data to disk                                                                              | `_10000`                            |
| `logFlushIntervalMs`                       | The maximum amount of time a message can sit in a log before we force a flush                                                                        | `1000`                              |
| `logRetentionBytes`                        | A size-based retention policy for logs                                                                                                               | `_1073741824`                       |
| `logRetentionCheckIntervalMs`              | The interval at which log segments are checked to see if they can be deleted                                                                         | `300000`                            |
| `logRetentionHours`                        | The minimum age of a log file to be eligible for deletion due to age                                                                                 | `168`                               |
| `logSegmentBytes`                          | The maximum size of a log segment file. When this size is reached a new log segment will be created                                                  | `_1073741824`                       |
| `logsDirs`                                 | A comma separated list of directories under which to store log files                                                                                 | `/bitnami/kafka/data`               |
| `maxMessageBytes`                          | The largest record batch size allowed by Kafka                                                                                                       | `_1000012`                          |
| `defaultReplicationFactor`                 | Default replication factors for automatically created topics                                                                                         | `1`                                 |
| `offsetsTopicReplicationFactor`            | The replication factor for the offsets topic                                                                                                         | `1`                                 |
| `transactionStateLogReplicationFactor`     | The replication factor for the transaction topic                                                                                                     | `1`                                 |
| `transactionStateLogMinIsr`                | Overridden min.insync.replicas config for the transaction topic                                                                                      | `1`                                 |
| `numIoThreads`                             | The number of threads doing disk I/O                                                                                                                 | `8`                                 |
| `numNetworkThreads`                        | The number of threads handling network requests                                                                                                      | `3`                                 |
| `numPartitions`                            | The default number of log partitions per topic                                                                                                       | `1`                                 |
| `numRecoveryThreadsPerDataDir`             | The number of threads per data directory to be used for log recovery at startup and flushing at shutdown                                             | `1`                                 |
| `socketReceiveBufferBytes`                 | The receive buffer (SO_RCVBUF) used by the socket server                                                                                             | `102400`                            |
| `socketRequestMaxBytes`                    | The maximum size of a request that the socket server will accept (protection against OOM)                                                            | `_104857600`                        |
| `socketSendBufferBytes`                    | The send buffer (SO_SNDBUF) used by the socket server                                                                                                | `102400`                            |
| `zookeeperConnectionTimeoutMs`             | Timeout in ms for connecting to Zookeeper                                                                                                            | `6000`                              |
| `authorizerClassName`                      | The Authorizer is configured by setting authorizer.class.name=kafka.security.authorizer.AclAuthorizer in server.properties.                          | `""`                                |
| `allowEveryoneIfNoAclFound`                | By default, if a resource has no associated ACLs, then no one is allowed to access that resource except super users.                                 | `true`                              |
| `superUsers`                               | You can add super users in server.properties                                                                                                         | `User:admin`                        |
| `command`                                  | Override kafka container command                                                                                                                     | `["/scripts/setup.sh"]`             |
| `args`                                     | Override kafka container arguments                                                                                                                   | `[]`                                |
| `extraEnvVars`                             | Extra environment variables to add to kafka pods (see [below]({KEY}                                                                                  | `[]`                                |
| `extraVolumes`                             | Extra volume(s) to add to Kafka statefulset                                                                                                          | `[]`                                |
| `extraVolumeMounts`                        | Extra volumeMount(s) to add to Kafka containers                                                                                                      | `[]`                                |
| `auth.clientProtocol`                      | Authentication protocol for communications with clients. Allowed protocols: `plaintext`, `tls`, `mtls`, `sasl` and `sasl_tls`                        | `plaintext`                         |
| `auth.interBrokerProtocol`                 | Authentication protocol for inter-broker communications. Allowed protocols: `plaintext`, `tls`, `mtls`, `sasl` and `sasl_tls`                        | `plaintext`                         |
| `auth.sasl.mechanisms`                     | SASL mechanisms when either `auth.interBrokerProtocol` or `auth.clientProtocol` are `sasl`. Allowed types: `plain`, `scram-sha-256`, `scram-sha-512` | `plain,scram-sha-256,scram-sha-512` |
| `auth.sasl.interBrokerMechanism`           | SASL mechanism for inter broker communication.                                                                                                       | `plain`                             |
| `auth.sasl.jaas.clientUsers`               | Kafka client user list                                                                                                                               | `["user"]`                          |
| `auth.sasl.jaas.clientPasswords`           | Kafka client passwords. This is mandatory if more than one user is specified in clientUsers                                                          | `[]`                                |
| `auth.sasl.jaas.interBrokerUser`           | Kafka inter broker communication user for SASL authentication                                                                                        | `admin`                             |
| `auth.sasl.jaas.interBrokerPassword`       | Kafka inter broker communication password for SASL authentication                                                                                    | `""`                                |
| `auth.sasl.jaas.zookeeperUser`             | Kafka Zookeeper user for SASL authentication                                                                                                         | `""`                                |
| `auth.sasl.jaas.zookeeperPassword`         | Kafka Zookeeper password for SASL authentication                                                                                                     | `""`                                |
| `auth.sasl.jaas.existingSecret`            | Name of the existing secret containing credentials for clientUsers, interBrokerUser and zookeeperUser                                                | `""`                                |
| `auth.saslMechanisms`                      | DEPRECATED: use `auth.sasl.mechanisms` instead.                                                                                                      | `plain,scram-sha-256,scram-sha-512` |
| `auth.saslInterBrokerMechanism`            | DEPRECATED: use `auth.sasl.interBrokerMechanism` instead.                                                                                            | `plain`                             |
| `auth.jaas`                                | DEPRECATED: use `auth.sasl.jaas` instead.                                                                                                            | `{}`                                |
| `auth.tls.type`                            | Format to use for TLS certificates. Allowed types: `jks` and `pem`                                                                                   | `jks`                               |
| `auth.tls.existingSecret`                  | Name of the existing secret containing the TLS certificates for the Kafka brokers                                                                    | `""`                                |
| `auth.tls.autoGenerated`                   | Generate automatically self-signed TLS certificates for Kafka brokers. Currently only supported if `auth.tls.type` is `pem`                          | `false`                             |
| `auth.tls.password`                        | Password to access the JKS files or PEM key when they are password-protected.                                                                        | `""`                                |
| `auth.tls.jksTruststoreSecret`             | Name of the existing secret containing your truststore if truststore not existing or different from the one in the `auth.tls.existingSecret`         | `""`                                |
| `auth.tls.jksKeystoreSAN`                  | The secret key from the `auth.tls.existingSecret` containing the keystore with a SAN certificate                                                     | `""`                                |
| `auth.tls.jksTruststore`                   | The secret key from the `auth.tls.existingSecret` or `auth.tls.jksTruststoreSecret` containing the truststore                                        | `""`                                |
| `auth.tls.endpointIdentificationAlgorithm` | The endpoint identification algorithm to validate server hostname using server certificate                                                           | `https`                             |
| `auth.jksSecret`                           | DEPRECATED: use `auth.tls.existingSecret` instead.                                                                                                   | `""`                                |
| `auth.jksTruststoreSecret`                 | DEPRECATED: use `auth.tls.jksTruststoreSecret` instead.                                                                                              | `""`                                |
| `auth.jksKeystoreSAN`                      | DEPRECATED: use `auth.tls.jksKeystoreSAN` instead.                                                                                                   | `""`                                |
| `auth.jksTruststore`                       | DEPRECATED: use `auth.tls.jksTruststore` instead.                                                                                                    | `""`                                |
| `auth.jksPassword`                         | DEPRECATED: use `auth.tls.password` instead.                                                                                                         | `""`                                |
| `auth.tlsEndpointIdentificationAlgorithm`  | DEPRECATED: use `auth.tls.endpointIdentificationAlgorithm` instead.                                                                                  | `https`                             |
| `listeners`                                | The address(es) the socket server listens on. Auto-calculated it's set to an empty array                                                             | `[]`                                |
| `advertisedListeners`                      | The address(es) (hostname:port) the broker will advertise to producers and consumers. Auto-calculated it's set to an empty array                     | `[]`                                |
| `listenerSecurityProtocolMap`              | The protocol->listener mapping. Auto-calculated it's set to nil                                                                                      | `""`                                |
| `allowPlaintextListener`                   | Allow to use the PLAINTEXT listener                                                                                                                  | `true`                              |
| `interBrokerListenerName`                  | The listener that the brokers should communicate on                                                                                                  | `INTERNAL`                          |


### Statefulset parameters

| Name                                 | Description                                                                                                                                                                                   | Value           |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| `replicaCount`                       | Number of Kafka nodes                                                                                                                                                                         | `1`             |
| `minBrokerId`                        | Minimal broker.id value, nodes increment their `broker.id` respectively                                                                                                                       | `0`             |
| `updateStrategy`                     | Update strategy for the stateful set                                                                                                                                                          | `RollingUpdate` |
| `rollingUpdatePartition`             | Partition update strategy                                                                                                                                                                     | `""`            |
| `hostAliases`                        | Add deployment host aliases                                                                                                                                                                   | `[]`            |
| `podManagementPolicy`                | StatefulSet controller supports relax its ordering guarantees while preserving its uniqueness and identity guarantees. There are two valid pod management policies: OrderedReady and Parallel | `Parallel`      |
| `schedulerName`                      | Name of the k8s scheduler (other than default)                                                                                                                                                | `""`            |
| `podLabels`                          | Kafka pod labels                                                                                                                                                                              | `{}`            |
| `podAnnotations`                     | Kafka Pod annotations                                                                                                                                                                         | `{}`            |
| `priorityClassName`                  | Name of the existing priority class to be used by kafka pods                                                                                                                                  | `""`            |
| `podAffinityPreset`                  | Pod affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                                                                                           | `""`            |
| `podAntiAffinityPreset`              | Pod anti-affinity preset. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                                                                                      | `soft`          |
| `nodeAffinityPreset.type`            | Node affinity preset type. Ignored if `affinity` is set. Allowed values: `soft` or `hard`                                                                                                     | `""`            |
| `nodeAffinityPreset.key`             | Node label key to match Ignored if `affinity` is set.                                                                                                                                         | `""`            |
| `nodeAffinityPreset.values`          | Node label values to match. Ignored if `affinity` is set.                                                                                                                                     | `[]`            |
| `affinity`                           | Affinity for pod assignment                                                                                                                                                                   | `{}`            |
| `nodeSelector`                       | Node labels for pod assignment                                                                                                                                                                | `{}`            |
| `tolerations`                        | Tolerations for pod assignment                                                                                                                                                                | `[]`            |
| `topologySpreadConstraints`          | Topology Spread Constraints for pod assignment spread across your cluster among failure-domains. Evaluated as a template                                                                      | `{}`            |
| `terminationGracePeriodSeconds`      | Seconds the pod needs to gracefully terminate                                                                                                                                                 | `""`            |
| `podSecurityContext.enabled`         | Enable security context for the pods                                                                                                                                                          | `true`          |
| `podSecurityContext.fsGroup`         | Group ID for the filesystem used by the containers                                                                                                                                            | `1001`          |
| `podSecurityContext.runAsUser`       | User ID for the service user running the pod                                                                                                                                                  | `1001`          |
| `containerSecurityContext`           | Kafka containers' Security Context                                                                                                                                                            | `{}`            |
| `resources.limits`                   | The resources limits for Kafka containers                                                                                                                                                     | `{}`            |
| `resources.requests`                 | The requested resources for Kafka containers                                                                                                                                                  | `{}`            |
| `livenessProbe.enabled`              | Enable livenessProbe                                                                                                                                                                          | `true`          |
| `livenessProbe.initialDelaySeconds`  | Initial delay seconds for livenessProbe                                                                                                                                                       | `10`            |
| `livenessProbe.periodSeconds`        | Period seconds for livenessProbe                                                                                                                                                              | `10`            |
| `livenessProbe.timeoutSeconds`       | Timeout seconds for livenessProbe                                                                                                                                                             | `5`             |
| `livenessProbe.failureThreshold`     | Failure threshold for livenessProbe                                                                                                                                                           | `3`             |
| `livenessProbe.successThreshold`     | Success threshold for livenessProbe                                                                                                                                                           | `1`             |
| `readinessProbe.enabled`             | Enable readinessProbe                                                                                                                                                                         | `true`          |
| `readinessProbe.initialDelaySeconds` | Initial delay seconds for readinessProbe                                                                                                                                                      | `5`             |
| `readinessProbe.periodSeconds`       | Period seconds for readinessProbe                                                                                                                                                             | `10`            |
| `readinessProbe.timeoutSeconds`      | Timeout seconds for readinessProbe                                                                                                                                                            | `5`             |
| `readinessProbe.failureThreshold`    | Failure threshold for readinessProbe                                                                                                                                                          | `6`             |
| `readinessProbe.successThreshold`    | Success threshold for readinessProbe                                                                                                                                                          | `1`             |
| `customLivenessProbe`                | Custom Liveness probe configuration for Kafka                                                                                                                                                 | `{}`            |
| `customReadinessProbe`               | Custom Readiness probe configuration for Kafka                                                                                                                                                | `{}`            |
| `pdb.create`                         | Enable/disable a Pod Disruption Budget creation                                                                                                                                               | `false`         |
| `pdb.minAvailable`                   | Minimum number/percentage of pods that should remain scheduled                                                                                                                                | `""`            |
| `pdb.maxUnavailable`                 | Maximum number/percentage of pods that may be made unavailable                                                                                                                                | `1`             |
| `sidecars`                           | Attach additional sidecar containers to the Kafka pod                                                                                                                                         | `[]`            |
| `initContainers`                     | Add extra init containers                                                                                                                                                                     | `[]`            |


### Exposure parameters

| Name                                              | Description                                                                                   | Value                  |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------- | ---------------------- |
| `service.type`                                    | Kubernetes Service type                                                                       | `ClusterIP`            |
| `service.port`                                    | Kafka port for client connections                                                             | `9092`                 |
| `service.internalPort`                            | Kafka port for inter-broker connections                                                       | `9093`                 |
| `service.externalPort`                            | Kafka port for external connections                                                           | `9094`                 |
| `service.nodePorts`                               | Specify the nodePort value for the LoadBalancer and NodePort service types.                   | `{}`                   |
| `service.loadBalancerIP`                          | loadBalancerIP for Kafka Service                                                              | `""`                   |
| `service.loadBalancerSourceRanges`                | Address(es) that are allowed when service is LoadBalancer                                     | `[]`                   |
| `service.annotations`                             | Service annotations                                                                           | `{}`                   |
| `externalAccess.enabled`                          | Enable Kubernetes external cluster access to Kafka brokers                                    | `false`                |
| `externalAccess.autoDiscovery.enabled`            | Enable using an init container to auto-detect external IPs/ports by querying the K8s API      | `false`                |
| `externalAccess.autoDiscovery.image.registry`     | Init container auto-discovery image registry                                                  | `docker.io`            |
| `externalAccess.autoDiscovery.image.repository`   | Init container auto-discovery image repository                                                | `bitnami/kubectl`      |
| `externalAccess.autoDiscovery.image.tag`          | Init container auto-discovery image tag (immutable tags are recommended)                      | `1.19.15-debian-10-r3` |
| `externalAccess.autoDiscovery.image.pullPolicy`   | Init container auto-discovery image pull policy                                               | `IfNotPresent`         |
| `externalAccess.autoDiscovery.image.pullSecrets`  | Init container auto-discovery image pull secrets                                              | `[]`                   |
| `externalAccess.autoDiscovery.resources.limits`   | Init container auto-discovery resource limits                                                 | `{}`                   |
| `externalAccess.autoDiscovery.resources.requests` | Init container auto-discovery resource requests                                               | `{}`                   |
| `externalAccess.service.type`                     | Kubernetes Service type for external access. It can be NodePort or LoadBalancer               | `LoadBalancer`         |
| `externalAccess.service.port`                     | Kafka port used for external access when service type is LoadBalancer                         | `9094`                 |
| `externalAccess.service.loadBalancerIPs`          | Array of load balancer IPs for each Kafka broker. Length must be the same as replicaCount     | `[]`                   |
| `externalAccess.service.loadBalancerSourceRanges` | Address(es) that are allowed when service is LoadBalancer                                     | `[]`                   |
| `externalAccess.service.nodePorts`                | Array of node ports used for each Kafka broker. Length must be the same as replicaCount       | `[]`                   |
| `externalAccess.service.useHostIPs`               | Use service host IPs to configure Kafka external listener when service type is NodePort       | `false`                |
| `externalAccess.service.domain`                   | Domain or external ip used to configure Kafka external listener when service type is NodePort | `""`                   |
| `externalAccess.service.annotations`              | Service annotations for external access                                                       | `{}`                   |
| `externalAccess.service.usePodIPs`                | using the MY_POD_IP address for external access.                                              | `false`                |


### Persistence parameters

| Name                              | Description                                                                                                                              | Value                     |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `persistence.enabled`             | Enable Kafka data persistence using PVC, note that Zookeeper persistence is unaffected                                                   | `true`                    |
| `persistence.existingClaim`       | Provide an existing `PersistentVolumeClaim`, the value is evaluated as a template                                                        | `""`                      |
| `persistence.storageClass`        | PVC Storage Class for Kafka data volume                                                                                                  | `""`                      |
| `persistence.accessModes`         | PV Access Mode                                                                                                                           | `["ReadWriteOnce"]`       |
| `persistence.size`                | PVC Storage Request for Kafka data volume                                                                                                | `8Gi`                     |
| `persistence.annotations`         | Annotations for the PVC                                                                                                                  | `{}`                      |
| `persistence.selector`            | Selector to match an existing Persistent Volume for Kafka's data PVC. If set, the PVC can't have a PV dynamically provisioned for it     | `{}`                      |
| `persistence.mountPath`           | Mount path of the Kafka data volume                                                                                                      | `/bitnami/kafka`          |
| `logPersistence.enabled`          | Enable Kafka logs persistence using PVC, note that Zookeeper persistence is unaffected                                                   | `false`                   |
| `logPersistence.existingClaim`    | A manually managed Persistent Volume and Claim                                                                                           | `""`                      |
| `logPersistence.existingLogClaim` | PV Storage Class                                                                                                                         | `""`                      |
| `logPersistence.accessModes`      | PV Access Mode                                                                                                                           | `["ReadWriteOnce"]`       |
| `logPersistence.size`             | PVC Storage Request for Kafka logs volume                                                                                                | `8Gi`                     |
| `logPersistence.annotations`      | Annotations for the PVC                                                                                                                  | `{}`                      |
| `logPersistence.selector`         | Selector to match an existing Persistent Volume for Kafka's log data PVC. If set, the PVC can't have a PV dynamically provisioned for it | `{}`                      |
| `logPersistence.mountPath`        | Mount path of the Kafka logs volume                                                                                                      | `/opt/bitnami/kafka/logs` |


### RBAC parameters

| Name                                          | Description                                                                                    | Value   |
| --------------------------------------------- | ---------------------------------------------------------------------------------------------- | ------- |
| `serviceAccount.create`                       | Enable creation of ServiceAccount for Kafka pods                                               | `true`  |
| `serviceAccount.name`                         | The name of the service account to use. If not set and `create` is `true`, a name is generated | `""`    |
| `serviceAccount.automountServiceAccountToken` | Allows auto mount of ServiceAccountToken on the serviceAccount created                         | `true`  |
| `rbac.create`                                 | Whether to create & use RBAC resources or not                                                  | `false` |


### Volume Permissions parameters

| Name                                          | Description                                                                                                          | Value                   |
| --------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | ----------------------- |
| `volumePermissions.enabled`                   | Enable init container that changes the owner and group of the persistent volume(s) mountpoint to `runAsUser:fsGroup` | `false`                 |
| `volumePermissions.securityContext.runAsUser` | User ID for the container                                                                                            | `0`                     |
| `volumePermissions.image.registry`            | Init container volume-permissions image registry                                                                     | `docker.io`             |
| `volumePermissions.image.repository`          | Init container volume-permissions image name                                                                         | `bitnami/bitnami-shell` |
| `volumePermissions.image.tag`                 | Init container volume-permissions image tag                                                                          | `10-debian-10-r199`     |
| `volumePermissions.image.pullPolicy`          | Init container volume-permissions image pull policy                                                                  | `Always`                |
| `volumePermissions.image.pullSecrets`         | Specify docker-registry secret names as an array                                                                     | `[]`                    |
| `volumePermissions.resources.limits`          | Init container volume-permissions resource  limits                                                                   | `{}`                    |
| `volumePermissions.resources.requests`        | Init container volume-permissions resource  requests                                                                 | `{}`                    |


### Metrics parameters

| Name                                             | Description                                                                                                                      | Value                                                                                   |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `metrics.kafka.enabled`                          | Whether or not to create a standalone Kafka exporter to expose Kafka metrics                                                     | `false`                                                                                 |
| `metrics.kafka.image.registry`                   | Kafka exporter image registry                                                                                                    | `docker.io`                                                                             |
| `metrics.kafka.image.repository`                 | Kafka exporter image repository                                                                                                  | `bitnami/kafka-exporter`                                                                |
| `metrics.kafka.image.tag`                        | Kafka exporter image tag (immutable tags are recommended)                                                                        | `1.4.2-debian-10-r5`                                                                    |
| `metrics.kafka.image.pullPolicy`                 | Kafka exporter image pull policy                                                                                                 | `IfNotPresent`                                                                          |
| `metrics.kafka.image.pullSecrets`                | Specify docker-registry secret names as an array                                                                                 | `[]`                                                                                    |
| `metrics.kafka.schedulerName`                    | Name of the k8s scheduler (other than default) for Kafka Exporter                                                                | `""`                                                                                    |
| `metrics.kafka.extraFlags`                       | Extra flags to be passed to Kafka exporter                                                                                       | `{}`                                                                                    |
| `metrics.kafka.certificatesSecret`               | Name of the existing secret containing the optional certificate and key files                                                    | `""`                                                                                    |
| `metrics.kafka.tlsCert`                          | The secret key from the certificatesSecret if 'client-cert' key different from the default (cert-file)                           | `cert-file`                                                                             |
| `metrics.kafka.tlsKey`                           | The secret key from the certificatesSecret if 'client-key' key different from the default (key-file)                             | `key-file`                                                                              |
| `metrics.kafka.tlsCaSecret`                      | Name of the existing secret containing the optional ca certificate for Kafka Exporter client authentication                      | `""`                                                                                    |
| `metrics.kafka.tlsCaCert`                        | The secret key from the certificatesSecret or tlsCaSecret if 'ca-cert' key different from the default (ca-file)                  | `ca-file`                                                                               |
| `metrics.kafka.resources.limits`                 | Kafka Exporter container resource limits                                                                                         | `{}`                                                                                    |
| `metrics.kafka.resources.requests`               | Kafka Exporter container resource requests                                                                                       | `{}`                                                                                    |
| `metrics.kafka.affinity`                         | Affinity for Kafka Exporter pod assignment                                                                                       | `{}`                                                                                    |
| `metrics.kafka.nodeSelector`                     | Node labels for Kafka Exporter pod assignment                                                                                    | `{}`                                                                                    |
| `metrics.kafka.tolerations`                      | Tolerations for Kafka Exporter pod assignment                                                                                    | `[]`                                                                                    |
| `metrics.kafka.initContainers`                   | Add init containers to the Kafka exporter pods                                                                                   | `[]`                                                                                    |
| `metrics.kafka.service.type`                     | Kubernetes service type (`ClusterIP`, `NodePort` or `LoadBalancer`) for Kafka Exporter                                           | `ClusterIP`                                                                             |
| `metrics.kafka.service.port`                     | Kafka Exporter Prometheus port                                                                                                   | `9308`                                                                                  |
| `metrics.kafka.service.nodePort`                 | Kubernetes HTTP node port                                                                                                        | `""`                                                                                    |
| `metrics.kafka.service.loadBalancerIP`           | loadBalancerIP if service type is `LoadBalancer`                                                                                 | `""`                                                                                    |
| `metrics.kafka.service.loadBalancerSourceRanges` | Load Balancer sources                                                                                                            | `[]`                                                                                    |
| `metrics.kafka.service.clusterIP`                | Static clusterIP or None for headless services                                                                                   | `""`                                                                                    |
| `metrics.kafka.service.annotations`              | Annotations for the Kafka Exporter Prometheus metrics service                                                                    | `{}`                                                                                    |
| `metrics.jmx.enabled`                            | Whether or not to expose JMX metrics to Prometheus                                                                               | `false`                                                                                 |
| `metrics.jmx.image.registry`                     | JMX exporter image registry                                                                                                      | `docker.io`                                                                             |
| `metrics.jmx.image.repository`                   | JMX exporter image repository                                                                                                    | `bitnami/jmx-exporter`                                                                  |
| `metrics.jmx.image.tag`                          | JMX exporter image tag (immutable tags are recommended)                                                                          | `0.16.1-debian-10-r66`                                                                  |
| `metrics.jmx.image.pullPolicy`                   | JMX exporter image pull policy                                                                                                   | `IfNotPresent`                                                                          |
| `metrics.jmx.image.pullSecrets`                  | Specify docker-registry secret names as an array                                                                                 | `[]`                                                                                    |
| `metrics.jmx.resources.limits`                   | JMX Exporter container resource limits                                                                                           | `{}`                                                                                    |
| `metrics.jmx.resources.requests`                 | JMX Exporter container resource requests                                                                                         | `{}`                                                                                    |
| `metrics.jmx.service.type`                       | Kubernetes service type (`ClusterIP`, `NodePort` or `LoadBalancer`) for JMX Exporter                                             | `ClusterIP`                                                                             |
| `metrics.jmx.service.port`                       | JMX Exporter Prometheus port                                                                                                     | `5556`                                                                                  |
| `metrics.jmx.service.nodePort`                   | Kubernetes HTTP node port                                                                                                        | `""`                                                                                    |
| `metrics.jmx.service.loadBalancerIP`             | loadBalancerIP if service type is `LoadBalancer`                                                                                 | `""`                                                                                    |
| `metrics.jmx.service.loadBalancerSourceRanges`   | Load Balancer sources                                                                                                            | `[]`                                                                                    |
| `metrics.jmx.service.clusterIP`                  | Static clusterIP or None for headless services                                                                                   | `""`                                                                                    |
| `metrics.jmx.service.annotations`                | Annotations for the JMX Exporter Prometheus metrics service                                                                      | `{}`                                                                                    |
| `metrics.jmx.whitelistObjectNames`               | Allows setting which JMX objects you want to expose to via JMX stats to JMX Exporter                                             | `["kafka.controller:*","kafka.server:*","java.lang:*","kafka.network:*","kafka.log:*"]` |
| `metrics.jmx.config`                             | Configuration file for JMX exporter                                                                                              | `""`                                                                                    |
| `metrics.jmx.existingConfigmap`                  | Name of existing ConfigMap with JMX exporter configuration                                                                       | `""`                                                                                    |
| `metrics.serviceMonitor.enabled`                 | if `true`, creates a Prometheus Operator ServiceMonitor (requires `metrics.kafka.enabled` or `metrics.jmx.enabled` to be `true`) | `false`                                                                                 |
| `metrics.serviceMonitor.namespace`               | Namespace in which Prometheus is running                                                                                         | `""`                                                                                    |
| `metrics.serviceMonitor.interval`                | Interval at which metrics should be scraped                                                                                      | `""`                                                                                    |
| `metrics.serviceMonitor.scrapeTimeout`           | Timeout after which the scrape is ended                                                                                          | `""`                                                                                    |
| `metrics.serviceMonitor.selector`                | ServiceMonitor selector labels                                                                                                   | `{}`                                                                                    |
| `metrics.serviceMonitor.relabelings`             | Relabel configuration for the metrics                                                                                            | `[]`                                                                                    |
| `metrics.serviceMonitor.metricRelabelings`       | MetricRelabelConfigs to apply to samples before ingestion                                                                        | `[]`                                                                                    |


### Kafka provisioning parameters

| Name                              | Description                                                           | Value   |
| --------------------------------- | --------------------------------------------------------------------- | ------- |
| `provisioning.enabled`            | Enable kafka provisioning Job                                         | `false` |
| `provisioning.numPartitions`      | Default number of partitions for topics when unspecified.             | `1`     |
| `provisioning.replicationFactor`  | Default replication factor for topics when unspecified.               | `1`     |
| `provisioning.schedulerName`      | Name of the k8s scheduler (other than default) for kafka provisioning | `""`    |
| `provisioning.podAnnotations`     | Provisioning Pod annotations.                                         | `{}`    |
| `provisioning.resources.limits`   | The resources limits for the container                                | `{}`    |
| `provisioning.resources.requests` | The requested resources for the container                             | `{}`    |
| `provisioning.command`            | Override provisioning container command                               | `[]`    |
| `provisioning.args`               | Override provisioning container arguments                             | `[]`    |
| `provisioning.topics`             | Kafka provisioning topics                                             | `[]`    |


### Zookeeper chart parameters

| Name                             | Description                                                                                                                                                             | Value   |
| -------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| `zookeeper.enabled`              | Switch to enable or disable the Zookeeper helm chart                                                                                                                    | `true`  |
| `zookeeper.auth.enabled`         | Enable Zookeeper auth                                                                                                                                                   | `false` |
| `zookeeper.auth.clientUser`      | User that will use Zookeeper clients to auth                                                                                                                            | `""`    |
| `zookeeper.auth.clientPassword`  | Password that will use Zookeeper clients to auth                                                                                                                        | `""`    |
| `zookeeper.auth.serverUsers`     | Comma, semicolon or whitespace separated list of user to be created. Specify them as a string, for example: "user1,user2,admin"                                         | `""`    |
| `zookeeper.auth.serverPasswords` | Comma, semicolon or whitespace separated list of passwords to assign to users when created. Specify them as a string, for example: "pass4user1, pass4user2, pass4admin" | `""`    |
| `externalZookeeper.servers`      | Server or list of external Zookeeper servers to use                                                                                                                     | `[]`    |


Specify each parameter using the `--set key=value[,key=value]` argument to `helm install`. For example,

```console
helm install my-release \
  --set replicaCount=3 \
  bitnami/kafka
```

The above command deploys Kafka with 3 brokers (replicas).

Alternatively, a YAML file that specifies the values for the parameters can be provided while installing the chart. For example,

```console
helm install my-release -f values.yaml bitnami/kafka
```

> **Tip**: You can use the default [values.yaml](values.yaml)

## Configuration and installation details

### [Rolling VS Immutable tags](https://docs.bitnami.com/containers/how-to/understand-rolling-tags-containers/)

It is strongly recommended to use immutable tags in a production environment. This ensures your deployment does not change automatically if the same tag is updated with a different image.

Bitnami will release a new chart updating its containers if a new version of the main container, significant changes, or critical vulnerabilities exist.

### Setting custom parameters

Any environment variable beginning with `KAFKA_CFG_` will be mapped to its corresponding Kafka key. For example, use `KAFKA_CFG_BACKGROUND_THREADS` in order to set `background.threads`. In order to pass custom environment variables use the `extraEnvVars` property.

Using `extraEnvVars` with `KAFKA_CFG_` is the preferred and simplest way to add custom Kafka parameters not otherwise specified in this chart. Alternatively, you can provide a *full* Kafka configuration using `config` or `existingConfigmap`.
Setting either `config` or `existingConfigmap` will cause the chart to disregard `KAFKA_CFG_` settings, which are used by many other Kafka-related chart values described above, as well as dynamically generated parameters such as `zookeeper.connect`. This can cause unexpected behavior.

### Listeners configuration

This chart allows you to automatically configure Kafka with 3 listeners:

- One for inter-broker communications.
- A second one for communications with clients within the K8s cluster.
- (optional) a third listener for communications with clients outside the K8s cluster. Check [this section](#accessing-kafka-brokers-from-outside-the-clusters) for more information.

For more complex configurations, set the `listeners`, `advertisedListeners` and `listenerSecurityProtocolMap` parameters as needed.

### Enable security for Kafka and Zookeeper

You can configure different authentication protocols for each listener you configure in Kafka. For instance, you can use `sasl_tls` authentication for client communications, while using `tls` for inter-broker communications. This table shows the available protocols and the security they provide:

| Method    | Authentication               | Encryption via TLS |
|-----------|------------------------------|--------------------|
| plaintext | None                         | No                 |
| tls       | None                         | Yes                |
| mtls      | Yes (two-way authentication) | Yes                |
| sasl      | Yes (via SASL)               | No                 |
| sasl_tls  | Yes (via SASL)               | Yes                |

Learn more about how to configure Kafka to use the different authentication protocols in the [chart documentation](https://docs.bitnami.com/kubernetes/infrastructure/kafka/administration/enable-security/).

If you enabled SASL authentication on any listener, you can set the SASL credentials using the parameters below:

- `auth.sasl.jaas.clientUsers`/`auth.sasl.jaas.clientPasswords`: when enabling SASL authentication for communications with clients.
- `auth.sasl.jaas.interBrokerUser`/`auth.sasl.jaas.interBrokerPassword`:  when enabling SASL authentication for inter-broker communications.
- `auth.jaas.zookeeperUser`/`auth.jaas.zookeeperPassword`: In the case that the Zookeeper chart is deployed with SASL authentication enabled.

In order to configure TLS authentication/encryption, you **can** create a secret containing the Java Key Stores (JKS) files: the truststore (`kafka.truststore.jks`) and one keystore (`kafka.keystore.jks`) per Kafka broker you have in the cluster. Then, you need pass the secret name with the `--auth.jksSecret` parameter when deploying the chart.

> **Note**: If the JKS files are password protected (recommended), you will need to provide the password to get access to the keystores. To do so, use the `auth.jksPassword` parameter to provide your password.

For instance, to configure TLS authentication on a Kafka cluster with 2 Kafka brokers use the command below to create the secret:

```console
kubectl create secret generic kafka-jks --from-file=./kafka.truststore.jks --from-file=./kafka-0.keystore.jks --from-file=./kafka-1.keystore.jks
```

> **Note**: the command above assumes you already created the trustore and keystores files. This [script](https://raw.githubusercontent.com/confluentinc/confluent-platform-security-tools/master/kafka-generate-ssl.sh) can help you with the JKS files generation.

As an alternative to manually create the secret before installing the chart, you can put your JKS files inside the chart folder `files/jks`, an a secret including them will be generated. Please note this alternative requires to have the chart downloaded locally, so you will have to clone this repository or fetch the chart before installing it.

If, for some reason (like using Cert-Manager) you can not use the default JKS secret scheme, you can use the additional parameters:

- `auth.jksTruststoreSecret` to define additional secret, where the `kafka.truststore.jks` is being kept. The truststore password **must** be the same as in `auth.jksPassword`
- `auth.jksTruststore` to overwrite the default value of the truststore key (`kafka.truststore.jks`).
- `auth.jksKeystoreSAN` if you want to use a SAN certificate for your brokers. Setting this parameter would mean that the chart expects a existing key in the `auth.jksSecret` with the `auth.jksKeystoreSAN`-value and use this as a keystore for **all** brokers

> **Note**: The truststore/keystore from above **must** be protected with the same password as in `auth.jksPassword`

You can deploy the chart with authentication using the following parameters:

```console
replicaCount=2
auth.clientProtocol=sasl
auth.interBrokerProtocol=tls
auth.certificatesSecret=kafka-jks
auth.certificatesPassword=jksPassword
auth.sasl.jaas.clientUsers[0]=brokerUser
auth.sasl.jaas.clientPasswords[0]=brokerPassword
auth.jaas.zookeeperUser=zookeeperUser
auth.jaas.zookeeperPassword=zookeeperPassword
zookeeper.auth.enabled=true
zookeeper.auth.serverUsers=zookeeperUser
zookeeper.auth.serverPasswords=zookeeperPassword
zookeeper.auth.clientUser=zookeeperUser
zookeeper.auth.clientPassword=zookeeperPassword
```

You can deploy the chart with AclAuthorizer using the following parameters:

```console
replicaCount=2
auth.clientProtocol=sasl
auth.interBrokerProtocol=sasl_tls
auth.tls.existingSecret=kafka-jks
auth.tls.password=jksPassword
'auth.sasl.jaas.clientUsers[0]=brokerUser'
'auth.sasl.jaas.clientPasswords[0]=brokerPassword'
auth.sasl.jaas.zookeeperUser=zookeeperUser
auth.sasl.jaas.zookeeperPassword=zookeeperPassword
zookeeper.auth.enabled=true
zookeeper.auth.serverUsers=zookeeperUser
zookeeper.auth.serverPasswords=zookeeperPassword
zookeeper.auth.clientUser=zookeeperUser
zookeeper.auth.clientPassword=zookeeperPassword
authorizerClassName=kafka.security.authorizer.AclAuthorizer
allowEveryoneIfNoAclFound=false
superUsers=User:admin
```

If you also enable exposing metrics using the Kafka expoter, and you are using `sasl_tls`, `tls`, or `mtls` authentication protocols, you need to mount the CA certificated used to sign the brokers certificates in the exporter so it can validate the Kafka brokers. To do so, create a secret containing the CA, and set the `metrics.certificatesSecret` parameter. As an alternative, you can skip TLS validation using extra flags:

```console
metrics.kafka.extraFlags={tls.insecure-skip-tls-verify: ""}
```

### Accessing Kafka brokers from outside the cluster

In order to access Kafka Brokers from outside the cluster, an additional listener and advertised listener must be configured. Additionally, a specific service per kafka pod will be created.

There are two ways of configuring external access. Using LoadBalancer services or using NodePort services.

#### Using LoadBalancer services

You have two alternatives to use LoadBalancer services:

- Option A) Use random load balancer IPs using an **initContainer** that waits for the IPs to be ready and discover them automatically.

```console
externalAccess.enabled=true
externalAccess.service.type=LoadBalancer
externalAccess.service.port=9094
externalAccess.autoDiscovery.enabled=true
serviceAccount.create=true
rbac.create=true
```

Note: This option requires creating RBAC rules on clusters where RBAC policies are enabled.

- Option B) Manually specify the load balancer IPs:

```console
externalAccess.enabled=true
externalAccess.service.type=LoadBalancer
externalAccess.service.port=9094
externalAccess.service.loadBalancerIPs[0]='external-ip-1'
externalAccess.service.loadBalancerIPs[1]='external-ip-2'}
```

Note: You need to know in advance the load balancer IPs so each Kafka broker advertised listener is configured with it.

Following the aforementioned steps will also allow to connect the brokers from the outside using the cluster's default service (when `service.type` is `LoadBalancer` or `NodePort`). Use the property `service.externalPort` to specify the port used for external connections.

#### Using NodePort services

You have two alternatives to use NodePort services:

- Option A) Use random node ports using an **initContainer** that discover them automatically.

```console
externalAccess.enabled=true
externalAccess.service.type=NodePort
externalAccess.autoDiscovery.enabled=true
serviceAccount.create=true
rbac.create=true
```

Note: This option requires creating RBAC rules on clusters where RBAC policies are enabled.

- Option B) Manually specify the node ports:

```console
externalAccess.enabled=true
externalAccess.service.type=NodePort
externalAccess.service.nodePorts[0]='node-port-1'
externalAccess.service.nodePorts[1]='node-port-2'
```

Note: You need to know in advance the node ports that will be exposed so each Kafka broker advertised listener is configured with it.

The pod will try to get the external ip of the node using `curl -s https://ipinfo.io/ip` unless `externalAccess.service.domain` or `externalAccess.service.useHostIPs` is provided.

#### Name resolution with External-DNS

You can use the following values to generate External-DNS annotations which automatically creates DNS records for each ReplicaSet pod:

```yaml
externalAccess:
  service:
    annotations:
      external-dns.alpha.kubernetes.io/hostname: "{{ .targetPod }}.example.com"
```
### Sidecars

If you have a need for additional containers to run within the same pod as Kafka (e.g. an additional metrics or logging exporter), you can do so via the `sidecars` config parameter. Simply define your container according to the Kubernetes container spec.

```yaml
sidecars:
  - name: your-image-name
    image: your-image
    imagePullPolicy: Always
    ports:
      - name: portname
       containerPort: 1234
```

### Setting Pod's affinity

This chart allows you to set your custom affinity using the `affinity` parameter. Find more information about Pod's affinity in the [kubernetes documentation](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity).

As an alternative, you can use of the preset configurations for pod affinity, pod anti-affinity, and node affinity available at the [bitnami/common](https://github.com/bitnami/charts/tree/master/bitnami/common#affinities) chart. To do so, set the `podAffinityPreset`, `podAntiAffinityPreset`, or `nodeAffinityPreset` parameters.

### Deploying extra resources

There are cases where you may want to deploy extra objects, such as Kafka Connect. For covering this case, the chart allows adding the full specification of other objects using the `extraDeploy` parameter. The following example would create a deployment including a Kafka Connect deployment so you can connect Kafka with MongoDB&reg;:

```yaml
## Extra objects to deploy (value evaluated as a template)
##
extraDeploy:
  - |
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: {{ include "kafka.fullname" . }}-connect
      labels: {{- include "common.labels.standard" . | nindent 4 }}
        app.kubernetes.io/component: connector
    spec:
      replicas: 1
      selector:
        matchLabels: {{- include "common.labels.matchLabels" . | nindent 6 }}
          app.kubernetes.io/component: connector
      template:
        metadata:
          labels: {{- include "common.labels.standard" . | nindent 8 }}
            app.kubernetes.io/component: connector
        spec:
          containers:
            - name: connect
              image: KAFKA-CONNECT-IMAGE
              imagePullPolicy: IfNotPresent
              ports:
                - name: connector
                  containerPort: 8083
              volumeMounts:
                - name: configuration
                  mountPath: /bitnami/kafka/config
          volumes:
            - name: configuration
              configMap:
                name: {{ include "kafka.fullname" . }}-connect
  - |
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: {{ include "kafka.fullname" . }}-connect
      labels: {{- include "common.labels.standard" . | nindent 4 }}
        app.kubernetes.io/component: connector
    data:
      connect-standalone.properties: |-
        bootstrap.servers = {{ include "kafka.fullname" . }}-0.{{ include "kafka.fullname" . }}-headless.{{ .Release.Namespace }}.svc.{{ .Values.clusterDomain }}:{{ .Values.service.port }}
        ...
      mongodb.properties: |-
        connection.uri=mongodb://root:password@mongodb-hostname:27017
        ...
  - |
    apiVersion: v1
    kind: Service
    metadata:
      name: {{ include "kafka.fullname" . }}-connect
      labels: {{- include "common.labels.standard" . | nindent 4 }}
        app.kubernetes.io/component: connector
    spec:
      ports:
        - protocol: TCP
          port: 8083
          targetPort: connector
      selector: {{- include "common.labels.matchLabels" . | nindent 4 }}
        app.kubernetes.io/component: connector
```

You can create the Kafka Connect image using the Dockerfile below:

```Dockerfile
FROM bitnami/kafka:latest
# Download MongoDB&reg; Connector for Apache Kafka https://www.confluent.io/hub/mongodb/kafka-connect-mongodb
RUN mkdir -p /opt/bitnami/kafka/plugins && \
    cd /opt/bitnami/kafka/plugins && \
    curl --remote-name --location --silent https://search.maven.org/remotecontent?filepath=org/mongodb/kafka/mongo-kafka-connect/1.2.0/mongo-kafka-connect-1.2.0-all.jar
CMD /opt/bitnami/kafka/bin/connect-standalone.sh /opt/bitnami/kafka/config/connect-standalone.properties /opt/bitnami/kafka/config/mongo.properties
```

## Persistence

The [Bitnami Kafka](https://github.com/bitnami/bitnami-docker-kafka) image stores the Kafka data at the `/bitnami/kafka` path of the container.

Persistent Volume Claims are used to keep the data across deployments. This is known to work in GCE, AWS, and minikube. See the [Parameters](#persistence-parameters) section to configure the PVC or to disable persistence.

### Adjust permissions of persistent volume mountpoint

As the image run as non-root by default, it is necessary to adjust the ownership of the persistent volume so that the container can write data into it.

By default, the chart is configured to use Kubernetes Security Context to automatically change the ownership of the volume. However, this feature does not work in all Kubernetes distributions.
As an alternative, this chart supports using an initContainer to change the ownership of the volume before mounting it in the final destination.

You can enable this initContainer by setting `volumePermissions.enabled` to `true`.

## Troubleshooting

Find more information about how to deal with common errors related to Bitnami’s Helm charts in [this troubleshooting guide](https://docs.bitnami.com/general/how-to/troubleshoot-helm-chart-issues).

## Upgrading

### To 14.0.0

In this version, the `image` block is defined once and is used in the different templates, while in the previous version, the `image` block was duplicated for the main container and the provisioning one

```yaml
image:
  registry: docker.io
  repository: bitnami/kafka
  tag: 2.8.0
```
VS
```yaml
image:
  registry: docker.io
  repository: bitnami/kafka
  tag: 2.8.0
...
provisioning:
  image:
    registry: docker.io
    repository: bitnami/kafka
    tag: 2.8.0
```

See [PR#7114](https://github.com/bitnami/charts/pull/7114) for more info about the implemented changes

### To 13.0.0

This major updates the Zookeeper subchart to it newest major, 7.0.0, which renames all TLS-related settings. For more information on this subchart's major, please refer to [zookeeper upgrade notes](https://github.com/bitnami/charts/tree/master/bitnami/zookeeper#to-700).

### To 12.2.0

This version also introduces `bitnami/common`, a [library chart](https://helm.sh/docs/topics/library_charts/#helm) as a dependency. More documentation about this new utility could be found [here](https://github.com/bitnami/charts/tree/master/bitnami/common#bitnami-common-library-chart). Please, make sure that you have updated the chart dependencies before executing any upgrade.

### To 12.0.0

[On November 13, 2020, Helm v2 support was formally finished](https://github.com/helm/charts#status-of-the-project), this major version is the result of the required changes applied to the Helm Chart to be able to incorporate the different features added in Helm v3 and to be consistent with the Helm project itself regarding the Helm v2 EOL.

**What changes were introduced in this major version?**

- Previous versions of this Helm Chart use `apiVersion: v1` (installable by both Helm 2 and 3), this Helm Chart was updated to `apiVersion: v2` (installable by Helm 3 only). [Here](https://helm.sh/docs/topics/charts/#the-apiversion-field) you can find more information about the `apiVersion` field.
- Move dependency information from the *requirements.yaml* to the *Chart.yaml*
- After running `helm dependency update`, a *Chart.lock* file is generated containing the same structure used in the previous *requirements.lock*
- The different fields present in the *Chart.yaml* file has been ordered alphabetically in a homogeneous way for all the Bitnami Helm Charts

**Considerations when upgrading to this version**

- If you want to upgrade to this version from a previous one installed with Helm v3, you shouldn't face any issues
- If you want to upgrade to this version using Helm v2, this scenario is not supported as this version doesn't support Helm v2 anymore
- If you installed the previous version with Helm v2 and wants to upgrade to this version with Helm v3, please refer to the [official Helm documentation](https://helm.sh/docs/topics/v2_v3_migration/#migration-use-cases) about migrating from Helm v2 to v3

**Useful links**

- https://docs.bitnami.com/tutorials/resolve-helm2-helm3-post-migration-issues/
- https://helm.sh/docs/topics/v2_v3_migration/
- https://helm.sh/blog/migrate-from-helm-v2-to-helm-v3/

### To 11.8.0

External access to brokers can now be achieved through the cluster's Kafka service.

- `service.nodePort` -> deprecated  in favor of `service.nodePorts.client` and `service.nodePorts.external`

### To 11.7.0

The way to configure the users and passwords changed. Now it is allowed to create multiple users during the installation by providing the list of users and passwords.

- `auth.jaas.clientUser` (string) -> deprecated  in favor of `auth.jaas.clientUsers` (array).
- `auth.jaas.clientPassword` (string) -> deprecated  in favor of `auth.jaas.clientPasswords` (array).

### To 11.0.0

The way to configure listeners and athentication on Kafka is totally refactored allowing users to configure different authentication protocols on different listeners. Please check the sections [Listeners Configuration](listeners-configuration) and [Listeners Configuration](enable-kafka-for-kafka-and-zookeeper) for more information.

Backwards compatibility is not guaranteed you adapt your values.yaml to the new format. Here you can find some parameters that were renamed or disappeared in favor of new ones on this major version:

- `auth.enabled` -> deprecated in favor of `auth.clientProtocol` and `auth.interBrokerProtocol` parameters.
- `auth.ssl` -> deprecated in favor of `auth.clientProtocol` and `auth.interBrokerProtocol` parameters.
- `auth.certificatesSecret` -> renamed to `auth.jksSecret`.
- `auth.certificatesPassword` -> renamed to `auth.jksPassword`.
- `sslEndpointIdentificationAlgorithm` -> renamedo to `auth.tlsEndpointIdentificationAlgorithm`.
- `auth.interBrokerUser` -> renamed to `auth.jaas.interBrokerUser`
- `auth.interBrokerPassword` -> renamed to `auth.jaas.interBrokerPassword`
- `auth.zookeeperUser` -> renamed to `auth.jaas.zookeeperUser`
- `auth.zookeeperPassword` -> renamed to `auth.jaas.zookeeperPassword`
- `auth.existingSecret` -> renamed to `auth.jaas.existingSecret`
- `service.sslPort` -> deprecated in favor of `service.internalPort`
- `service.nodePorts.kafka` and `service.nodePorts.ssl` -> deprecated in favor of `service.nodePort`
- `metrics.kafka.extraFlag` -> new parameter
- `metrics.kafka.certificatesSecret` -> new parameter

### To 10.0.0

If you are setting the `config` or `log4j` parameter, backwards compatibility is not guaranteed, because the `KAFKA_MOUNTED_CONFDIR` has moved from `/opt/bitnami/kafka/conf` to `/bitnami/kafka/config`. In order to continue using these parameters, you must also upgrade your image to `docker.io/bitnami/kafka:2.4.1-debian-10-r38` or later.

### To 9.0.0

Backwards compatibility is not guaranteed you adapt your values.yaml to the new format. Here you can find some parameters that were renamed on this major version:

```diff
- securityContext.enabled
- securityContext.fsGroup
- securityContext.fsGroup
+ podSecurityContext
- externalAccess.service.loadBalancerIP
+ externalAccess.service.loadBalancerIPs
- externalAccess.service.nodePort
+ externalAccess.service.nodePorts
- metrics.jmx.configMap.enabled
- metrics.jmx.configMap.overrideConfig
+ metrics.jmx.config
- metrics.jmx.configMap.overrideName
+ metrics.jmx.existingConfigmap
```

Ports names were prefixed with the protocol to comply with Istio (see https://istio.io/docs/ops/deployment/requirements/).

### To 8.0.0

There is not backwards compatibility since the brokerID changes to the POD_NAME. For more information see [this PR](https://github.com/bitnami/charts/pull/2028).

### To 7.0.0

Backwards compatibility is not guaranteed when Kafka metrics are enabled, unless you modify the labels used on the exporter deployments.
Use the workaround below to upgrade from versions previous to 7.0.0. The following example assumes that the release name is kafka:

```console
helm upgrade kafka bitnami/kafka --version 6.1.8 --set metrics.kafka.enabled=false
helm upgrade kafka bitnami/kafka --version 7.0.0 --set metrics.kafka.enabled=true
```

### To 2.0.0

Backwards compatibility is not guaranteed unless you modify the labels used on the chart's deployments.
Use the workaround below to upgrade from versions previous to 2.0.0. The following example assumes that the release name is kafka:

```console
kubectl delete statefulset kafka-kafka --cascade=false
kubectl delete statefulset kafka-zookeeper --cascade=false
```

### To 1.0.0

Backwards compatibility is not guaranteed unless you modify the labels used on the chart's deployments.
Use the workaround below to upgrade from versions previous to 1.0.0. The following example assumes that the release name is kafka:

```console
kubectl delete statefulset kafka-kafka --cascade=false
kubectl delete statefulset kafka-zookeeper --cascade=false
```
