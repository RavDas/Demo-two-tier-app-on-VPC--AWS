# Demo two tier app on VPC - AWS

This example demonstrates how to create a VPC that can be used for servers in a production environment. 

![image](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/cbea5b14-c9d0-4df1-be0f-f093deee91da)


The VPC has public and private subnets in two Availability Zones. Each public subnet contains a NAT gateway and a Load Balancer node. To improve resiliency, I deploy the servers in two Availability Zones using an Auto Scaling group and an Application Load balancer. 

For additional security, I deploy the servers in private subnets. The servers receive requests through the load balancer. The servers can connect to the internet by using a NAT gateway. 

To improve resiliency, I deploy the NAT gateway in both Availability Zones. Using a NAT gateway hides the IP address of the Application instance in the private subnet. If the application needs to access anything from outside(eg. API calling over the Internet) the NAT gateway will mask the IP of the Application instance. 


### Access AWS Console

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/801483be-15bb-4e9a-95ee-6ae83301c702" alt="1" width="600"/> 

On the dashboard, click on "Create VPC."

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/a506571f-d000-447e-8f20-573d65f05f96" alt="2" width="600"/>

Preview on the two tier architecture 

Above architecture is a default one provided by AWS when creating a VPC. Here in the VPC there are two public and private subnets respectively. And the public subnets are attached with one route table and private subnets are attached with another. 

Subnets should be attched with route tables. Route tables define how to handle the traffic within the subnets. After that public subnets have a destination called internet gateway via their route table that opens the subnets to the internet while private subnets are are destined to a VPC endpoint - S3 bucket. Instead of S3 bucket you can either choose any other endpoint or not.

Change the architecture according to your needs. Below is based on that.

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/07a6849e-b643-41a8-a2d6-4bc6ee25c194" alt="3" width="600"/>

### Configure VPC:

Select VPC and more 

Give VPC a name 

Use default settings for IPv4 CIDR block 

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/93175247-6257-4053-bf37-72951d6e3731" alt="4" width="600"/>

### Configure Subnets:

Choose to have VPC in two different Availability Zones for better reliability. 

Here we use two public and two private subnets for applications inside the VPC.

Set up one NAT gateway for each Availability Zone to ensure a more robust system.

If instances need to access an S3 bucket, choose the S3 Gateway option. This helps instances in your private subnet reach Amazon S3. It's cost-free, so you might as well keep this option enabled even if you're not currently using S3.

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/c62bbcb6-c58c-43ee-98df-da933ac6f427" alt="5" width="600"/>

Creation of the VPC Workflow

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/b5e6d3eb-6a48-4d78-a75b-1dad23d4413b" alt="6" width="600"/>

Created VPC Workflow Architecture 

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/ec895db5-bf36-45a8-9c02-f67f364e9ad9" alt="7" width="600"/>

## Creating Auto Scaling Groups

Go to EC2 instance >Auto Scaling

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/6b5c9733-753e-4a68-85db-8266b3da3579" alt="8" width="600"/>

Goto to Auto scaling Group

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/39b810e9-8107-4621-a902-5e8c16049ec1" alt="9" width="600"/>

Create launch instance template

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/76511b62-75bf-4354-b1c5-caa7b5802963" alt="10" width="600"/>

Create a template and with Ubuntu Image

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/f8cccc45-790a-47cd-a9db-60eb91e92709" alt="11" width="600"/>

Select Instance Type

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/5a51e8d5-017e-4eb9-883f-584bf530d76a" alt="12" width="600"/>

Create new key pair - use pem file format and save the key pair file locally. / Use a key pair earlier created.

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/ebc91651-472b-4a14-b971-9d473598500b" alt="13" width="600"/>

In Network Settings > Fill below details

Give a name for the Security Group

Note- select your created VPC here

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/25424af0-37ad-4e41-99ed-05e672c5ebb5" alt="14" width="600"/>

Setup Inbound Security Group Rules - Open port 8000 for the application and port 22 to ssh into the EC2 instance

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/bb1cd968-e9ba-4803-b966-91509d15f64e" alt="15" width="600"/>

### Auto Scaling Group 

Select Created launch Template

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/8817d089-fe9f-4874-8ef7-574e432050ad" alt="16" width="600"/>

Set Version as Default

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/796317a8-ab46-4612-b657-7a1af6721bdd" alt="17" width="600"/>

In the Network -> Select your created VPC and private subnets

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/e5af4027-7ebb-49d0-b403-a1c3a5bda8e1" alt="18" width="600"/>

