# Secure-VPC-Peering-for-Multi-Cloud-Connectivity

## 📌 Project Overview
This project demonstrates **secure VPC-to-VPC peering** in AWS, enabling private communication between multiple **Virtual Private Clouds (VPCs)** without using the public internet. The architecture ensures **scalability, security, and high availability** for cloud environments.

## 🎯 Key Features
- **Private VPC Communication** – Establishes a secure, direct connection between VPCs.
- **Multi-Environment Setup** – Enables seamless connectivity across dev, test, and prod environments.
- **Custom Route Tables & CIDR Ranges** – Prevents network conflicts and ensures controlled access.
- **IAM Role-Based Security** – Implements least privilege access control for VPC peering.
- **Highly Available & Scalable** – Supports multiple regions and accounts for flexible deployments.

## 🏗️ Architecture Diagram
![Image](https://github.com/user-attachments/assets/530e0307-3bd5-46dc-b58f-8164bd74af9d)

## 📋 Prerequisites
Ensure you have the following before starting:
- AWS Account with IAM Admin Access
- Two or more VPCs with **non-overlapping CIDR blocks**
- AWS CLI installed and configured
- Terraform (optional) for Infrastructure as Code (IaC)

## 🚀 Deployment Steps
### **1️⃣ Create VPCs**
Define and configure VPCs in **different AWS regions or accounts**:
```sh
aws ec2 create-vpc --cidr-block 10.0.0.0/16
aws ec2 create-vpc --cidr-block 192.168.1.0/24
```

### **2️⃣ Configure VPC Peering**
Create a **VPC peering connection** between VPCs:
```sh
aws ec2 create-vpc-peering-connection \
    --vpc-id vpc-xxxxxxxx \
    --peer-vpc-id vpc-yyyyyyyy \
    --region us-east-1
```

### **3️⃣ Accept the Peering Connection**
```sh
aws ec2 accept-vpc-peering-connection --vpc-peering-connection-id pcx-zzzzzzzz
```

### **4️⃣ Update Route Tables**
Modify the route tables in **both VPCs** to allow traffic:
```sh
aws ec2 create-route --route-table-id rtb-xxxxx \
    --destination-cidr-block 192.168.1.0/24 \
    --vpc-peering-connection-id pcx-zzzzzzzz
```

### **5️⃣ Verify Connectivity**
Use `ping` or `telnet` to confirm communication between instances in different VPCs.

## 🔐 Security Best Practices
✅ Use **IAM Policies** to restrict access to VPC Peering.
✅ Implement **Network ACLs & Security Groups** for fine-grained access control.
✅ Avoid **transitive peering** unless explicitly needed.
✅ Use **VPC Flow Logs** to monitor traffic and detect anomalies.
✅ Regularly audit security configurations using **AWS Config & CloudTrail**.

## 🛠️ Terraform Automation (Optional)
You can automate this setup using **Terraform**:
```hcl
resource "aws_vpc_peering_connection" "peer" {
  vpc_id        = aws_vpc.main.id
  peer_vpc_id   = aws_vpc.peer.id
  auto_accept   = true
}
```

## 📌 Use Cases
- **Multi-Region VPC Communication** – Enables hybrid cloud setups.
- **Microservices Architecture** – Connects services running in different VPCs.
- **Enterprise Cloud Networking** – Securely integrates multiple AWS environments.

## 📜 Conclusion
This project enables **secure, scalable, and efficient** VPC-to-VPC communication in AWS. By following best practices, organizations can optimize cloud networking, enhance security, and ensure seamless multi-environment connectivity.

## 🤝 Contributing
Feel free to open an issue or submit a pull request if you have improvements or suggestions!

## 📧 Contact
For queries or collaborations, connect with me on **[LinkedIn](https://linkedin.com/in/vaishnavi-pangare)** or **GitHub**!

---
🔹 **Author:** Vaishnavi Pangare  
🔹 **GitHub:** https://github.com/Vaishnavi639
🔹 **License:** MIT
