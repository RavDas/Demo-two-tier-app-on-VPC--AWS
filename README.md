# Demo-two-tier-app-on-VPC--AWS

This example demonstrates how to create a VPC that can be used for servers in a production environment.

![image](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/e7f8ab91-1ee8-4597-a5ea-96897e74c45f)

The VPC has public and private subnets in two Availability Zones. Each public subnet contains a NAT gateway and a Load Balancer node. To improve resiliency, I deploy the servers in two Availability Zones using an Auto Scaling group and an Application Load balancer. For additional security, I deploy the servers in private subnets. The servers receive requests through the load balancer. The servers can connect to the internet by using a NAT gateway. To improve resiliency, I deploy the NAT gateway in both Availability Zones. Using a NAT gateway hides the IP address of the Application instance in the private subnet. If the application needs to access anything from outside(eg. API calling over the Internet) the NAT gateway will mask the IP of the Application instance.


![1](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/801483be-15bb-4e9a-95ee-6ae83301c702)
![2](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/a506571f-d000-447e-8f20-573d65f05f96)
![3](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/07a6849e-b643-41a8-a2d6-4bc6ee25c194)

![4](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/93175247-6257-4053-bf37-72951d6e3731)
![5](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/c62bbcb6-c58c-43ee-98df-da933ac6f427)
![6](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/b5e6d3eb-6a48-4d78-a75b-1dad23d4413b)
![7](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/ec895db5-bf36-45a8-9c02-f67f364e9ad9)
![8](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/6b5c9733-753e-4a68-85db-8266b3da3579)
![9](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/39b810e9-8107-4621-a902-5e8c16049ec1)
![10](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/76511b62-75bf-4354-b1c5-caa7b5802963)
![11](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/f8cccc45-790a-47cd-a9db-60eb91e92709)
![12](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/5a51e8d5-017e-4eb9-883f-584bf530d76a)
![13](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/ebc91651-472b-4a14-b971-9d473598500b)
![14](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/25424af0-37ad-4e41-99ed-05e672c5ebb5)
![15](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/bb1cd968-e9ba-4803-b966-91509d15f64e)
![16](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/8817d089-fe9f-4874-8ef7-574e432050ad)
![17](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/796317a8-ab46-4612-b657-7a1af6721bdd)
![18](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/e5af4027-7ebb-49d0-b403-a1c3a5bda8e1)
![19](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/42cdf822-1362-4507-ae16-96b7cab5cc1d)
![20](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/deb9c824-4693-4601-977a-21756bc0d86b)
![21](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/245ef6d5-2775-4c96-8556-58351ee9eaba)
![22](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/3205e037-4b0f-4b26-b8d6-9d9c3d43b439)
![23](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/fd6aaf5b-e257-4adf-aa2e-ce6de1b09698)
![24](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/4447d846-f836-4826-b4b4-412551627d2a)
![25](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/4dab2927-35b0-4e0b-93ce-2fba39d28a63)
![26](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/13c409e1-9c06-420e-9769-985f4cfb23eb)
![27](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/b1f9b95c-9bdd-478d-adc2-a191128fbdab)
![28](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/8227d06a-80c8-49a3-958c-38052368c40f)
