# Linux-Configuration-Project
## Project Description
This is the final project for Udacity Full Stack Web Development program. In this project, I take a baseline installation of a Linux server and prepare it to host web applications. I also secure the server from a number of attack vectors, install and configure a database server, and deploy one of my existing web applications onto it.

- IP-Address: 54.189.211.121
- Accessible SSH port: 2200
- URL: http://54.189.211.121.xip.io/

## Walkthrough of software packages installed and configuration changes made:
1. In this project, I used Amazon Lightsail for a publicly accessible Ubuntu Linux Server to host the web application. I made an account with Amazon Web Services(AWS) and created a Lightsail Instance, selecting the "OS only" option and "Ubuntu 16.04 LTS". I kept the instance with its default name. As long as you delete the instance within one month, you should not be charged.
2. Once the instance is created, we'll first connect via SSH through the browser by clicking on "Connect using SSH".
3. run `sudo apt-get upgdate` to make server aware of updates.
4. run `sudo apt-get upgrade` to upgrade software.
5. run `sudo apt-get autoremove` to remove software no longer required.
6. run `sudo apt-get install finger` to install finger software; with this software, you can run `finger [username]`(for example, `finger ubuntu`) to find more details about a particular user.
7. run `sudo adduser grader` to make a user named `grader`.
8. run `sudo nano /etc/sudoers.d/grader` to create file and type in `grader ALL=(ALL) NOPASSWD:ALL`. Save file. This step grants `grader` user the ability to use the `sudo` command.
9. run `su grader` to switch user to grader. Under grader, we will set up a public key authentication method so we can use our terminal to login to the linux server from now on.
10. On the local machine, open the terminal and run `ssh-keygen` to generate a key pair. It is recommended you save it under the default directory and change the file name (the last portion of the path). I will save mine as `/Users/Phosid/.ssh/keyforgrader/`.
11. Connect back to SSH using the browser. Once the key pairs are generated, we need to update the server with the `.pub` key. run `mkdir .ssh` within your home directory and create a new file by running `touch .ssh/authorized_keys`.
12. Back on your local machine, read the contents of the .pub file (public key) by running the `cat` command. Copy the public key.
13. run `sudo nano .ssh/authorized_keys` and paste the contents of the public key into the file. Save the file.
14. Set permissions by running `chmod 700 .ssh` and `chmod 644 .ssh/authorized_keys`. run `sudo service ssh restart` to apply changes.
15. Back on your local machine, run `ssh grader@[YOUR_SERVERS_IP_ADDRESS] -p 22 -i ~.ssh/keyforgrader`. You must enter the public IP address after the @ sign for your server. This will log you into your server from your local machine's terminal. If you set a password when you created the ssh key pair, it will prompt you to enter the password.
16. On the server, run `sudo nano /etc/ssh/sshd_config`.
17. Change `PasswordAuthentication yes` to `PasswordAuthentication no`, `Port 22` to `Port 2200`, and `PermitRootLogin prohibit-password` to `PermitRootLogin no`. These changes will force key-based authentication, change the server port to 2200 (so you will use -p 2200 to login now), and disable remote login for the root user.
18. run `sudo ufw default deny incoming` to block all incoming requests.
19. run `sudo ufw default allow outgoing` to allow outgoing requests.
20. run `sudo ufw allow ssh`, `sudo ufw allow ntp` (port 123), `sudo ufw allow www` (port 80), and `sudo ufw allow 2200/tcp`.
21. Just in case, add custom rules to your firewall under the networking tab on the AWS website.
22. run `sudo ufw enable` to enable firewall.
23. Install Apache by running `sudo apt-get install apache2`.
24. Install mod_wsgi by running `sudo apt-get install libapache2-mod-wsgi`.
25. Enable mod_wsgi with `sudo a2enmod wsgi`.
26. Start apache with `sudo service apache2 start`.
27. Install git with `sudo apt-get install git`.
28. Run `cd /var/www` and create a new folder with `sudo mkdir catalog`. Change the owner of the catalog folder using `sudo chown -R grader:grader catalog`.
29. In `/var/www/catalog`, run `git clone https://github.com/phosid/Item-Catalog-Project` to clone your catalog project. *Replace my link with your link.
30. In the same folder containing the copied items, run `sudo nano catalog.wsgi` and add the follow text:
`#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/FlaskApp/")

from FlaskApp import app as application
application.secret_key = 'Add your secret key'`
31. 
