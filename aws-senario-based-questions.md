## 1. You created an EC2 instance but cannot connect via SSH. What will you check?
1. Security Group rules

Make sure the instance’s security group allows SSH inbound:

| Direction | Protocol | Port | Source                                |
| --------- | -------- | ---- | ------------------------------------- |
| Inbound   | TCP      | 22   | Your IP (not `0.0.0.0/0` if possible) |

Also verify:

- Outbound rules allow traffic to 0.0.0.0/0 (or at least allow return SSH traffic).

2. Correct key pair & permissions

You must SSH using the same key pair that was associated at instance launch.

- Private key file (.pem) permissions must be set correctly:

chmod 400 keypair.pem

3. Public IP / Networking

Check that:

- The instance has a public IP / Elastic IP if connecting from the Internet.

- The instance is in a public subnet (route table has a route to an Internet Gateway).

- Network ACLs allow SSH (inbound and outbound):

- Inbound allow port 22

- Outbound allow ephemeral ports (1024–65535)

So if SSH doesn’t work, the issue will be one of these (most likely):

| Category | Examples                                                  |
| -------- | --------------------------------------------------------- |
| Network  | Public IP, Security Groups, NACLs, routing                |
| Key Pair | Wrong key, missing private key, wrong permissions         |
| OS       | Wrong username, SSH daemon is down, firewall blocking SSH |

## 3. Your private subnet instance needs to download updates. What will you use? 
If an EC2 instance is in a private subnet and needs to reach the internet to download updates or packages, the correct solution is NAT Gateway (or NAT Instance) in a public subnet.

Instances in a private subnet do not have a route to the Internet Gateway (IGW), so they cannot access external repositories for updates.

A NAT Gateway provides:

- Outbound Internet access from private subnets

- No inbound Internet access (remains secure)

**So the traffic flow is:**

Private subnet instance → NAT Gateway → Internet Gateway → Internet

## 4. EC2 in private subnet wants to access S3 without Internet. What should you configure?
To allow an EC2 instance in a private subnet to access Amazon S3 without using the Internet, you should configure:

A VPC Gateway Endpoint for S3

🔍 **Why this is needed**

Instances in private subnets cannot reach S3 by default because:

- S3 is a public AWS service

- Private subnets do not route to the Internet Gateway

A **VPC Gateway Endpoint for S3** creates a private connection between your VPC and S3 using the AWS backbone — no Internet, no NAT Gateway required.

🧱 Required configuration

1. Create a Gateway VPC Endpoint for S3

2. Attach it to the route table of the private subnet

3. (Optional but recommended) Add an S3 bucket policy to allow access only via the VPC endpoint

After adding the endpoint, the private subnet route table gets an entry:

pl-xxxxxxxxxx (S3 VPC endpoint) → prefix list for S3

🆚 Why not NAT Gateway?

| Option               | Internet Required? | Use Case                                     |
| -------------------- | ------------------ | -------------------------------------------- |
| NAT Gateway          | Yes                | Internet access for OS updates, app installs |
| VPC Gateway Endpoint | No                 | Private access to S3 and DynamoDB only       |

## 2. Your private subnet instance needs to download updates. What will you use?
I will use NAT Gateway because NAT Gateway allow instance in a private to communicate with the internet.
