# Demo-two-tier-app-on-VPC--AWS

This example demonstrate how to cretae a VPC that can use for servers in a production environment.

![image](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/e7f8ab91-1ee8-4597-a5ea-96897e74c45f)

The VPC has public and private subnets in two Availability Zones. Each public subnet contains a NAT gateway and a load balancer node. To improve resilency, I deploy the servers in two Avilability Zones, by using an Auto Scaling group and an Application Load balancer. For additional security, I deploy the servers in a private subnets. The servers receive requests through the load balancer. The servers can connect to the internet by using a NAT gateway. To improve resilency, I deploy the NAT gateway in both Availability Zones.
