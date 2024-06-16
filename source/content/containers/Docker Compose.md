---
title: Docker Compose
summary: A tool for defining and running multi-container applications.
description: A tool for defining and running multi-container applications.
tags:
  - docker
  - container
---

# Resources

* **[https://github.com/docker/awesome-compose](https://github.com/docker/awesome-compose)**

# CLI

---

### Basis


 > 
 > **<font color=red>docker-compose up -f</font> /pathToComposeFiles**</br>
 > Create a network and run containers in it.
 > 
 > **<font color=red>docker-compose stop -f</font> /pathToComposeFiles**</br>
 > Stop containers.
 > 
 > **<font color=red>docker-compose down -f </font>/pathToComposeFiles**</br>
 > Remove network and containers.

# Compose File Examples

---

### Network


````yaml
version: "3"


services:
	myContainer1:
		image: nginx
		ports: 
			- "8081:80"
		restart: always		   # Restart at machine startup.
		
	myContainer2:
		image: nginx
		ports: 
			- "8082:80"
		restart: always		   # Restart at machine startup.
		networks:			   # Put the container in the network
			ipv4_address: 192.168.168.0.100

   
networks:
	myNetwork:
		ipam:				    # IP Address Managment
			driver: default 	# Bridge
			config:
				- subnet: “192.168.168.0.0/24”
````
