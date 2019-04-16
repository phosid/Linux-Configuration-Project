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
14. Set permissions by running `chmod 700 .ssh` and `chmod 644 .ssh/authorized_keys`.
15. Back on your local machine, run `ssh grader@[YOUR_SERVERS_IP_ADDRESS] -p 22 -i ~.ssh/keyforgrader`. You must enter the public IP address after the @ sign for your server.
16. 
