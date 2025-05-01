# How to Deploy Applications on EC2 Instance

## Overview

A step-by-step guide to deploy web applications on Amazon EC2 instances.

## Step 1: Create an EC2 Instance

- Choose an EC2 name


- Select AMI → *Ubuntu Server 24.04* or *Amazon Linux 2*


- Choose Instance Type → *t2.micro (free tier)*
- Choose Key Pair → `demo-first-project.pem`
- Launch the instance and ensure it is in the **Running** state.

## Step 2: Connect to EC2 Instance

### Using EC2 Console:

1. Go to **AWS EC2 Dashboard** → **Instances**.
2. Select your running instance.
3. Click **Connect** (top right).
4. In the popup window, choose the **“SSH client”** tab.
5. AWS will show a command like this:

```bash
ssh -i "demo-first-project.pem" ubuntu@13.201.23.106
```

Open PowerShell (or any terminal on your PC):

```bash
cd /c/Users/pushp/Downloads
```

Run the SSH command:

```bash
ssh -i "demo-first-project.pem" ubuntu@13.201.23.106
```

✅ You should now be logged into your EC2 instance.


## Step 3: Install and Configure Apache Web Server

```bash
# Update package index
sudo apt update

# Install Apache
sudo apt install apache2 -y

# Start Apache service
sudo systemctl start apache2

# Enable Apache to start on boot
sudo systemctl enable apache2
```

## Step 4: Configure Security Group

- Navigate to EC2 Instance **Security settings**
- Edit **Inbound Rules**
- Add new rule:
  - Type: HTTP
  - Source: Anywhere (0.0.0.0/0)
- Save rules


## Step 5: Deploy Application Files

From your local machine:

```bash
# Copy project files to EC2 instance
scp -i path_to_key.pem -r path_to_project_folder ubuntu@13.201.23.106:/home/ubuntu/

# On EC2 instance, copy files to web server directory
sudo cp -r /home/ubuntu/project_folder/* /var/www/html/

# Restart web server
sudo systemctl restart apache2
```


## Step 6: Troubleshooting

If CSS or static assets aren't loading, set proper permissions:

```bash
sudo chmod -R 755 /var/www/html/
## Important Notes

- Always keep your `.pem` key secure
- Ensure your EC2 security group allows necessary ports (e.g., SSH, HTTP)
- Regularly monitor and maintain your EC2 instance



👉 For a detailed tutorial with screenshots, visit the Notion page: [https://www.notion.so](https://www.notion.so)



### 🔥 **What to do next:**

✅ Place your exported images in a `/media/` folder inside your repo (or update the image paths if hosted elsewhere).  
✅ Save this as `README.md` in your GitHub repository root.

Let me know if you'd like me to **adjust headings, tone, or formatting** further!