## 1. What is VPC?
A vpc (virtual private cloud) is logical isolated section of a public cloud where we can deploy resources such as virtual machine, database and other services. It provide a private and secure network enviroment for cloud resources, similarly to an on-premices data center but hosted in public cloud. 

## 2. To create a vpc how many resources are required ?
To create a vpc minimum 4 resources are required :
1. vpc: The main resource that provides a logically isolated network.
2. subnet: Divide the vpc in smaller seagment called subnet.
3. Internet Gateway (IGW) (For public subnet): Allow instances in public subnets to communicate with the internet. Attached to vpc.
4. Route Table: Define how taffic is routed withen or outside the vpc.