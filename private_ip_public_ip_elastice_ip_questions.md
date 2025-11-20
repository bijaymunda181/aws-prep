## **Private IP — Interview Questions**

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

## 3. Which subnets get private IPs — public or private?
Both public and private subnets get private IPs.

Every EC2 instance launched in a VPC always receives a private IP, no matter which subnet it is in.

## 4. Can private IPs communicate with the internet?
A private IP cannot communicate with the internet directly, but it can access the internet through a NAT device.

## 5. Can private IPs communicate between different VPCs?
Yes — private IPs can communicate between different VPCs, but only if the VPCs are connected using a networking method.

Private IPs alone cannot do it — there must be a connection path.

🔗 Ways for private IPs to communicate across VPCs

| Connectivity Method                  | Allows private IP to communicate?           |
| ------------------------------------ | ------------------------------------------- |
| **VPC Peering**                      | ✔ Yes                                       |
| **Transit Gateway**                  | ✔ Yes                                       |
| **AWS Site-to-Site VPN**             | ✔ Yes (via on-prem or another VPC)          |
| **Direct Connect**                   | ✔ Yes (if routed properly)                  |
| **PrivateLink (Interface Endpoint)** | ✔ Yes (but one-direction: client → service) |


## 6. Can two EC2 instances in the same VPC communicate using private IP?
Yes — two EC2 instances in the same VPC can communicate using their private IPs.

In fact, they always communicate using private IPs inside the VPC, even if they also have public IPs.

## 7. Can you change the private IP of an EC2 instance?
Yes — you can change the private IP of an EC2 instance, but with some conditions.

For Primary Private IP (the main IP)

| Case                                | Allowed?                |
| ----------------------------------- | ----------------------- |
| **Stop the instance and change IP** | ✔ Yes                   |
| **Change while running**            | ❌ Not allowed           |
| **Detach ENI and attach a new ENI** | ✔ Changes IP indirectly |


To change the primary private IP:

1. Stop the EC2 instance

2. Go to Network Interfaces (ENI)

3. Choose the ENI → Edit primary private IP

4. Assign a new IP from the subnet range

5. Start the instance again

**For Secondary Private IPs**

| Action                     | Allowed?        |
| -------------------------- | --------------- |
| Add / Remove while running | ✔ Yes           |
| Move to another instance   | ✔ Yes (via ENI) |

Secondary private IPs can be added anytime and do not require instance stop.

## 8. What is primary vs secondary private IP?
The primary private IP is the default, mandatory IP assigned to an EC2 instance through its ENI and is used for default outbound communication. Secondary private IPs are optional extra IPs that can be manually attached to the same ENI and can be added or removed without stopping the instance.

## 9. When does AWS assign a private IP?
AWS assigns a private IP to an EC2 instance automatically at launch time.

## 10. 
