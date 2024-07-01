# Demo-two-tier-app-on-VPC--AWS

This example demonstrate how to cretae a VPC that can use for servers in a production environment.

![image](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/e7f8ab91-1ee8-4597-a5ea-96897e74c45f)

The VPC has public and private subnets in two Availability Zones. Each public subnet contains a NAT gateway and a load balancer node. To improve resilency, I deploy the servers in two Avilability Zones, by using an Auto Scaling group and an Application Load balancer. For additional security, I deploy the servers in a private subnets. The servers receive requests through the load balancer. The servers can connect to the internet by using a NAT gateway. To improve resilency, I deploy the NAT gateway in both Availability Zones.

/home/raveen/Pictures/28.png
/home/raveen/Pictures/27.png
/home/raveen/Pictures/26.png
/home/raveen/Pictures/25.png
/home/raveen/Pictures/24.png
/home/raveen/Pictures/23.png
/home/raveen/Pictures/22.png
/home/raveen/Pictures/21.png
/home/raveen/Pictures/20.png
/home/raveen/Pictures/19.png
/home/raveen/Pictures/18.png
/home/raveen/Pictures/17.png
/home/raveen/Pictures/16.png
/home/raveen/Pictures/15.png
/home/raveen/Pictures/14.png
/home/raveen/Pictures/13.png
/home/raveen/Pictures/12.png
/home/raveen/Pictures/11.png
/home/raveen/Pictures/10.png
/home/raveen/Pictures/9.png
/home/raveen/Pictures/8.png
/home/raveen/Pictures/7.png
/home/raveen/Pictures/6.png
/home/raveen/Pictures/5.png
/home/raveen/Pictures/4.png
/home/raveen/Pictures/3.png
/home/raveen/Pictures/2.png
/home/raveen/Pictures/1.png
