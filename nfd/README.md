# Setting up Node Feature Discovery
[Node Feature Discovery (NFD) Operator](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator) manages the deployment and lifecycle of the NFD add-on to detect hardware features and system configuration, such as PCI cards, kernel, operating system version, etc.

## Prerequisites
- Provisioned RHOCP cluster. Follow steps [here](/README.md#provisioning-rhocp-cluster).

## Install NFD Operator
Follow the guide below to install the NFD operator using CLI or web console. 
- [Install from the CLI](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator#install-operator-cli_psap-node-feature-discovery-operator)
- [Install from the web console](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/specialized_hardware_and_driver_enablement/psap-node-feature-discovery-operator#install-operator-web-console_psap-node-feature-discovery-operator)

## Configure NFD Operator
Note: As RHOCP cluster administrator, you might need to merge the NFD operator config from the following Custom Resources (CRs) with other NFD operator configs that are already applied on your cluster.  

1. Create `NodeFeatureDiscovery` CR instance.
```
$ oc apply -f https://raw.githubusercontent.com/intel/intel-technology-enabling-for-openshift/main/nfd/node-feature-discovery-openshift.yaml 
```

2.	Create `NodeFeatureRule` CR instance.
```
$ oc apply -f https://raw.githubusercontent.com/intel/intel-technology-enabling-for-openshift/main/nfd/node-feature-rules-openshift.yaml
```

## Verification 
Use the following command to get the node name
```
$ oc get nodes
```
Use the command shown below to verify whether the nodes are labeled properly by NFD:
```
$ oc describe node <node_name> | grep intel.feature.node.kubernetes.io
```
Example output: 
```
intel.feature.node.kubernetes.io/dgpu-canary=true
intel.feature.node.kubernetes.io/gpu=true
```

## Labels Table
| Label | Intel hardware feature | 
| ----- | ---------------------- |
| `intel.feature.node.kubernetes.io/gpu=true` | Intel® Data Center GPU Flex Series or Intel® Data Center GPU Max Series | 
| `intel.feature.node.kubernetes.io/sgx=true` | Intel® SGX | 
| `intel.feature.node.kubernetes.io/qat=true` | Intel® QAT | 
| `intel.feature.node.kubernetes.io/dsa=true` | Intel® DSA | 

## See Also
