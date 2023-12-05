# Create Subnets and Allocate IP addresses in an Amazon Virtual Private Cloud (Amazon VPC)

Create Subnets and Allocate IP addresses in an Amazon Virtual Private Cloud (Amazon VPC)

TOOLS
CIDR Calculator
https://www.subnet-calculator.com/cidr.php
Subnet Calculator
 https://www.subnet-calculator.com/ 
Guide
 https://datatracker.ietf.org/doc/html/rfc1918

BEST PRACTICE
Hosts within enterprises that use IP can be partitioned into three categories:

      Category 1: hosts that do not require access to hosts in other
                  enterprises or the Internet at large; hosts within
                  this category may use IP addresses that are
                  unambiguous within an enterprise, but may be
                  ambiguous between enterprises.

      Category 2: hosts that need access to a limited set of outside
                  services (e.g., E-mail, FTP, netnews, remote login)
                  which can be handled by mediating gateways (e.g.,
                  application layer gateways). For many hosts in this
                  category an unrestricted external access (provided via IP connectivity) may be unnecessary and even
                  undesirable for privacy/security reasons. Just like
                  hosts within the first category, such hosts may use
                  IP addresses that are unambiguous within an
                  enterprise, but may be ambiguous between
                  enterprises.

      Category 3: hosts that need network layer access outside the
                  enterprise (provided via IP connectivity); hosts in
                  the last category require IP addresses that are
                  globally unambiguous.


## OBJECTIVES

Summarize the customer scenario
Create a Amazon Virtual Private Cloud (Amazon VPC) and understand how to create subnets and allocate IP addresses
Familiarize yourself with the Amazon Web Services (AWS) Management Console
Develop a solution to the customer’s issue in this lab
Summarize and describe your findings.

SCENARIO
Your role is a cloud support engineer at AWS. During your shift, a customer from a startup company requests assistance regarding a networking issue within their AWS infrastructure. The following is the email and an attachment regarding their architecture:

TICKET FROM YOUR CUSTOMER
Hello, Cloud Support!

I’m new to AWS, and I need help setting up a VPC. Can you please help me through the setup process? I would like to build only the VPC part and would like to make it look something like the following picture. Can you help me ensure I have around 15,000 private IP addresses in this VPC available? I would also like the VPC IPv4 CIDR block to be a 192.x.x.x. I don’t remember which is a private range though. Can you confirm that? I would also like to allocate at least 50 IP addresses for the public subnet.

Thanks! Paulo Santos Startup Owner

CUSTOMER DIAGRAM
The customer's VPC architecture, which consists of a VPC that requires 15,000 IP addresses, an internet gateway, and a public subnet that requires 50 IP addresses

Figure: In the customer’s VPC architecture, the customer needs approximately 15,000 IP addresses for their Seattle office headquarters and 50 IP addresses for their operations department, which will be in the public subnet.

AWS SERVICE RESTRICTIONS
In this lab environment, access to AWS services and service actions might be restricted to the ones that you need to complete the lab instructions. You might encounter errors if you attempt to access other services or perform actions beyond the ones that this lab describes.

Start lab
To launch the lab, at the top of the page, choose Start lab.
 You must wait for the provisioned AWS services to be ready before you can continue.

To open the lab, choose Open Console.
You are automatically signed in to the AWS Management Console in a new web browser tab.

 Do not change the Region unless instructed.

COMMON SIGN-IN ERRORS
Error: You must first sign out


If you see the message, You must first log out before logging into a different AWS account:

Choose the click here link.
Close your Amazon Web Services Sign In web browser tab and return to your initial lab page.
Choose Open Console again.
Error: Choosing Start Lab has no effect
In some cases, certain pop-up or script blocker web browser extensions might prevent the Start Lab button from working as intended. If you experience an issue starting the lab:

Add the lab domain name to your pop-up or script blocker’s allow list or turn it off.
Refresh the page and try again.
Task 1: Investigate the customer’s needs
In previous courses, you covered the purpose of IP subnetting and the use of Classless Inter-Domain Routing (CIDR) notations. As you go through this lab, think about which CIDR notation the customer should use for the VPC and subnet.

Before you start, quickly go over what a VPC is:

