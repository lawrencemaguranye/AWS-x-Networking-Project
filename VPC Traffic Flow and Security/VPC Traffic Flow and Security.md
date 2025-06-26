# VPC Traffic Flow and Security

**Author**: Lawrence T. Maguranye  
**Platform**: AWS Cloud

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC lets you create a private network within AWS where you control IP addresses, subnets, routing, and security. It’s useful for securely hosting resources like EC2 instances and databases, with full control over traffic flow and access.

---

### How I used Amazon VPC in this project

I used Amazon VPC to set up a secure network with a public subnet, routing, and access controls—perfect for organizing my project into isolated, manageable layers.

---

### One thing I didn't expect in this project was...

One thing I didn't expect in this project was how easily a small routing misconfiguration could block access between tiers—it was a great reminder that in cloud networking, even tiny details matter.

---

### This project took me...

It took me about 2 hours to complete this task.

---

## Route Tables

A route table is a set of rules, called routes, used to determine where network traffic is directed. They are associated with subnets in a VPC and play a key role in controlling the flow of traffic within your cloud network and between the internet.

> **Why are route tables needed to make a subnet public?**  
A subnet becomes public in AWS only when its route table contains a route to the Internet Gateway (IGW). Without this route, resources in the subnet cannot communicate with the internet.

![My Route 2](https://github.com/lawrencemaguranye/AWS-x-Networking-Project/blob/main/images/Route%202.png)

## Route Destination and Target

Routes are defined by their **destination** and **target**, which means:

- **Destination**: Specifies the range of IP addresses the traffic is intended for.
- **Target**: The gateway through which that traffic should be directed to reach its destination.

> **Example**:  
The route in my route table that directed internet-bound traffic to my internet gateway had a:
- **Destination**: `0.0.0.0/0`  
- **Target**: `igw-03683c3e06b5f92a3`

![My Route 2](https://github.com/lawrencemaguranye/AWS-x-Networking-Project/blob/main/images/Route%202.png)

## Security Groups

Security groups are virtual firewalls in AWS that control inbound and outbound traffic for resources like EC2 instances. They act as gatekeepers, allowing or denying traffic based on rules you define.

![My Security Group Diagram](https://github.com/lawrencemaguranye/AWS-x-Networking-Project/blob/main/images/Security%20Group.png)


### Inbound vs Outbound Rules

- **Inbound Rules**: Access control settings that define which incoming traffic is allowed to reach an AWS resource (e.g., EC2 instance).
  - Example: I configured an inbound rule that allows all inbound HTTP traffic.

- **Outbound Rules**: Control which types of traffic your AWS instance is allowed to send out to the internet or other destinations.
  - Default: All outbound traffic is allowed.

---

## Network ACLs (Access Control Lists)

Network ACLs are **stateless**, subnet-level firewalls in AWS that control **inbound and outbound traffic** in and out of your Virtual Private Cloud (VPC). Network ACLs evaluate every request independently—both coming in and going out.

---

### Security Groups vs. Network ACLs

| Feature            | Security Groups | Network ACLs      |
|--------------------|------------------|--------------------|
| Stateful/Stateless | Stateful         | Stateless          |
| Level              | Instance-level   | Subnet-level       |

---

### Default vs Custom Network ACLs

- **Default Network ACL**:
  - Inbound and outbound rules allow **all traffic**.
  - Allows every protocol, every port range, and all IP addresses (IPv4: `0.0.0.0/0`, IPv6: `::/0`).

- **Custom Network ACL**:
  - All traffic is **denied by default**.
  - Requires specific **allow rules** to permit data flow for defined ports, protocols, and IP addresses.

![My Route 2](images/Network ACL.png)

---
