# Installation of MetalLB in a k8s cluster:
MetalLB is a load-balancer implementation for bare metal Kubernetes clusters. In Kubernetes, load balancing is usually handled by cloud providers, but in bare metal environments, there is no built-in load balancer, which can make it difficult to expose services externally. MetalLB solves this problem by providing a layer 2 or layer 3 load balancing solution that integrates with Kubernetes.

With MetalLB, you can allocate an IP address range for use with load balancers in your cluster. When a service is created that needs to be exposed externally, MetalLB automatically assigns an available IP address from that range to the service. MetalLB supports a range of load-balancing protocols, including TCP, UDP, and SNI.
One of the benefits of MetalLB is that it is relatively simple to set up and configure. It can be installed as a Kubernetes manifest and configured using a simple YAML configuration file. Additionally, MetalLB is open source software, so it is freely available for use and can be customized to meet specific requirements

This documentation helps an engineer to understand self sufficient to deploy and configure MetalLB in bare metal kubernetes cluster.

## Contents:
1.	What is MetalLB.
2.	Prerequisites.
3.	Installation process.
4.	Source code
5.	Conclusion.


### Prerequisites:
1.	A running Kubernetes cluster: You should have a working Kubernetes cluster, either locally or on a cloud provider.
2.	Access to the Kubernetes API server: You should have access to the Kubernetes API server, either by running kubectl commands locally or through a web-based interface such as the Kubernetes dashboard.
3.	Administrative access: You should have administrative access to the Kubernetes cluster, as MetalLB requires the ability to create Kubernetes resources such as namespaces, secrets, and ConfigMaps.
4.	A range of IP addresses to use for load balancing: You should have a range of IP addresses that MetalLB can use to assign to services. These IP addresses should be within the same subnet as the nodes in your Kubernetes cluster, and they should not be used by any other devices on your network.
5.	Kubernetes version: MetalLB works with Kubernetes versions 1.13 or later.
6.	By ensuring that these prerequisites are met, you can install and use MetalLB in your Kubernetes cluster with minimal hassle.

### Installation process.
1.	Create a namespace by running below file
```
namespace.yaml
```
2.	Run the metallb-config.yaml file
* metallb-config.yaml is a YAML file that is used to configure MetalLB, a load balancer for Kubernetes. The metallb-config.yaml file contains the configuration for MetalLB's behavior, such as how to allocate IP addresses for Kubernetes services. The configuration file typically defines one or more IP address pools that MetalLB can use to assign IP addresses to services. An IP address pool is defined as a range of IP addresses and a protocol (either layer 2 or layer 3).
3.	Run metallb.yaml
* IPAddressPool is a feature in MetalLB that allows you to define a pool of IP addresses that can be used for load balancing in a Kubernetes cluster. When you create a Kubernetes service that needs to be exposed externally, MetalLB assigns an available IP address from this pool to the service. An IPAddressPool can be defined in the MetalLB configuration using a Kubernetes ConfigMap. The ConfigMap contains a YAML file that defines the pool, including the range of IP addresses to use, the protocol to use (either layer 2 or layer 3), and any additional options such as the subnet mask or gateway.
4.	Run configmap-12-1.yaml
5.	Run L2Advertisement.yaml
* L2Advertisement is a feature in MetalLB that allows you to advertise your Kubernetes services using layer 2 (L2) addressing. When you create a Kubernetes service in a cluster, MetalLB can automatically assign it an IP address from a pool of available addresses, and then advertise that address to the local network using the Address Resolution Protocol (ARP). Other devices on the network can then use this address to connect to the service.

### Source code
All the codes have been documented in TFS GitHub - https://github.com/praveenprv/metallb

### Conclusion
MetalLB is a load balancer implementation for Kubernetes clusters that provides network load balancing functionality. It allows Kubernetes services to be exposed outside the cluster by assigning them IP addresses from a configured address pool. By installing MetalLB in a Kubernetes cluster, users can easily create and manage load balancers for their applications without relying on external load balancing solutions. MetalLB supports both Layer 2 and BGP routing modes and can be used in a wide range of deployment scenarios. Overall, MetalLB is a powerful and flexible load balancer solution for Kubernetes that is well-suited for a wide range of use cases, from small-scale deployments to large enterprise-level clusters. When creating a Kubernetes service with type: LoadBalancer, MetalLB can be used to assign an external IP address to the service. This IP address will be selected from the IP address pool that is configured in MetalLB.

