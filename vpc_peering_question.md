## 1. What is VPC Peering?
A private network connection between two VPCs that enables communication using private IPs.

## 2. Can you peer VPCs in different regions?
Yes, using Inter-Region VPC Peering.

## 3. Does VPC peering use the Internet?
No — traffic flows through the AWS backbone, so it's secure and low latency.

## 4. What is the biggest limitation?
No transitive routing (A ↔ B and B ↔ C does not allow A ↔ C).

## 5. Do VPC CIDRs need to be unique?
Yes, no overlapping CIDR blocks are allowed.

## 6. What do you need to update after creating peering?
1. Route tables in both VPCs

2. Security groups to allow traffic

## 7. How do you test VPC peering?
- Ping private IP

- SSH using private IP

- Curl HTTP/HTTPS