## Introduction

- In this repository contains files necessary to provisioning Zabbix in Kubernetes

# Pre requirements

- Kubernetes (Used version: v1.25.0)

# Zabbix service configuration with K8S
![image](https://github.com/smilewonjin/k8s-zabbix/assets/126428788/3c1482bf-a2c7-4102-8f04-9999726b001f)

![image](https://github.com/smilewonjin/k8s-zabbix/assets/126428788/4ec77444-73fc-4518-ba77-1aea4c2892a1)

# File structure

| File			| Content | Resources |
| ------------- | ------- | --------- |
| [cadvisor.yaml](./cadvisor.yaml) | Configuration to get and export monitoring metrics of [cAdvisor](https://prometheus.io/docs/guides/cadvisor/) ||
| [clusterRole-monitoring.yaml](./clusterRole-monitoring.yaml) | Prometheus roles ||
| [confimaps.yaml](./confimaps.yaml) | Non confidential variables with data used in many files | [ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)
| [nampespace.yaml](./nampespace.yaml) | Namespace configuration |[Namespaces](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/)|
| [zabbix-agent.yaml](zabbix-agent.yaml) | Configuration of Zabbix Agent | [Statefulsets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/), [PVC and PV](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) |
| [database-mysql.yaml](./database-mysql.yaml) |Database configuration | [Statefulsets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/), [PVC and PV](https://kubernetes.io/docs/concepts/storage/persistent-volumes/), [Service](https://kubernetes.io/docs/concepts/services-networking/service/), [StorageClass](https://kubernetes.io/docs/concepts/storage/storage-classes/) |
| [zabbix-server.yaml](./zabbix-server.yaml) | Zabbix server configuration | [Statefulsets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) and [Service](https://kubernetes.io/docs/concepts/services-networking/service/) |
| [zabbix-frontend.yaml](./zabbix-frontend.yaml) | Frontend configuration | [Statefulsets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) and [Service](https://kubernetes.io/docs/concepts/services-networking/service/) |


# Step by Step


1- Execute the apply to create namespace.

```
kubectl apply -f namespace.yaml
```

2- Execute the apply to create configmaps
```
kubectl apply -f configmaps.yaml
```

3 - Execute the apply to create secrtetes
```
kubectl apply -f secretes.yaml
```

4 - Execute the apply to create database
```
kubectl apply -f database-mysql.yaml 
```

5 - Execute the apply to create zabbix-agent
```
kubectl apply -f zabbix-agent.yaml
```

6- Execute the apply to create zabbix-server

```
 kubectl apply -f zabbix-server.yaml
```
7 - Execute the apply to create frontend

```
 kubectl apply -f zabbix-frontend.yaml 
```

Execute the command to get informations about your enviromennt:

```
kubectl get deployment,svc,pods,pvc,ingress  -n monitoring

```
![image](https://github.com/smilewonjin/k8s-zabbix/assets/126428788/c0c1f2fd-11cd-4332-9c3c-edf85cb20462)

```
kubectl describe -n monitoring svc

```
![image](https://github.com/smilewonjin/k8s-zabbix/assets/126428788/5f67cbdf-9da8-4f7d-9ba5-682864de90b4)


## CADVISOR

The Cadvisor export the metrics of the Kubernetes if you preferer monitoring this environment with the Zabbix.

```
kubectl apply -f cadvisor.yaml
```



## Access

## Metrics

## Dashboard
![image](https://github.com/smilewonjin/k8s-zabbix/assets/126428788/b6dd4dd8-927c-48b5-ac84-4c452fcb36f2)





## Reference

https://www.zabbix.com/documentation/current/manual/config/items/itemtypes/prometheus

https://hub.docker.com/u/zabbix/

https://kubernetes.io/docs/concepts/


Thanks, @QuintilianoB for collaborating with the best practices Kubernetes  :)
