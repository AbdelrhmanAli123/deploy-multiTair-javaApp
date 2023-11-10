# deploy-multi-tair-javaApp

# Prerequisites
#
- AWS account
- JDK 11
- Maven 
- MySQL 8

# Technologies 
- Spring MVC
- Spring Security
- Spring Data JPA
- Maven
- JSP
- Tomcat
- MySQL
- Memcached
- Rabbitmq
# Project design
#  
![project1](https://github.com/AbdelrhmanAli123/deploy-three-tair-javaApp/assets/133269614/a7f813b6-9b72-423b-b41c-2f8224d92c33)

 
# Project steps
#

## Create a Security Group
- create SG for the LB
- create SG for the tomcat server
- create SG for the backend servers (mysql - memcached - rabbitmq)
- the inbound and the outpound traffic and  the open ports are attached as pictures in the repo

## Create  4 VMs
- The first for Tomcat server
- The second for MySQL server
- The third for Memcached server
- the fourth for Rabbitmq server
- use the USER DATA option to configure the servers and install the services during the boot process

## Create hosted zone using route53
- create a private hosted zone using route53 to allow the traffic between the VMs using names, not IPs
- write the name that you want instead of using the private IP, not the public IP
- test the connection by using the command ping and use any name that you wrote
- after writing the name of each server, write these names in the application.properties 

## Create Load Balancer
- first, you should create a target group
- add the Tomcat server to the target group
- allow the health check on the path /login
- create an application load balancer
- attach the TG to LB and apply SSL certificate if you have one
- if you have a domain name use the domain name to map it to the LB URL

## build the artifact 
- first clone the repo go to the src Dir
- run this command to build the artifact
```
mvn install
```
- cp the artifact to the/var/lib/tomcat7/webapps/
- restart the tomcat service

## validation 
### Try to hit the Load Balancer URL or you domain name if you have one and it's supposed to work correctly
