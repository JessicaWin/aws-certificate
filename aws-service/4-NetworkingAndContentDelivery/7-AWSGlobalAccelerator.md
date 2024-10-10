# Overview
+ AWS Global Accelerator is a service in which you create *accelerators* to **improve the performance of your applications** for local and global users.
+ Global Accelerator is a global service that supports endpoints in multiple AWS Regions.
# AWS Global Accelerator components
## **Static IP addresses**
+ Global Accelerator provides you with **a set of two static IP addresses that are anycast** from the AWS edge network.
+ If you **bring your own IP address range** to AWS (BYOIP) to use with Global Accelerator, you can instead assign IP addresses from your own pool to use with your accelerator. 
+ The static IP addresses provided by AWS Global Accelerator serve as **single fixed entry points** for your clients. 
+ With some endpoint types, you have the option to preserve and access the client IP address. 
+ Two types of endpoints can preserve the source IP address of the client in incoming packets: Application Load Balancers and Amazon EC2 instances.
+ Global Accelerator does not support client IP address preservation for Network Load Balancer and Elastic IP address endpoints.
+ Endpoints on custom routing accelerators always have the client IP address preserved.
## **Accelerator**
+ An accelerator **directs traffic to endpoints over the AWS global network** to improve the performance of your internet applications. Each accelerator includes one or more listeners.
+ A *standard* accelerator directs traffic to the optimal AWS endpoint based on several factors, including the user’s location, the health of the endpoint, and the endpoint weights that you configure. 
+ By using a **standard accelerator**, you can **improve availability of your internet applications** that are used by a global audience.
+ Endpoints can be Network Load Balancers, Application Load Balancers, Amazon EC2 instances, or Elastic IP addresses.
+ By using a **custom routing accelerator**, you can **map one or more users to a specific destination** among many destinations.
## **DNS name**
+ Global Accelerator assigns each accelerator a **default Domain Name System (DNS) name**, similar to `a1234567890abcdef.awsglobalaccelerator.com`, that points to the static IP addresses that Global Accelerator assigns to you or that you choose from your own IP address range.
## **Network zone**
+ A network zone services the static IP addresses for your accelerator from a unique IP subnet.**Similar to an AWS Availability Zone**, a network zone is an isolated unit with its own set of physical infrastructure.
## **Listener**
+ A listener **processes inbound connections from clients to Global Accelerator**, based on the port (or port range) and protocol (or protocols) that you configure.
+ A listener can be configured for **TCP, UDP**, or both TCP and UDP protocols.
+ Each listener has **one or more endpoint groups** associated with it, and traffic is forwarded to endpoints in one of the groups.
## **Endpoint group**
+ Each endpoint group is **associated with a specific AWS Region**.
+ Endpoint groups include **one or more endpoints in the Region**
## **Endpoint**
+ An endpoint is the resource that Global Accelerator directs traffic to.
+ Endpoints for **standard accelerators** can be Network Load Balancers, Application Load Balancers, EC2 instances, or Elastic IP addresses.
+ Endpoints for **custom routing accelerators** are virtual private cloud (VPC) subnets with one or many Amazon EC2 instances that are the destinations for traffic.
# How AWS Global Accelerator works
## Health Check
+ In **standard** accelerators, Global Accelerator **continuously monitors the health** of all endpoints, and instantly begins directing traffic to another available endpoint when it determines that an active endpoint is unhealthy. 
+ **Health checks aren't used with custom routing accelerators** and there is no failover, because you specify the destination to route traffic to.
## Idle timeout in AWS Global Accelerator
+ AWS Global Accelerator sets an idle timeout period that applies to its connections.
+ If no data has been sent or received by the time that the idle timeout period elapses, Global Accelerator closes the connection.
+ The timeout is 340 seconds for TCP connections.
+ The timeout is 30 seconds for UDP connections.
## Traffic flow management 
+ Change the **traffic dial** to **limit the traffic for one or more endpoint groups**
+ For each endpoint group in a standard accelerator, you can set a traffic dial to **control the percentage of traffic that is sent to the endpoint group**.
+ The percentage is **applied only to traffic that is already directed to the endpoint group**, not to all listener traffic.
+ For example, if you set the traffic dial for an endpoint group in `us-east-1` to 50 (that is, 50%) and the accelerator directs 100 user requests to that endpoint group, only 50 requests are accepted by the group. The accelerator directs the remaining 50 requests to endpoint groups in other Regions.
+ **Specify weights** to **change the proportion of traffic to the endpoints in a group**
+ The accelerator calculates the sum of the weights for the endpoints in an endpoint group, and then directs traffic to the endpoints based on the ratio of each endpoint's weight to the total.
+ By default, the weight for an endpoint is 128—that is, half of the maximum value for a weight, 255.
+ You configure traffic dials for *endpoint groups*. 
+ You use weights, on the other hand, to set values for *individual endpoints* within an endpoint group.
# Use cases
+ Scale for increased application utilization
+ Acceleration for latency-sensitive applications
+ Disaster recovery and multi-Region resiliency
+ Protect your applications
+ Improve performance for VoIP or online gaming applications
# Work with standard accelerators
+ To set up a standard accelerator, do the following: 
+ **Create an accelerator**, and choose the standard accelerator option.
+ **Add a listener** with a specific set of ports or port range, and choose the protocol to accept: TCP, UDP, or both.
+ **Add one or more endpoint groups**, one for each AWS Region in which you have endpoint resources.
+ **Add one or more endpoints to endpoint groups**. This isn't required, but traffic won't be routed if you don't have any endpoints. 
# Work with custom routing accelerators
+ To set up custom routing accelerator, you do the following: 
+ Review the guidelines and requirements for creating a custom routing accelerator
+ **Create a VPC subnet.** You can add EC2 instances to the subnet at any time after adding the subnet to Global Accelerator.
+ **Create an accelerator**, and select the option for a custom routing accelerator.
+ **Add a listener and specify a range of ports** for Global Accelerator to listen on. 
    + Make sure that you include a large range with enough ports for Global Accelerator to map to all the destinations that you expect to have.
    + These ports are distinct from destination ports, which you specify in the next step. 
+ **Add one or more endpoint groups** for AWS Regions in which you have VPC subnets. You specify the following for each endpoint group:
+ **An endpoint port range**, which represents the ports on your destination EC2 instances that will be able to receive traffic.
+ **The protocol for each destination port range**: UDP, TCP, or both UDP and TCP.
+ For the endpoint subnet, select a subnet ID. You can **add multiple subnets in each endpoint group** and subnets can be different sizes (up to /17).
# Reference
+ [What is AWS Global Accelerator? - AWS Global Accelerator](https://docs.aws.amazon.com/global-accelerator/latest/dg/what-is-global-accelerator.html)