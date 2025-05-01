# How to Deploy Applications on EC2 Instance

## Overview

A step-by-step guide to deploy web applications on Amazon EC2 instances.

## Step 1: Create an EC2 Instance

- Choose an EC2 name

![image.png](How%20to%20Deploy%20Applications%20on%20EC2%20Instance%201e67219e525c806ea3cec23bb554cc02/image.png)

- Select AMI → *Ubuntu Server 24.04* or *Amazon Linux 2*

![image.png](How%20to%20Deploy%20Applications%20on%20EC2%20Instance%201e67219e525c806ea3cec23bb554cc02/image%201.png)

- Choose Instance Type → *t2.micro (free tier)*
- Choose Key Pair → `demo-first-project.pem`
- Launch the instance and ensure it is in the **Running** state.

## Step 2: Connect to EC2 Instance

### **Using EC2 Console:**

1. Go to **AWS EC2 Dashboard** → **Instances**.
2. Select your running instance.
3. Click **Connect** (top right).
4. In the popup window, choose the **“SSH client”** tab.
5. AWS will show a command like this:

```bash

ssh -i "demo-first-project.pem" ubuntu@13.201.23.106

```

Open PowerShell (or any terminal on your PC).

![image.png](How%20to%20Deploy%20Applications%20on%20EC2%20Instance%201e67219e525c806ea3cec23bb554cc02/image%202.png)

1. Navigate to the folder where your `.pem` file is stored:

```bash

cd /c/Users/pushp/Downloads

```

Run the SSH command from step 5:

```bash

ssh -i "demo-first-project.pem" ubuntu@13.201.23.106

```

✅ You should now be logged into your EC2 instance.

📷 

![image.png](How%20to%20Deploy%20Applications%20on%20EC2%20Instance%201e67219e525c806ea3cec23bb554cc02/image%203.png)

## Step 3: Install and Configure HTTPD Web Server

```bash
# Install Apache web server
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2

```

## Step 4: Configure Security Group

- Navigate to EC2 Instance Security settings
- Edit Inbound Rules
- Add new rule:
    - Type: HTTP
    - Source: Anywhere
- Save rules

![image.png](How%20to%20Deploy%20Applications%20on%20EC2%20Instance%201e67219e525c806ea3cec23bb554cc02/image%204.png)

## Step 5: Deploy Application Files

From your local machine:

```bash
# Copy project files to EC2
scp -i path_to_key.pem -r path_to_project_folder ec2-user@ec2-instance-ip:/home/ec2-user/

# On EC2 instance, copy files to web server directory
sudo cp -r . /var/www/html/

# Restart web server
sudo systemctl restart httpd

```

[https://www.notion.so](https://www.notion.so)

![image.png](How%20to%20Deploy%20Applications%20on%20EC2%20Instance%201e67219e525c806ea3cec23bb554cc02/image%205.png)

## Step 6: Troubleshooting

<aside>
If CSS or styling isn't loading, set proper permissions:

</aside>

```bash
sudo chmod -R 755 /var/www/html/

```

## Important Notes

- Always keep your .pem key secure
- Ensure proper security group configurations
- Regularly monitor your EC2 instance