In the Configured Advanced options page - We will attach a load balancer later

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/42cdf822-1362-4507-ae16-96b7cab5cc1d" alt="19" width="600"/>

Set Configure group size and scaling

Desired Capacity -Set 2

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/deb9c824-4693-4601-977a-21756bc0d86b" alt="20" width="600"/>

Scaling limits

* Min desired capacity- Set 1

* Max desired capacity - Set 4
  
<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/245ef6d5-2775-4c96-8556-58351ee9eaba" alt="21" width="600"/>

Automatic scaling - select No scaling policies

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/3205e037-4b0f-4b26-b8d6-9d9c3d43b439" alt="22" width="600"/>

Add notifications -set as default (optional)

Add tags-Set as default (optional)

Review and Create Auto scaling Group

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/4447d846-f836-4826-b4b4-412551627d2a" alt="24" width="600"/>

Auto scaling Group is created successfully

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/4dab2927-35b0-4e0b-93ce-2fba39d28a63" alt="25" width="600"/>

Now go to EC2 Dashboard -> Instances - Observe two instances are create in private subnet

Goto on Instance ID ,and observe private subnet

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/13c409e1-9c06-420e-9769-985f4cfb23eb" alt="26" width="600"/>

Go to second private subnet instance -observe subnet ID

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/b1f9b95c-9bdd-478d-adc2-a191128fbdab" alt="27" width="600"/>

### Install the application on Private subnet EC2 instance

As you observe there is no public IP address for two private instances. To access those instances we need to create bastion -host EC2 instances.

Create a Bastion Host 

* Go to the EC2 dashboard

* Go to instances -> Launch Instance
  
<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/8227d06a-80c8-49a3-958c-38052368c40f" alt="28" width="600"/>

Enter EC2 instance name here

![d](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/e7428ad0-3e1a-4abe-a5d7-3697ccba9969)

Choose an Ubuntu Image (AMI) for your Bastion host.

![a](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/ce5b7d1b-f926-405b-aafe-90fc301658a3)

Instance Type - t2.micro

Choose a key pair (aws-prod-example-keypair.pem)

![b](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/668b3f66-10f8-4d7f-984d-ccf37ab077f1)

Network settings->

* Select your created VPC

* Subnet -set as default

* Auto-assign public IP - Enable

* Create security group


![c](https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/9547bc45-920f-4bf2-8a46-e0737aeccc32)


Why a Bastion Host?

A Bastion host acts as a secure gateway, providing a controlled point of entry to your private subnet. This ensures that access to your sensitive resources is both monitored and safeguarded.

Now we need to securely copied our .pem file which is generated using key-pair creation into public instance (Bastion-host) using below command. Here your .pem file is needed to ssh into from one instance to another and for that .pem  file should be in both instances. So as my main intetion is to login to the private subnets via the bastion hosts, I need to have .pem file in my bastion-host as well. I have a copy in my local machine and I am going to copy it from my local machine to the bastion-host instance. (Or you can copy it from private instance to the bastion-host instance as well.)

Go to terminal ,and run below command

```
scp -i /home/raveen/Documents/.-keypair.pem /home/raveen/Documents/aws-prod-example-keypair.pem ubuntu@52.207.224.163:/home/ubuntu/

## scp -i <.pem file name> <source path> <target path>

```

Check the file is transferred successfully or not

```
ssh -i aws-prod-example-keeypair.pem ubuntu@52.207.224.163

### ssh -i <.pem file name> ubuntu@<bastion-host_ip>

```

Now lets connect ssh with private instance,

1.Go to Private subnet instances

2.Copy private ip address


<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/7494493a-7b7a-4962-b880-98814f8ed027" alt="a" width="600"/>

3.Run below command in terminal

```
ssh -i "aws-prod-example-keypair.pem" ubuntu@10.0.141.77

### ssh -i <pem file name> ubuntu@<ip address of private instance>
 
```
Now we have successfully connected private subnet using bastion-host

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/1f6e04c4-edf7-4904-ac5d-33cf834dca66" alt="b" width="600"/>



Now lets create Simple HTML file

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/44eb506c-2deb-408c-a70a-0549c2a86888" alt="c" width="600"/>

Run index.html file on port 8000 -> 

```
python3 -m http.server 8000
```

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/7ef03301-e74c-4abf-9d39-13abcb8a0d7e" alt="d" width="600"/>

