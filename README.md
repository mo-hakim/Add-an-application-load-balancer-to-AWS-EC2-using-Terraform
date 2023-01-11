<h1>Add an application load balancer to AWS EC2 using Terraform</h1>


<h2>Description</h2>
A highly available application has higher chances of attracting customers because they are assured of consistency in service. Load balancing is a cost-effective way to increase an application’s availability. In this note, I describe the steps to add an application load balancer to three EC2 instances hosted in three different availability zones in a region using Terraform.
<br />


<h2>Environments Used </h2>

- <b>AWS EC2</b>
- <b>Load balancer</b>
- <b>Terraform</b> 

<h2>Walk-through:</h2>

<p align="center">
Step 1: Create a target group: <br/>
<img src="https://i.imgur.com/zbZFB61.png" height="80%" width="80%" alt="Disk Sanitization Steps"/> <br/>
Per AWS-Docs, a target group is used to route requests to one or more registered targets. I specified the port and protocol that this target group was listening to. <br />
<br />
<br />
Step 2: Attach the target group to the AWS instances <br/>
<img src="https://i.imgur.com/sTtnvMp.png" height="70%" width="70%" alt="Disk Sanitization Steps"/> <br/r>
In this step, I attached the aws_lb_target_group to the three EC2 instances and specified the port number on which traffic would be routed.
<br />
Since this was a proof of concept and since I did not require HTTPS traffic, I did not bother to create more than what was necessary. 
<br />
<br />
Step 3: Create the load balancer <br/>
Then I created the load balancer and attached a security group and a set of subnets.<br/>
<img src="https://i.imgur.com/lVkachw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Step 4: Create a listener <br/>
Finally, I attached the load balancer to the target group. Per AWS-Docs, a listener is a process that checks for connection requests, using the protocol and port that you configure. The rules that you define for a listener determine how the load balancer routes requests to its registered targets. <br/>
<img src="https://i.imgur.com/kx1zrzJ.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
With all the above code, I ran the usual Terraform commands of terraform apply (after initializing the repository). And after Terraform provisioned the resources, I received the message below. That is due to the specification in the output block (in the output.tf file):  <br/>
<img src="https://i.imgur.com/M2e2AWw.png" height="60%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />
This is the load balancer DNS name. I typed that on my web browser, and the request was randomly routed to one of the EC2 instances’ index.html page. The request was routed to a different EC2 instance with each web browser refresh. And that is how an application load balancer works <br/>
<br />
<br />
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
