# Setup Multiple Static Websites on a Single Server Using Nginx Virtual Hosts

Nginx web server can host multiple websites on a single server using its server blocks feature.

The main purpose of this project is to make two websites with two subdomains of the `devopsproject.top` domain name and host both of them in the server that we created in "**Setup A Static Website Using Nginx**" project. Here is the list of steps:

1. Create two subdomains
2. Install and configure Nignx on a server
3. Create two website directories with two different website templates.
4. Configure the Virtual host to point two subdomains to two different website directories.
5. Add the IP of the server as A record to the two subdomains.
6. Validate the setup accessing the subdomains.
7. Create a wildcard Letsencrypt SSL certificate for the root Domain.
8. Configure wildcard SSL on Nginx for two websites.
9. Validate the subdomain websites’ SSL using OpenSSL utility.

In this project, I assume that you have completed the "**Setup A Static Website Using Nginx**" project. Before proceeding with the following steps, please make sure that you have read all of the steps for setting up Ubuntu server and Nginx web server, including creating a virtual machine, installing Ubuntu Server, configuring both server and firewall, installing Nginx, and configuring Nginx.

Now, let's dive into this project! 🔥🔥🔥

## Create two subdomains
