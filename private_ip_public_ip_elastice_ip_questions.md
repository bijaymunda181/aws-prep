## 1. What is a private IP address?
Private ip address are not reachable over the internet and can be used for communication between the instances in you vpc.

When you launch an EC2 instance into a vpc, A primary private ip address from the address range of the subnet is assigned to default network interface (eth0) of the instance.

A private ip address remain associate with the network interface when the instance is stoped and restarted and released when the instace is terminated.   