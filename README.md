# Zeebe Cluster Helm Chart

This functionality is in beta and is subject to change. The design and code is less mature than official GA features and is being provided as-is with no warranties. Beta features are not subject to the support SLA of official GA features.

## Requirements

* [Helm](https://helm.sh/) >= 2.8.0
* Kubernetes >= 1.8
* Minimum cluster requirements include the following to run this chart with default settings. All of these settings are configurable.
  * Three Kubernetes nodes to respect the default "hard" affinity settings
  * 1GB of RAM for the JVM heap


## Installing

* Add the official zeebe helm charts repo
  ```
  helm repo add zeebe https://helm.zeebe.io
  ```
* Install it
  ```
  helm install --name zeebe-cluster zeebe/zeebe-cluster
  ```

 ## Configuration
  | Parameter                     | Description                                                                                                                                                                                                                                                                                                                | Default                                                                                                                   |
| ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `elasticsearch.enabled`                 | Enable ElasticSearch deployment as part of the Zeebe Cluster                                                                                                                                | `true`                                                                                                           |
| `kibana.enabled`                 | Enable Kibana deployment as part of the Zeebe Cluster                                                                                                                                | `false`                                                                                                           |
| `clusterSize`                 | Set the Zeebe Cluster Size and the number of replicas of the replica set                                                                                                                                | `3`   
| `partitionCount`                 | Set the Zeebe Cluster partition count                                                                                                                                | `3`   
| `replicationFactor`                 | Set the Zeebe Cluster replication factor                                                                                                                                | `3`   
| `cpuThreadCount`                 | Set the Zeebe Cluster CPU thread count                                                                                                                                | `2`   
| `ioThreadCount`                 | Set the Zeebe Cluster IO thread count                                                                                                                                | `2`  
| `JavaOpts`                 | Set the Zeebe Cluster Broker JavaOpts. This is where you should configure the jvm heap size.                                                                                                                                | `-XX:+UseParallelGC -XX:MinHeapFreeRatio=5 -XX:MaxHeapFreeRatio=10 -XX:MaxRAMPercentage=25.0 -XX:GCTimeRatio=4 -XX:AdaptiveSizePolicyWeight=90 -XX:+PrintFlagsFinal`  
| `resources`                 | Set the Zeebe Cluster Broker Kubernetes Resource Request and Limits                                                                                                                                | `requests:`<br>  `cpu: 500m`<br>  ` memory: 1Gi`<br>`limits:`<br>  ` cpu: 1000m`<br>  ` memory: 2Gi`  
| `pvcSize`                 | Set the Zeebe Cluster Persistence Volume Claim Request storage size                                                                                                                                | `10Gi`  
| `pvcAccessModes`                 | Set the Zeebe Cluster Persistence Volume Claim Request accessModes                                                                                                                                | `[ "ReadWriteOnce" ]`  
| `pvcStorageClassName`                 | Set the Zeebe Cluster Persistence Volume Claim Request storageClassName                                                                                                                                | ``  

## Dependencies
This chart currently depends on the following charts: 
- [ElasticSearch Helm Chart](https://github.com/elastic/helm-charts/blob/master/elasticsearch/README.md)
- [Kibana Helm Chart](https://github.com/elastic/helm-charts/tree/master/kibana)
- [Prometheus Operator Helm Chart](https://github.com/helm/charts/tree/master/stable/prometheus-operator)

These dependencies can be turned on or off and parameters can be overriden from these dependent charts by changing the `values.yaml` file. For example:
```
elasticsearch:
  enabled: true
  imageTag: <YOUR VERSION HERE>
kibana:
  enabled: false
```