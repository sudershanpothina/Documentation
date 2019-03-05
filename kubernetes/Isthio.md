# Isthio

 ### Summary
- envoy is a side car that gets injected, its c++ and foot print is small
- < 1ms latency
- create a sevice account which can inject sidecars (for helm)
- namespace should have the label for istio-injectio=enabled
- kubectl label namespace <namespace> isthio-injection=enabled (apply this label for the namespace)
- create a container for that namespace
- Intelligent routing - canary testing is possible
- traffic shifting based on the comfort level is possible
- Egress gateway is possible (traffic going out is also possible)
- policies are created to open traffic up
- Circuit breakers (stops the service on multiple failures)
- retry policies 
- request rate limiting
- Can be applied to onprem applications
- Security
    - you can lock down in the same namespaces
    - injects mutual tls (turned on by default)
- observability
    - logs
    - telemetry
    - tracing
    - injects correlation id
    - no code changes necessary
    - dashboard for service tracing is possible (Weave scope is an example)
- Virtual services
    - route traffic based on different user
    - Taffic shifting is possible (route traffic between versions)
- goto kataconda for an example walk through 

- https://www.katacoda.com/courses/istio/deploy-istio-on-kubernetes
- https://blog.openshift.com/istio-on-openshift/

### Pros
    - Github stars graph
    - backed by google 
    - more traction on isthio
### Cons



# LinkerD
 - uses daemon sets