# Kubernetes

USE CONTAINER LINUX as OS image

Simian army consists of Chaos Monkey. Chaos Gorilla and others


Probes are important for readyniess and health checks

Clair - security scanning for scanning registry (open source)

https://coreos.com/clair/docs/latest/

https://github.com/coreos/clair

Check what images are being pulled often (architecture side)


# installation (All these are production ready)

kubeadm
cops

### redhat way
okd

#### logging
efk (f - fluent)
logstash is not really that great

Distillation
 - expose minimum ports
 - NO yum, apt-get 
 - No internal builds

### using jlink from java 9 may reduce the resource utilization

## kubernetes job? Read more about it


#### Deamon set is a pod that runs on every node



jobs and cron jobs can be done with simple containers 
example liquidbase 

# look into kubernetes job object

 - cronjob can be scheduled

### Pod composites
 - Can be used as side cars or ambarsidors

### You can also have init containers which validates, makes things ready for the continers

## Initialization containers - are they gone after ? YES

## !!!!! kind Pod preset -> will inject pod definition (very useful)

Microfront end is a pattern for breaking up front end





