## 1. What is VPC?
A vpc (virtual private cloud) is logical isolated section of a public cloud where we can deploy resources such as virtual machine, database and other services. It provide a private and secure network enviroment for cloud resources, similarly to an on-premices data center but hosted in public cloud. 

## 2. To create a vpc how many resources are required ?
To create a vpc minimum 4 resources are required :
1. vpc: The main resource that provides a logically isolated network.
2. subnet: Divide the vpc in smaller seagment called subnet.
3. Internet Gateway (IGW) (For public subnet): Allow instances in public subnets to communicate with the internet. Attached to vpc.
4. Route Table: Define how taffic is routed withen or outside the vpc.

## 3.Why do we need a VPC in AWS?
We need a VPC in AWS to control our network environment.

It helps us manage IP ranges, subnets, routing, security, and access to our resources.

Without a VPC, we cannot securely deploy EC2, databases, or other services.

VPC gives isolation, security, and full control like an on-prem data center.

## 4. What is CIDR? What CIDR did you use in your project?
CIDR (Classless Inter-Domain Routing) is a method of writing IP address ranges.

10.0.0.0/16

192.168.1.0/24

172.31.0.0/16

The /number (prefix) tells how many bits are fixed for the network part.

**In simple words:**

**CIDR defines how big your network is and how many IPs you get.**

**Example:**

- /16 → 65,536 IPs

- /24 → 256 IPs

- /28 → 16 IPs

CIDR is used in VPCs, subnets, routing tables, security groups, etc.

## 5. What is a subnet?
A subnet is a smaller network segment inside a VPC.

## 6. What is the difference between a public and private subnet?
A subnet whose route table has a route to the Internet Gateway (IGW) is called a public subnet.

A subnet whose route table does not have a route to the Internet Gateway (IGW) is called a private subnet.

| Feature           | Public Subnet   | Private Subnet         |
| ----------------- | --------------- | ---------------------- |
| Internet access   | Direct          | No direct access       |
| Route to IGW      | Yes             | No                     |
| Common resources  | Web servers     | Databases, app servers |
| Outbound internet | Direct          | Via **NAT Gateway**    |
| Security          | Less restricted | More secure            |

## 7. What is an Internet Gateway? 
An Internet Gateway allows instances in a public subnet to communicate with the internet.
