# Kubernetes logging and monitoring example

This repo contains all the kubernetes resources yaml files to deploy monitoring & centralized logging.

## Cloning
```
git clone git@github.com:Misterhex/kubernetes-logging-monitoring-example.git
cd kubernetes-logging-monitoring-example
```

## Cluster setup ( Kops )
Follow below document to setup cluster on AWS
https://github.com/kubernetes/kops/blob/master/docs/aws.md

## Dashboard
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/kubernetes-dashboard/v1.7.1.yaml
```

## Monitoring with Heapster - Standalone

Heapster is required to supports the horizontal pod autoscaler.

Install using:
```
kubectl create -f https://raw.githubusercontent.com/kubernetes/kops/master/addons/monitoring-standalone/v1.7.0.yaml
```

## Create an ELK Cluster ( out of band )
Provision your own elasticsearch cluster or used [elastic hosted solution](https://cloud.elastic.co)

## Monitoring Kubernetes (ELK)
Once you have elasticsearch running out of band. ( not inside kubernetes )

### Centralized Logging
Runs fluentd as daemonset to collect containers logs.

```
kubectl apply -f fluentd
```

### Monitoring
kube-state-metrics provide metricset for metricbeat's kubernetes.

```
kubectl apply -f kube-state-metrics
kubectl apply -f metricbeat
```
