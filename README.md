# 🛡️ Secure AWS Web Architecture with WAF Blocking Demo

This project demonstrates how to set up an **AWS Web Architecture** that **blocks traffic from specific IP addresses** using **AWS WAF**, while routing allowed traffic through an **Application Load Balancer (ALB)** to an **EC2 Instance** hosted in a **Public Subnet**.

---

## 📌 Architecture Diagram

```
USER (Laptop IP)
    │
    ▼
❌ AWS WAF (Blocks Specific IPs e.g., your laptop IP)
    │
    ▼
✅ Application Load Balancer
    │
    ▼
✅ EC2 Instance (Public Subnet in VPC)
```
![ScreenRecording2025-04-09at07 59 33-ezgif com-video-to-gif-converter](https://github.com/user-attachments/assets/da49e3d5-305a-4e26-846c-7bbd26852ea3)


---

## 🎯 Objective

To demonstrate the **403 Forbidden** response using AWS WAF by explicitly **blocking the laptop IP address** used to access the application.

---

## 🧰 Components Used

| Service            | Description                                      |
|--------------------|--------------------------------------------------|
| **AWS WAF**         | Blocks incoming requests based on rules (e.g., IP) |
| **Application Load Balancer** | Distributes incoming traffic                |
| **EC2 Instance**    | Hosts the web application                        |
| **VPC with Public Subnet** | Network layer for deploying EC2 securely     |

---

## ⚙️ Step-by-Step Setup

### 1. ✅ Create a VPC and Public Subnet

- Create a VPC with CIDR `10.0.0.0/16`
- Add a public subnet (e.g., `10.0.1.0/24`)
- Attach an Internet Gateway
- Add routes for internet access

### 2. ✅ Launch an EC2 Instance

- Amazon Linux 2 or Ubuntu
- Install a simple web server (`nginx`, `httpd`, or Flask app)
- Open **port 80** (HTTP) and **port 22** (SSH) in the Security Group

```bash
sudo yum install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
```

### 3. ✅ Set Up an Application Load Balancer (ALB)

- Create a **Target Group**
- Register the EC2 instance
- Create an ALB with a listener on **port 80**
- Forward traffic to the target group

### 4. ❌ Create a WAF Web ACL

- Go to AWS WAF → Create Web ACL
- Add a rule to **block your laptop IP address**

Example Rule (Block IP Set):
```text
IP Set: MyLaptopIPBlockList
IP Address: <Your Laptop IP>/32
Action: Block
```

- Associate the WAF Web ACL with the ALB

---

## 🔪 Demo: Trigger 403 Forbidden

1. Access your **ALB DNS URL** from your **laptop browser**
2. AWS WAF detects your IP and returns:

```text
403 Forbidden
```

3. Try from another IP (VPN or mobile hotspot), and it works fine.

---

## 🔒 Real-World Use Cases

- Block malicious users by IP
- Prevent access from specific regions
- Allow internal traffic while blocking external access
- Integrate with CloudWatch for real-time alerts

---

## 📌 Notes

- To find your current IP:
  ```bash
  curl https://checkip.amazonaws.com
  ```
- You can modify the IP set to allowlist instead of blocklist for different scenarios.

---

## 🧑‍💻 Author

**Ambati Bhargavi**  
🌐 [GitHub](https://github.com/ambatibhargavi) | 📨 ambatibhargavi977@gmail.com

<img width="1209" alt="Screenshot 2025-04-10 at 15 03 39" src="https://github.com/user-attachments/assets/39ba45bf-02e9-4369-bc72-48cf42d603c5" />
<img width="1247" alt="Screenshot 2025-04-10 at 15 03 22" src="https://github.com/user-attachments/assets/f9317f7b-fc9b-46e7-975a-c1ed1aa5d3c2" />
<img width="911" alt="Screenshot 2025-04-10 at 15 00 49" src="https://github.com/user-attachments/assets/9710e881-cc40-46b3-9796-3f5da3bab2ae" />
<img width="1238" alt="Screenshot 2025-04-10 at 14 10 41" src="https://github.com/user-attachments/assets/c0b3c95b-c7ee-42b1-9495-741ed55e619b" />
<img width="724" alt="Screenshot 2025-04-10 at 15 09 45" src="https://github.com/user-attachments/assets/5e37a11c-b984-4df8-88aa-03dd3fc0fafa" />



