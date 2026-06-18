EC2 (Elastic Compute Cloud) 
AWS's core compute service. It lets you launch virtual servers (instances) on demand, in minutes. You control OS, software, networking, and scaling. Billed per second/hour. Use cases: web apps, batch processing, development environments, machine learning.
AMI (Amazon Machine Image)
A pre-configured template containing the OS (e.g., Amazon Linux, Ubuntu, Windows) and optionally applications, software, and configurations. When you launch an EC2 instance, you select an AMI. You can create custom AMIs from existing instances to reuse setups, or use AWS Marketplace AMIs for third-party solutions.
Instance types 
Define the underlying hardware of an EC2 instance: vCPU, memory (RAM), storage, networking performance. Families:  
- General purpose (e.g., t3, m5) – balanced for web servers, small DBs.  
- Compute optimized (e.g., c5, c6g) – for CPU-heavy workloads (batch, media transcoding).  
- Memory optimized (e.g., r5, x1) – for large in-memory caches, real-time analytics.  
- Storage optimized (e.g., i3, d2) – high disk I/O for databases, data warehouses.  
- GPU instances (e.g., p3, g4) – for deep learning, 3D rendering.  

EBS (Elastic Block Store)  
Persistent block-level storage volumes that attach to EC2 instances. They survive instance stops/terminations. Types: gp2/gp3 (general purpose SSD), io1/io2 (high-performance SSD – low latency), st1 (throughput optimized HDD), sc1 (cold HDD). Snapshots to S3 for backup. Can be detached and reattached to other instances. Max volume size: 16 TiB.

Security Groups 
Stateful virtual firewalls at the instance level. Each rule specifies protocol, port, and source/destination (CIDR or another security group). Default: all inbound denied, all outbound allowed. You can have up to 5 (or more with request) SGs per instance. They are separate from NACLs (stateless subnet firewalls). Changes take effect immediately.

SSH (Secure Shell)  
Encrypted protocol for remote command-line access to Linux/Unix EC2 instances. Typically on port 22. Requires a key pair: private key (.pem) held by user, public key stored on instance at launch. Windows instances use RDP (3389) instead. Best practice: restrict SSH access to trusted IPs, use security groups, never share private keys.
