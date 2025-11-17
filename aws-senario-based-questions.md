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
