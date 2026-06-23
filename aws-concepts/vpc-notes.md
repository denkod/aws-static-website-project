**VPC (Virtual Private Cloud) 
Your logically isolated section of AWS. You define an IP address range using **CIDR blocks** (e.g., 10.0.0.0/16). Provides **network isolation** from other VPCs and accounts by default.

**Subnets 
Subdivisions of your VPC CIDR (e.g., 10.0.1.0/24). Deployed in a single Availability Zone.  
- **Public subnet– has a route to an Internet Gateway. Resources (e.g., web servers) get public IPs.  
- **Private subnet – no direct route to the internet. Used for databases, app servers. Outbound access via NAT Gateway.

Route Tables 
Define where network traffic goes. Each subnet must be associated with one route table. Rules say: "destination → target" (e.g., 0.0.0.0/0 → Internet Gateway for public subnets; or 0.0.0.0/0 → NAT Gateway for private subnets).

Internet Gateway (IGW)  
A horizontally scaled, redundant VPC component enabling communication between VPC resources and the internet. Attached to a VPC. Required for public subnets.

NAT Gateway 
Managed service that allows instances in a private subnet to initiate outbound traffic to the internet (e.g., for updates) but prevents inbound traffic from the internet. Placed in a public subnet with an Elastic IP.

Security Groups vs NACLs**  
- Security Groups (SG):Instance-level, stateful. Only "allow" rules.  
- Network ACLs (NACL): Subnet-level, stateless. Supports allow/deny rules. Rules evaluated in order.  
- Use both for defense-in-depth: SG for granular instance control, NACL for subnet-level boundaries (e.g., block specific IPs).

Real Architecture (example) 
- VPC: 10.0.0.0/16  
- Public Subnet (AZ-a): Web servers behind ALB, route 0.0.0.0/0 → IGW  
- Private Subnet (AZ-a): App servers, route 0.0.0.0/0 → NAT Gateway  
- Private Subnet (AZ-b): RDS database, no internet route  
- Security Groups: Web SG allows HTTP/HTTPS from 0.0.0.0/0; App SG allows only from Web SG; DB SG allows only from App SG on port 3306.  
- NACLs: Stateless rules allowing ephemeral ports for return traffic.