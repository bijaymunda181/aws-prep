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

## 8. How does a NAT Gateway work?
A NAT Gateway (Network Address Translation Gateway) allows instances in a private subnet to access the internet

**How it works step-by-step:**

1. **Instance in private subnet sends a request**

Example: An EC2 instance in a private subnet wants to download updates from the internet.

2. **Traffic goes to the NAT Gateway**

The private subnet’s route table has a route:

0.0.0.0/0 → NAT Gateway


3. **NAT Gateway replaces the private IP with its own public IP**

This hides the private instance’s IP by performing address translation.

4. **Traffic goes out to the Internet Gateway (IGW)**

The NAT Gateway is in a public subnet, so it sends the request through the IGW.

5. **Response returns to NAT Gateway**

The external server responds to the NAT Gateway’s public IP.

6. **NAT Gateway translates the response back**

It maps the response to the private IP of the instance.

7. **Response is delivered to the private instance**

The private instance gets the data, but it was never exposed to the internet.

## 9. What is the difference between IGW and NAT Gateway?
🚪 Internet Gateway (IGW)

Purpose: Allows instances with public IPs to access the internet and allows the internet to reach them.

Key Points

- Attach an IGW to your VPC to enable internet connectivity.

- Works with public subnets.

- Allows bi-directional traffic (outbound + inbound).

- Instances must have:

- A public IPv4 address (Elastic IP or auto-assigned), and

- A route to the IGW (0.0.0.0/0 → igw-xxxx).

**Use Case**

- Hosting public web servers, ALBs, bastion hosts, etc.

🔄 NAT Gateway

Purpose: Allows instances in private subnets to access the internet outbound only while preventing the internet from initiating inbound connections to them.

Key Points

- A NAT Gateway is placed in a public subnet.

- Private subnets route internet-bound traffic to the NAT Gateway (0.0.0.0/0 → nat-xxxx).

- Supports only outbound connections.

- Instances remain private (no public IP needed).

**Use Case**

Private EC2s needing updates or external API calls without being exposed to the internet.

## 10. What is a Route Table?
Route Table define how traffic will route within or outside the vpc.

## 11. What Is the Default VPC?
A preconfigured VPC that AWS creates for you in every AWS region so you can immediately launch EC2 instances that have internet access without creating any networking components.


