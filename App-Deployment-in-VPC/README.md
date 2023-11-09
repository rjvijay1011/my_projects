**Application deployment within a VPC(Virtual Private Cloud)**


1. The idea here is we are going to create a VPC(Highly secured isolated virtual private cloud environment) which comes with a size of 65,536 IPs(varies). In which we are going to create a public subnet and a private subnet (Subnet is nothing but a list of IP ranges).
2. We are going to deploy our application in an EC2 instance which is inside a private subnet. Since, security is our primary concern we won’t be having a public IP enabled for this instance.
3. In the public subnet we will be having an EC2 instance, which is called jump server/Bastion server.
We will login to that Jump server using its Public IP and then from there I will SSH to the private IP of my instance which is inside the private subnet where my application will be deployed.
4. There are few components that are used in the architecture: Internet Gateway, NAT Gateway, Application Load Balance(ALB), Auto Scaling group(ASG), Security Group(SG) & NACL(Network Access Control List - Not used but can be used).
* Internet Gateway : Through which the user will access the application.
* NAT Gateway : If my application inside the private subnet wants to access or download a few packages from the internet, then NAT Gateway helps me in accessing the internet and at the same time masks the IP address of my private instance. So that the IP address won't be exposed to hackers.
* ALB : distributes the incoming traffic/load across the instances.
* ASG : This is used to scale in(remove)/scale out(add) EC2 instances based on the Demand/Load.
* SG : Acts as a Firewall at the instance level.
* NACL : Acts as a Firewall at the subnet level.
* Target Groups : Within the ALB there will be a target group, which will route the requests to individual targets(EC2) using the protocol & port.
* Route Table : It displays where the traffic is directed.

Things to keep in mind, private subnets will only have the EC2 instance where the application is hosted. Public subnet will have jump server, ALB & NAT gateway

Note : 
1. For High Availability, we are doing this deployment on multiple AZs(Availability Zones).
2. I am launching my EC2’s within the Auto-scaling group as I want to scale in/scale out the EC2 instances to handle the incoming load.
3. VPC is spread across multiple AZs but public & private subnets are restricted to a specific AZ.
