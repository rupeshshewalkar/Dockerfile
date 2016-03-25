##Introduction to Docker

 1)Docker is tool used to packing application with its software dependencies in virtual container
 2)Docker can run linux, windows & Mac
 3)Docker used in lot of cases like build management,configuration management,rapid deployment, Application isolation etc
 4)Docker offers you the ability to isolate your application,standardize your build & deployment process
 
##Containers Vs. Virtual Machines

Virtual Machines : 
                  1)Virtual Machine allows you to set up one operating system within another
		  2)Virtualization allows you to run two completely different OS on same hardware. 
	            Each guest OS goes through all the process of bootstrapping, loading kernel etc. 
		    You can have very tight security, for example, guest OS can't get full access to host OS or other guests and mess things up.
Containers : 
                 containers one of the function of OS is to allow sharing of global resources like network and disk to processes. 
		 What if these global resources were wrapped in namespaces so that they are visible only to those processes that runs in the same namespace? 
		 Say, you can get a chunk of disk and put that in namespace X and then processes running in namespace Y can't see or access it. 
		 Similarly, processes in namespace X can't access anything in memory that is allocated to namespace Y.
		 Of course, processes in X can't see or talk to processes in namespace Y. This provides kind of virtualization and isolation for global resources. 
		 This is how docker works: Each container runs in its own namespace but uses exactly the same kernel as all other containers. 
		 The isolation happens because kernel knows the namespace that was assigned to the process and during API calls it makes sure that process can only access resources in its own namespace.
            
Limitation 

		The limitations of containers vs VM should be obvious now: You can't run completely different OS in containers like in VMs. 
		However you can run different distros of Linux because they do share the same kernel. 
		The isolation level is not as strong as in VM. In fact, there was a way for "guest" container to take over host in early implementations. 
		Also you can see that when you load new container, the entire new copy of OS doesn't start like it does in VM. 
		All containers share same kernel. This is why containers are light weight. Also unlike VM, you don't have to pre-allocate significant chunk of memory to VM because we are not running new copy of OS. 
		This enables to run thousands of containers on one OS while sandboxing them which might not be possible to do if we were running separate copy of OS in its own VM.

##Docker Architecture

 Docker clients & daemons communicate via sockets or through a RESTful API (http in xml format)

 
##Docker Installation

 docker version
 docker images : show all available repo/images
 docker images : show all available repo/images
 docker search <<image_search>> : will search image in docker hub

##Creating Our First Image

 docker info : all information about current installation docker include images details, partation details etc
 docker pull <<image_need_install>>: used to pull image from docker hub
 docker inspect << image_name>> : will give all information container
 docker run -i -t <<image_name>> /bin/bash : interactive shell from docker container

 
##Packaging A Customized Container

 docker ps -a : process running under container
 docker commit -m=" Add a ruby json module using gem" -a=" Linux academy" <<container_id>> <<image_name>> : used to make your own image -a is author name -m is for message

 
##Running Container Commands With Docker

 docker run <<image_name>> /bin/echo 'hello from your Docker Container!''
 docker run -d ubuntu:latest /bin/bash -c "while true; do echo DockerMAN; sleep 1;done"
 docker log : display all log of specific container
 docker stop : used to stop container

## Exposing Our Container With Port Redirects

 docker run -d -p 8080:80 <<name_baseimage>>
 
##Attach to a Running Container

 docker attach << container_name OR ID>>
 docker is process oriented

## Removing Images

 docker rm << container name or ID>> : remove container
 docker rmi : used to remove images

## Directory Structure

 cat repositories-devicemapper | python -mjson.tool

## Pushing Images to Docker Hub

 docker push username/baseOSname:label : used to push image in hub

## Image Volume Management

 docker run -i -t -v /myapp container_name or ID /bin/bash

## Advanced Container Network Management

 ip link add br10 type bridge
 ip addr add 10.10.100.1/24 dev br10
 ip link set br10 up

## Interactive Shell Control

 docker exec -i -t <<container_Name>> /usr/bin/top :used to run inside process/service

## Previous Container Management

 docker rm `docker ps -a`

## Sharing Container Resources

 docker run -d -i -t -v /data --name DATA1 centos:centos6 /bin
 doker run -d -i -t --volume-from data1 --name data2 centos:centos6 /bin/bash

## Committing a Running Container (Snapshot Images)

 docker commit <<container_name>> centos6:which

## Optimizing Our Dockerfile Builds

 docker image -t : will give how container build & how much sub container used to build

## Five Useful Docker CLI Commands

 docker cp <<container_name>>:/etc/yum.conf /tmp : used to copy some file from container to base image location
 
 docker diff : used to find all changes in container
 
 docker events : used to find/monitor all events i.e(start,stop,die..etc) container
 
 docker events --since '2014-12-05' find all events happening with container since 2014-12-05
 
 docker history <<container_name>> : find out history of all running command in container
 
 docker exec : used to run any command running container

## More Useful Docker CLI Commands

 docker info : all information docker system(Kernel,Ram,Partition..etc)
 docker top <<container_ID/Name>> : top process running inside container
 docker stop : docker container stop
 docker kill : unclean way stop container
 docker [un]pause <<container_ID/name>> : used to pause/unpause container
 docker export <<container_ID/name>> > export.tar : used to export container
 docker load < export.tar : load container from export file
