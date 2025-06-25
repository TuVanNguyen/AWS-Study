# Elastic Load Balancer

### What is ELB?
service that distributes network traffic across group of servers

![Elastic Load Balancer](../imgs/ELB.png)

### Types
* Application Load Balancer: distributes HTTP/HTTPS traffic
    * operate on layer 7 (Application layer) on [OSI model](../../0.NetworkingBasics/OSI.md)
    * support advanced request routing to specific web servers based on HTTP header
* Network Load Balancer: TCP traffic, high performance
    * operates on layer 4 (Transport layer)
* Classic Load Balancer: HTTP/HTTPS, TCP, legacy
    * support layer 7 specific features e.g X-Forwarded-For headers, sticky sessions
    * support layer 4 TCP protocol
* Gateway Load Balancer: workloads for 3rd party apps 
    * e.g virtual apps purchased on AWS marketplace
    * virtual firewalls
    * Intrusion Detection Systems (IDS) or Intrusion Prevention System (IPS)

### 



