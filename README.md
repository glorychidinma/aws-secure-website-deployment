# Deploying a Secure Website on AWS EC2 with Custom Domain and SSL/TLS

## Project Overview

This project demonstrates how I deployed a production-like website on an AWS EC2 instance using Nginx, connected a custom domain from Namecheap, and secured the website with Let’s Encrypt SSL/TLS.

The goal of this project was to gain hands-on experience in cloud computing, networking, and web security by implementing a real-world deployment workflow.


## Tools & Technologies 

- Amazon Web Services (AWS EC2)
- AWS VPC (Virtual Private Cloud)
- Ubuntu Linux
- MobaXterm (SSH Client)
- Nginx Web Server
- Let’s Encrypt (Certbot)
- Namecheap (Domain & DNS Management)
- Git & GitHub


## Architecture Overview

This project follows a simple cloud architecture:

**User → Internet → AWS VPC → EC2 Instance → Nginx → HTTPS (SSL/TLS)**


## Step-by-Step Implementation

###  Step 1: VPC Setup

- Used the default VPC provided by AWS
- Deployed the EC2 instance in a public subnet
- Used the default Internet Gateway for internet access
- Used default route table for inbound and outbound traffic
- No custom VPC configuration was required for this deployment


### step 2: EC2 Instance Setup

- Launched an EC2 instance (ubuntu)
- Enabled inbound security group rules:
    - Port 22 (SSH)
    - Port 80 (HTTP)
    - Port 443 (HTTPS)

    
### step 3: SSH Connection via MobaXterm

- Opened MobaXterm
- Clicked **Session**
- Selected **SSH**
- Entered EC2 Public IP
- Username: `ubuntu` (or `ec2-user` depending on AMI)
- Imported the private key file (.pem) generated during EC2 setup
- Clicked **Connect**

Successfully connected to the EC2 instance via SSH.


### Step 4: Install Nginx (Web Server)

- I began by updating and upgrading the server to ensure all system packages were current and secure.

After that, I installed Nginx as the web server to host my application.

Run the following commands:

sudo apt update && sudo apt upgrade -y
sudo apt install nginx -y
sudo systemctl status nginx

- To confirm that Nginx was installed and running correctly, I opened my browser and accessed my EC2 instance using its public IP address.

  http://54.167.41.128

If configured properly, this displays the default “Welcome to Nginx” page, confirming that the web server is active and serving content successfully.


### step 5: Deploy Website

- Clone the project repository from github

Run the following commands:

git clone https://github.com/digitalwitchdemo/mediplus.git
cd mediplus
ls


- Move Files to Nginx Directory

sudo mv ./* /var/www/html/

cd /var/www/html/

ls


- verify deployment
   - visit : http://54.167.41.128
   - Confirmed that the website is live and accessible.


### Step 6: Domain Setup (Namecheap)

a. Configure Domain

- Purchased a domain from Namecheap and configure it (e.g. glorychidinmaotulu.online).
- Log in to Namecheap
- Go to **Domain List**
- Click **Manage**
- Add DNS records


b. DNS Records

**A Record**

- Host: `@`
- Value: `<EC2 Public IP>`
- TTL: Automatic

**CNAME Record**

- Host: `www`
- Value: `glorychidinmaotulu.online`
- TTL: Automatic


  This connects:
    - `glorychidinmaotulu.online`
    - `www.glorychidinmaotulu.online`

to my server.


### Step 7: DNS Propagation Check

- After configuring my DNS records, I verified that the changes had propagated globally using DNSChecker.

I entered my domain name into the DNSChecker search bar and confirmed that it was resolving correctly across multiple locations worldwide.


- Live Website Verification:

Once propagation was successful, I accessed my website:

 http://glorychidinmaotulu.online

- The site loaded successfully, confirming that my domain was properly connected to the EC2 server and that the web server was functioning as expected.




