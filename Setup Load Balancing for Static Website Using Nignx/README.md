# Setup Load Balancing for Static Website Using Nignx

List of steps: 

1. Deploy three servers
2. Set up static websites on two servers using Nginx. Make a small change in the index.html file of one of the websites to differentiate between two servers.
3. Set up Nginx on the third server. It will act as a load balancer.
4. Configure Nginx to load and balance traffic between two static websites.
5. Add the Nginx Load balancer IP to the DNS A record.
6. Try accessing the website. Every time you reload the website you should see a different index.html.
7. Try different Nginx load-balancing algorithms and options.
8. Understand L7 load balancing.

## Deploy three servers

You can use any cloud service, such as AWS, Google Cloud, or Azure. In this project, I will use Google Cloud.

To deploy three servers, simply create three virtual machines (VMs) and and install an operating system on each one. In this project, I will use Debian 10 as the operating system.

![1695872643422](image/README/1695872643422.png)

As you can observe, I have created three server instances named `server-1`, `server-2` and `server-3`, each with its designated purpose:

1. `server-1` and `server-2`: These servers host two distinct websites.
2. `server-3`: It acts as a load balancer, distributing traffic to remain servers.
