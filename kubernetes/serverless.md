# Serverless

### Summary
- start in 20ms and run in half second
- multiple languages support
- scaling is done by kube based on requests
- fast way to prototype and mock
- goto cncf (cloud native foundation) http://s.cncf.io
- kubeless
- serverless commands are the same, no matter what techonology is used
- two different ways
    - function is injection into a container from code in configmap (Recommended)
    - function is prebaked in a container
- this is a custom resource definition
- kubeless
    - uses prebaked method
    - kataconda/javajohn has example on how
    - this is not stable
    - but does demonstrate how it works
    - has a dashboard where we can look at all the functions
        - `kubeless get-server-config`
        - create a python function 
        - submit as kubeless function
        - check on the dashboard
        - the function gets submitted as a config file
        - `kubeless function list` 
        - `kubeless function call <funtion name> --data '{"length":"10"}`
        - can also be done with kubectl commands
- openFaas
    - it is also open source like kubeless
    - more traction
    - alternative to injecting code as configmaps
    - may be production ready
    - goto katakoda for tutorial
    - not the same kubernetes yaml template
- openwhisk
    - learn.openshift.com/serverless
- knative
    - joint effort between google, redhat and others
    - pure kubernetes
    - works with istio mesh
    - not a serverless solution but is a common ground
    - pivitol -> riff -> knative (enterprise prod ready)

- Apache openwisk or Oracle Fn may be enterprise prodcution ready    
### Pros

### Cons
 - still imature
### Others