### Creating an Application Load Balancer on AWS

Now go to EC2 Dashboard -> Click on Load Balancer

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/c01b8bc1-0b0e-4c0b-9dc6-8a9abb475504" alt="e" width="600"/>

Click on Create Load Balancer

Select Application Load Balancer -> Click on create

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/d6d9d766-24fc-46fd-8a60-1beb82d8e8c4" alt="f" width="600"/>

Now create Load Balancer,

1.Enter Load Balancer Name

2.Scheme-Set as default (Internet facing load balancer routes reponses from clients over the internet to target instances.)

3.IP address type - set as default (IPv4)

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/bc5795e5-0f80-480f-8164-9f009f723a78" alt="g" width="600"/>

Network Mapping

1.Select Created VPC earlier

2.Mapping - Select the two availability zones with their relavant public subnets cretaed earlier. (Load balancers are connected via the public subnets of the VPC. Load balancer should be in the public subnets of the VPC)

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/787029d8-3891-49f5-ae98-70745a4186c1" alt="h" width="600"/>

Security Groups - Select all three option (Select the necessary security group to control the traffic to the VPC to ensure necessary ports are open of the Load Balancer. YEven you can choose the only one group.)

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/d7182c16-6153-4abe-a3a9-744afbfc2edd" alt="i" width="600"/>

Listeners and routing 

We need to create a target group to define which private instances should be accessible for the Load Balancer.

Specify group details - Choose target type as Instances ( We need the Load Balancer for our private subnets / instances that host our application)

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/9dff422f-5b42-47f4-883a-6f9484bc8beb" alt="k" width="600"/>

Click on Create target group

Specify group Details

Choose a target type - Instances

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/833fd128-1fa5-45b9-97e0-1174e2dc1448" alt="a" width="600"/>

Enter target group name:aws-prod-example

Protocol :port - HTTP ,Enter port 8000 (We just need to run HTTP protocols only and we ran a simple HTML file on port 8000 of the private instance)

IP address type - IPv4

VPC - Selected the cretaed VPC

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/a9037fa0-53e3-4e48-8a39-d3adc92ecbb8" alt="b" width="600"/>

Health Check - Set Default

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/10503414-42a9-4b1b-b85a-a2e595aa2e92" alt="c" width="600"/>

Select the two private subnets / instances

Then click on "Include  as pending" and "Create target group"

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/f94f87c5-9d5a-4db1-9f48-d39fc94789bc" alt="d" width="600"/>

Target group creation is successful.

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/8b5c8c47-1953-4d05-ae73-a57cb86a95c7" alt="e" width="600"/>

After you have created a target group, then go to the "Listerns and routing" section again and add the newly created traget group - "aws-prod-example".

In the same section, choose the protocola as HTTP and port 80. (The port which we open for the Load Balancer. Make sure to open prot 80 of the chosen security groups when creating the Load Balancer to allow inbound traffic on port 80)

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/833fd128-1fa5-45b9-97e0-1174e2dc1448" alt="a" width="600"/>

Load Balancer is created successfully. Click on View Load Balancer to verify the creation

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/b79cb865-4d9f-458a-9739-c2d511536cdf" alt="e 1" width="600"/>

Click on Load Balancer name 

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/6f279936-9e91-46f4-931a-82554200a61f" alt="f" width="600"/>

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/1653990e-66a0-44b1-bb81-cbe16443502d" alt="g" width="600"/>

Listeners and rules - Select HTTP

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/8ec90f78-99c5-403a-bcf2-79bec3bcd385" alt="h" width="600"/>

Click on Security -> Select your created Security Group ID

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/3ce1430e-5e2c-4ca6-bbe5-61f6afa74593" alt="j" width="600"/>

Click on Edit Inbound Rule

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/1e3f02f4-0086-4e0a-9532-2c474ee6b72a" alt="k" width="600"/>

Add port 80 for HTTP traffic -> click on Save

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/6128345d-e9d5-4d9a-9b79-f5113e6bd87b" alt="l" width="600"/>

Go to Load Balancer - Copy DNS name ,and paste it in the browser

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/2f9357a0-9b53-41ad-93ef-93db4165cc24" alt="m" width="600"/>

### Test the Application 

Finally Application is deployed.

<img src="https://github.com/RavDas/Demo-two-tier-app-on-VPC--AWS/assets/86109995/4e6fa37b-2569-45fe-acda-e7ab828ce15f" alt="o" width="600"/>


