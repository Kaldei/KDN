---
title: Docker CLI
summary: A note about the Docker CLI.
description: A note about the Docker CLI.
tags:
  - docker
---

# Administration

---

### Context


 > 
 > **<font color=red>docker context ls</font>**</br>
 > Show created contexts (list of Docker sockets).
 > 
 > **<font color=red>docker context use</font> myRemoteContext**</br>
 > Switch to a Docker context.

 > 
 > **<font color=red>docker context create</font> myRemoteContext <font color=red>--docker "host=</font>ssh://my.remote.docker.ip<font color=red>"</font>**</br>
 > Create a remote context (connect via ssh to execute Docker commands).

---

### Monitoring


 > 
 > **<font color=red>docker ps</font>**</br>
 > Show running containers.
 > 
 > **<font color=red>docker ps -a</font>**</br>
 > Show all containers.
 > 
 > **<font color=red>docker stats</font>**</br>
 > Stats about running containers.

 > 
 > **<font color=red>docker volume ls</font>**</br>
 > Show volumes.

# Images

---

### Basis


 > 
 > **<font color=red>docker images</font>**</br>
 > Show images locally available.

 > 
 > **<font color=red>docker pull</font> registryImage**</br>
 > Pull image from an image registry.
 > 
 > **<font color=red>docker pull</font> registryImage<font color=red>:</font>imageTag**</br>
 > Pull specific tag of an image an image registry.

 > 
 > **<font color=red>docker rmi </font>myImage**</br>
 > Remove the local image.

---

### Layers


 > 
 > **<font color=red>docker image history</font> myImage**</br>
 > Show image layers.
 > 
 > **<font color=red>docker image history</font> myImage <font color=red>--no-trunc --format json | tac | jq -r '.CreatedBy'</font>**</br>
 > Show image layers commands.

---

### Create


 > 
 > **<font color=red>docker build </font> path/to/Dockerfile <font color=red>-t</font> myUser<font color=red>/</font>myImageName<font color=red>:</font>myVersion**</br>
 > Create an image from a Dockerfile.

 > 
 > **<font color=red>docker diff</font> myContainer**</br>
 > Show differences between an image and a container created from this image.
 > 
 > **<font color=red>docker commit</font> myContainer myNewImage**</br>
 > Save the current state of a container into a new image.

 > 
 > **<font color=red>docker save</font> myImage <font color=red>\></font> /path/myImage.tar**</br>
 > Export an image (archive).
 > 
 > **<font color=red>docker load -i</font> /path/myImage.tar**</br>
 > Import an image (form archive).

# Containers

---

### Create


 > 
 > **<font color=red>docker create</font> myImage**</br>
 > Create a new container.
 > 
 > **<font color=red>docker run</font> myImage myCommand**</br>
 > Run a command in new container.

---

### Manage


 > 
 > **<font color=red>docker rename</font> myContainer myContainerNewName**</br>
 > Rename container.

 > 
 > **<font color=red>docker start</font> myContainer**</br>
 > Start the container.
 > 
 > **<font color=red>docker pause</font> myContainer**</br>
 > Pause the container.
 > 
 > **<font color=red>docker stop</font> myContainer**</br>
 > Stop the container.

 > 
 > **<font color=red>docker rm</font> myContainer**</br>
 > Remove the container.

---

### Interact


 > 
 > **<font color=red>docker exec</font> myCommand myContainer**</br>
 > Run the command in a running container.
 > 
 > **<font color=red>docker exec -it /bin/bash</font> myContainer**</br>
 > Run Bash in interactive mode in a running container.

 > 
 > **<font color=red>docker cp</font> myFile.txt myContainer<font color=red>:</font>/path/to/destination**</br>
 > Copy a file from host to the container.
 > 
 > **<font color=red>docker cp</font> myContainer<font color=red>:</font>/path/to/source myFile.txt**</br>
 > Copy a file form the container to the host.

---

### Flags


 > 
 > **<font color=red>--name</font> myContainer**</br>
 > Give a name to the container.

 > 
 > **<font color=red>-d</font>**</br>
 > Detached Mode (run in background).
 > 
 > **<font color=red>-it</font>**</br>
 > Keep stdin open (to use it like a shell).
 > 
 > **<font color=red>--rm</font>**</br>
 > Remove the container when it is stopped.

 > 
 > **<font color=red>-p</font> 1212<font color=red>:</font>1212**</br>
 > Map ports (host:container).
 > 
 > **<font color=red>-v</font> /myHostFolder<font color=red>:</font>/myContainerFolder**</br>
 > Map a folder between the host and the container.

 > 
 > **<font color=red>--read-only</font>**</br>
 > Makes the container's root file system read-only.
 > 
 > **<font color=red>--security-opt=no-new-privileges</font>**</br>
 > Prevents processes inside the container from gaining new privileges during execution (security measure against privilege escalation).

 > 
 > **<font color=red>--cap-drop=ALL</font>**</br>
 > Start the container without capabilities.
 > 
 > **<font color=red>--cap-add=SYS_NICE</font>**</br>
 > Capability for scheduling (required for GPU scheduling?).

 > 
 > **<font color=red>--cpus=</font>2**</br>
 > Set CPU limit.
 > 
 > **<font color=red>--gpu</font> all**</br>
 > Set GPU limits (syntax allows for more detailed control than CPU).
 > 
 > **<font color=red>--memory=</font>4g**</br>
 > Set RAM limit.
 > 
 > **<font color=red>--memory-swap=</font>4g**</br>
 > Set Swap limit.

# Tips

---

### Access Container File System


 > 
 > **CONTAINER_PID=$(<font color=red>docker inspect -f '{{.State.Pid}}'</font> myContainer)**</br>
 > Get container's PID.
 > 
 > **<font color=red>nsenter --target</font> $CONTAINER_PID <font color=red>--mount ls</font> /**</br>
 > Run ls in the container's file system.
