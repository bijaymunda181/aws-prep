## 1. What is a private IP address?
Private ip address are not reachable over the internet and can be used for communication between the instances in you vpc.

When you launch an EC2 instance into a vpc, A primary private ip address from the address range of the subnet is assigned to default network interface (eth0) of the instance.

A private ip address remain associate with the network interface when the instance is stoped and restarted and released when the instace is terminated.   

## 2. Why do we use private IPs in AWS?
We use private IPs in AWS to enable secure internal communication between resources without exposing them to the public internet.

🔑 Key Reasons Why Private IPs are used

1. Security

Resources like databases, backend servers, and internal applications should not be reachable from the outside world.

Using private IP ensures:

- No direct internet access

- Reduced attack surface

2. Internal communication

Instances inside a VPC talk using private IPs:

EC2 ↔ RDS

EC2 ↔ EC2

EC2 ↔ Load Balancer

This allows fast and secure traffic within the VPC. 

3. Cost savings

Traffic over private IP (inside VPC) is free or cheaper compared to internet traffic.

Private IPs keep internal traffic secure and isolated, while allowing AWS resources to communicate efficiently without internet.