A VPC is like a data center but in the cloud. It is logically isolated from other virtual networks, and you can use a VPC to spin up and launch your AWS resources within minutes.
Resources within a VPC communicate with each other through private IP addresses. An instance needs a public IP address for it to communicate outside the VPC. The VPC needs networking resources, such as an internet gateway and a route table, for the instance to reach the internet.
A CIDR block is a range of private IP addresses that is used within the VPC (for example, the /16 number that you see next to an IP address).
A subnet is a range of IP addresses within your VPC.
To determine the CIDR range, you can use the following third-party calculator
To determine the recommended range of private IP addresses that you can use, you can refer to the following guide
For task 1, you will investigate the customer’s needs and build a VPC environment based on the customer’s requirements. You then build a short and simple walkthrough for the customer to follow.

In the scenario, Paulo, who is the customer requesting assistance, has switched to using AWS and would like assistance in launching his first VPC. He has some networking knowledge but is new to AWS. You know that he needs around 15,000 IP addresses in the private range within his VPC, and he would like a public subnet. He would like to allocate at least 50 IP addresses in the public subnet.

For the customer, you will build one VPC and a guide about how to launch one.

Once you are in the AWS console, type and search for 

VPC
 in the search bar at the top. Select VPC from the list.

Tip: Alternatively, You can also find VPC under Services - Networking & Content Delivery in the top left corner

The search bar can be used to find the Amazon VPC service. Once you find the service, select it.

Figure: AWS Management Console search bar.

You are now in the Amazon VPC dashboard. You use the Amazon Virtual Private Cloud (Amazon VPC) service to build your VPC.

Choose Create VPC and configure the following options:

Resources to create: Choose VPC and more.

Name tag auto-generation: Enter 

First
.

IPv4 CIDR: Enter 

192.168.0.0/18
.

Use the following IP address calculator

IPv6 CIDR block: Choose No IPv6 CIDR block.

Tenancy: Choose Default.

Number of Availability Zones (AZs): 1

Number of public subnets: 1

Number of private subnets: 0

Expand Customize subnets CIDR blocks

Public subnet CIDR block in region: 

192.168.1.0/26
VPC endpoints: Choose None

Choose Create VPC.

On the next screen, Success message is displayed with VPC details.

Choose View VPC.

First-vpc details are displayed as per configuration.

Question: Which VPC configurations do you think have been used in previous labs?

If you thought they have been using VPCs with one subnet, that is correct. Depending on the needs of the customer, they might be using multiple public only or public and private subnets. It depends on what they need to accomplish. For this task, Brock wants to use a VPC with a Single Public Subnet according to his diagram.

Question: Why do you think there are private and public subnets?

Public subnets are for instances that can be accessed by the internet and that access the internet with a public IP and internet gateway. Private subnets keep instances private and cannot be addressed by the internet. For instances within a private subnet to connect to the internet, they will need something called a network address translation (NAT) gateway, which a later section covers in more detail.

Question: Why do you think private IP addresses are used within the VPC?

Private IP addresses are not reachable over or from the internet. This keeps your resources and its communication between your resources private within the VPC.

Task 2: Send the response to the customer (group activity)
In groups of two, submit your findings.

Person 1 acts as Brock the customer, and person 2 acts as the cloud support engineer. Person 2 walks through how they would build the VPC with person 1.

Note This task should take 30 minutes. If a group activity is not possible, have one student walk through their findings with the class.

End lab
Follow these steps to close the console and end your lab.

Return to the AWS Management Console.

At the upper-right corner of the page, choose AWSLabsUser, and then choose Sign out.

Choose End lab and then confirm that you want to end your lab.

RECAP
In this lab, you have investigated the customer’s environment and analyzed the customer’s request to build a successful walkthrough of their environment. Through this experience, you learned how to launch a VPC, which CIDR block and range to give the customer, and how to show the customer to build a VPC.

Additional resources
What is Amazon VPC?
IP Addressing in your VPC
RFC 1918
VPC CIDR
Subnet calculator
For more information about AWS Training and Certification, see https://aws.amazon.com/training/.

Your feedback is welcome and appreciated. If you would like to share any suggestions or corrections, please provide the details in our AWS Training and Certification Contact Form.

© 2022 Amazon Web Services, Inc. and its affiliates. All rights reserved. This work may not be reproduced or redistributed, in whole or in part, without prior written permission from Amazon Web Services, Inc. Commercial copying, lending, or selling is prohibited.

https://awsrestart.labs.awsevents.com/lab/arn%3Aaws%3Alearningcontent%3Aus-east-1%3A470679935125%3Ablueprintversion%2FCUR-TF-100-RSNETK-3%2F263-lab-NF-create-subnets-vpc%3A3.0.0-270aa82e/en-US