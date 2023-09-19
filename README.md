# Setup A Static Website Using Niginx Project

This project marks my inaugural self-guided DevOps project, encompassing a step-by-step process for establishing a website. The project entails:

- Setting up an Ubuntu Server.
- Accessing the server securely via SSH protocol and configuring the server.
- Initiating firewall rules for enhanced security.
- Installing and deploying Nginx as a web server.
- Transferring website files (including .html, .css, .js, etc.) to the Nginx /var/www/ directory using SCP (Secure Copy Protocol).
- Registering a DNS (Domain Name System) account and associating the server's external IP address with a domain name.
- Leveraging Nginx's Server Block feature to host multiple websites on a single IP address.
- Accquiring a Let's Encrypt certificate to enable SSL encrytion for the hosted websites.

This project serves as an educational exercise, covering various aspects of web hosting and server management within a DevOps context.

## Setting up a ubuntu server

The purpose of this step is to deploy a Virtual Machine on a cloud platform, and in this project, Google Cloud is utilized. Following that, we will set up the Ubuntu Server operating system on this virtual machine.

![1695092965829](image/README/1695092965829.png)

## Accessing the server securely via SSH protocol and configuring the server

##### Accessing the server

To accessing the server, there are several ways:

* using [SSH-in-Browser](https://cloud.google.com/compute/docs/ssh-in-browser) from the Google Cloud console.
* using SSH by running the [`gcloud compute ssh` command](https://cloud.google.com/sdk/gcloud/reference/compute/ssh).
* using SSH from an OpenSSH client (I prefer this way).
* using SSH from the Windows PuTTY app (If your operating system is Window).

Since my computer is currently running Ubuntu (22.04.3 LTS), which supports SSH connections natively, we only need to generate an SSH key pair (public key, private key) with the following command:

```plaintext
ssh-keygen -t rsa
```

Keep the private key on your computer and insert the public key into the Virtual machine you created in the previous step.

Now, access the server using the following command:

```
ssh <server_external_IP>
```

During the first-time connection, you might receive a warning, but don't worry; simply type 'yes'. Afterward, you should be able to connect to the server succesfully.

##### Configuring the server

Next, it's essential to create a new user that have many administrative privileges to facilitate various tasks while minimizing security risk. This user is commonly referred to as a non-root user.

Here's how you can create a non-root user:

First, use the following command to add a new user, replacing `<username>` with your chosen username:

```php
sudo adduser <username>
```

After adding the new user, exit the current SSH connection session:

```bash
exit
```

Reconnect to the server using the new username and the server's external Ip address:

```bash
ssh <new_username>@<server_external_IP>
```

## Initializing firewall rules for enhanced security.

To implement restricted access to specific services on our server, we can employ the UFW (Uncomplicated Firewall) to manage and control access. In this context, we will configure UFW to permit access to OpenSSH, which is the service we utilize for connecting to the server.

To identify the services that have their profiles registered with UFW, we can execute the following command:

```
sudo ufw app list
```

To instruct the firewall to allow SSH connections, use the following command:

```
sudo ufw allow OpenSSH
```

Once OpenSSH access has been granted, we can activate the firewall using the enable command:

```
sudo ufw enable
```

When prompted, confirm the action by entering `y` to complete the process. To check the current status of the firewall, you can use the following command:

```
sudo ufw status
```

## Installing and deploying Nginx as a web server.

To begin the installation of Nginx using the `apt` package manager, it's essential to refresh the local package cache by checking the configured software repositories for any updates or new packages. To perform this update, use this following command:

```
sudo apt update
```

Afterward, install Nginx by a single command using `apt` package:

```bash
sudo apt install nginx
```

Once the process of installing Nginx complete, configure the firewall again to enable Ngix service in the firewall configuration.

Let's see the list of available application that have their profiles registerd with UFW

```
sudo ufw app list
```

Enable the option "Nginx Full" by the following command. The firewall will enable traffic through port `:80` and `:443` immediately

```
sudo ufw allow 'Nginx Full'
```

To manage Nginx service, use following commands:

```
// Start (activate)
sudo systemctl start nginx

// Restart (Start or restart)
sudo systemctl restart nginx

// Stop (deactivate)
sudo systemctl stop nginx

// Reload (without losing connection)
sudo systemctl reload nginx

// Enable Nginx service so that it starts automatically at boot time
sudo systemctl enable nginx

// Disable Nginx service, preventing it from starting automatically at boot time
sudo systemctl disable nginx
```

To see the status of Nginx service, use the following command:

```
systemctl status nginx
```

Now, open your browser and enter the external IP of your server. If you see something like this, congratulation!

![1695108016796](image/README/1695108016796.png)

## Transferring website files (including .html, .css, .js, etc.) to the Nginx /var/www/ directory using SCP (Secure Copy Protocol).
