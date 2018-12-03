# Linux Server Configuration

## About

This is the sixth project for the Udacity Full Stack Nanodegree. This project involves taking a baseline installation of Linux on a virtual machine and preparing it to host web applications. This includes installing updates, securing the server from attacks, and installing / configuring web and database servers.


# Server Info

- **Public IP:** 159.89.17.50
- **SShPort:** 2200

- http://159.89.17.50

## Getting Started

This project uses [Digitalocean] to create a Linux server instance.


1. Secure the server.

    - Update all currently installed packages.
    
            sudo apt-get update
            sudo apt-get upgrade
            
    - Change the SSH port from 22 to 2200.
    
            Edit the file `/etc/ssh/sshd_config` and change the line `Port 22` to:

`Port 2200`

Then restart the SSH service:

`sudo service ssh restart`

        
        
    - Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).
        
            sudo ufw allow 2200/tcp
            sudo ufw allow 80/tcp
            sudo ufw allow 123/tcp
            sudo ufw enable

        ## Set-up SSH keys for user grader
As root user do:
```
mkdir /home/grader/.ssh
chown grader:grader /home/grader/.ssh
chmod 700 /home/grader/.ssh
cp /root/.ssh/authorized_keys /home/grader/.ssh/
chown grader:grader /home/grader/.ssh/authorized_keys
chmod 644 /home/grader/.ssh/authorized_keys
```

2. Give grader access.

## Add user and set a password
Add user `grader` with command:

```
useradd -m -s /bin/bash grader
```

Set a password for the user (you need this when running the `sudo` command) with:

```
passwd grader
```

## Add user grader to sudo group
Assuming your Linux distro has a `sudo` group (like Ubuntu 16.04), simply add the user to
this admin group:
```
usermod -aG sudo grader
```
you can access server by
```
ssh -i ~/.ssh/id_rsa grader@159.89.17.50 -p 2200
```

3. Prepare to deploy  project.

    - Configure the local timezone to UTC.
    
            `sudo timedatectl set-timezone UTC`
            
            
    - Install and configure Apache to serve a Python mod_wsgi application.
    
        ngnix is used instead of Apache
        
        configuration steps can be found here 
        
        https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uwsgi-and-nginx-on-ubuntu-16-04
        




. Deploy the Item Catalog project.

    http://159.89.17.50
    
## Resources


https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uwsgi-and-nginx-on-ubuntu-16-04

https://help.ubuntu.com/community/PostgreSQL
