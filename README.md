# SSH-setup

![ssh-setup](https://github.com/user-attachments/assets/6695d345-d9f3-4643-a8d8-b9a2d9479f51)
SSH Server Setup Guide
Follow these steps to set up and secure your SSH server.

#Prerequisites

A Linux machine with sudo access.
An SSH client on your device (e.g., ssh on Linux/Mac or PuTTY on Windows).
Step 1: Install OpenSSH Server
Run these commands to install the SSH server:

sudo apt update
sudo apt install openssh-server -y

Enable and start the SSH service:

sudo systemctl enable ssh 
sudo systemctl start ssh

Confirm running

sudo systemctl status ssh

<------------------Optional security configuration ---------->

Step 2 : Secure the SSH Server

Editing the sshd_config File

Recommended Changes for the SSH Config File
Disable root login: PermitRootLogin no
Change default port(on server side preference) : Port 2222
Allow certain users: AllowUsers your-username

Save the edited file and reboot the service

sudo systemctl restart ssh

Step 3: Firewall Configuration

sudo ufw allow ssh

sudo ufw allow 2222/tcp

sudo ufw enable

<-------------------------->

Step:  Connect to the Server

Use an SSH client to connect:

ssh your-username@server-ip-address

If you changed the port:

ssh -p 2222 your-username@server-ip-address

<-------Optional: Key-Based Authentication--------------->

Generate a key pair locally:

ssh-keygen -t rsa

Copy the public key to the server:

ssh-copy-id your-username@server-ip-address

Disable password authentication in /etc/ssh/sshd_config:


PasswordAuthentication no

Restart the SSH service:

sudo systemctl restart ssh
Troubleshooting
SSH service not running: Start it with sudo systemctl start ssh.
Firewall Blocking access: Check the allowed port using the command sudo ufw status.
Authentication Failure: Check your username, password or key configuration .
<----------------------------------------->
