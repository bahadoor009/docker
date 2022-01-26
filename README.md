# Docker

- What is Docker?
- Containerization vs virtualization
- Advantages of Containerization
- Understanding Docker Terminologies
- Listing out important commands in Docker
- Run command options in Docker
- Downloading the image and creating container
- Stopping the container and removing the container
- Understanding detached mode and interactive mode
- Using environment variable
- Creating multi-container architecture using --link
- Implementing LAMP Architecture using Docker
- Creating CI-CD Environment using Docker
- Creating testing environment using Docker
- Installing Docker compose
- Examples of docker-compose file
- Understanding Docker volume
- Types of docker volume
- Creating customized docker images
- Understanding Keywords of Docker file
- Working with Docker file
- Version controlling on Docker file
- Cache Busting
- Working with Registry
- Understanding the default process of the container
- Changing the default process of the container
- Container Orchestration
- Docker swarm

# What is Docker?
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

# Containerization vs virtualization
Virtualization -- Fixed hardware allocation.<br>
Containerization - No Fixed Hardware<br>
Process isolation ( Dependency on os is removed )<br>

# Advantages of Containerization
In comparison to the traditional virtualization functionalities of hypervisors, Docker containers eliminate the need for a separate guest operating system for every new virtual machine. Docker implements a high-level API to provide lightweight containers that run processes in isolation. A Docker container enables rapid deployment with minimum run-time requirements. It also ensures better management and simplified portability. This helps developers and operations team in rapid deployment of an application.

# Understanding Docker Terminologies
We should be comformatable with four terms:<br>

1) Docker Images:<br>
Combinations of binaries/libraries which are necessary for one software application.<br>
3) Docker Containers:<br>
When image is installed and in comes into running condition, it is called container.<br>
5) Docker Host:<br>
Machine on which docker is installed, is called as Docker host.<br>
7) Docker Client:<br>
Terminal used to run docker run commands ( Git bash )<br>

On linux machine, git bash will work like docker client.

# Listing out important commands in Docker

Docker Commands<br>
Working on Images :<br>
1) To download a docker image<br> 
   docker pull <image_name> 

2) To see the list of docker images<br> 
  docker image ls<br> 
  (or)<br> 
  docker images<br> 

3) To delete a docker image from docker host<br> 
  docker rmi <image_name/image_id><br> 

4) To upload a docker image into docker hub<br> 
   docker push <image_name><br> 

5) To tag an image<br> 
docker tag <image_name> ipaddress_of_local_registry:5000/image_name<br> 

6) To build an image from a customised container<br> 
  docker commit container_name/container_id>  <new_image_name><br> 

7) To create an image from docker file<br> 
   docker build -t  <new_image_name><br> 

8) To search for a docker image<br> 
   docker search <image_name><br> 

9)  To delete all images that are not attached to containers<br> 
   docker system prune -a<br> 

# Working on containers


10) To see the list of all running continers<br> 
   docker  container  ls<br> 

11) To see the list of running and stopped containers<br> 
    docker ps -a<br> 

12) To start a container<br> 
    docker start container_name/container_id<br> 

13) To stop a running container<br> 
    docker stop  container_name/container_id<br> 

14) To restart a running container<br> 
   docker restart container_name/container_id<br> 
         To restart after 10 seconds<br> 
   docker restart  -t  10  container_name/container_id<br> 

15) To delete a stopped container<br> 
    docker  rm  container_name/container_id<br>

16) To delete a running container<br> 
    docker  rm  -f  container_name/container id<br> 

17) To stop all running containers<br> 
    docker stop $(docker ps -aq)<br> 

18) To restart all containers<br> 
    docker restart $(docker ps -aq)<br> 

19) To remove all stopped containers<br> 
    docker rm $(docker ps -aq)<br> 

20) To remove all contianers(running and stopped)<br> 
    docker rm -f  $(docker ps -aq)<br> 

21) To see the logs generated by a container<br> 
   docker logs container_name/container_id<br> 

22) To see the ports used by a container<br> 
   docker port container_name/container_id<br> 

23) To get detailed info about a container<br> 
   docker inspect container_name/container_id<br> 

24) To go into the shell of a running contianer which is moved into background<br> 
   docker attach container_name/container id<br> 

25) To execute anycommand in a container<br> 
   docker exec -it container_name/container_id command<br>
   Eg: To launch the bash shell in a contianer<br> 
   docker exec -it container_name/container_id    bash<br> 

26) To create a container from a docker image  ( imp )<br>
     docker run image_name<br>   


# Run command options in Docker

-it 	for opening an interactive terminal in a container<br> 

--name 	Used for giving a name to a container<br> 

-d 	Used for running the container in detached mode as a background process<br> 

-e 	Used for passing environment varaibles to the container<br> 

-p 	Used for port mapping between port of container with the dockerhost port.<br>

 -P 	Used for automatic port mapping ie, it will map the internal port of the container<br> 
                with some port on host machine.<br> 
               This host port will be some number greater than 30000<br> 

-v 	Used for attaching a volume to the container<br> 

--volume-from 	 Used for sharing volume between containers<br> 

--network 	Used to run the contianer on a specific network<br> 

--link 		Used for linking the container for creating a multi container architecture<br> 

--memory  	Used to specify the maximum amount of ram that the container can use<br> 

# Downloading the image and creating container:

To download tomcat image<br>
docker pull tomee<br>

To check downloaded images<br>
docker images<br>		

To create a container from an image<br>
docker run --name mytomcat  -p   7070:8080   tomee<br>
Note: If two containers are running at same port, inorder to avoid conflict while accessing the application we use "Port mapping". 


# Stopping the container and removing the container
To stop the container we use the command<br>
docker stop container_name<br>

To remove the container<br>
docker rm -f container_name

# Understanding detached mode and interactive mode
To create ubuntu container<br>
docker run --name myubuntu  -it ubuntu<br>

Observation:  -it stands for interavtive mode. You have automatically entered into ubuntu bash<br>

Scenario 1:<br>
Start tomcat as a container and name it as "webserver". Perform port mapping and run this container in detached mode<br>

docker run --name  webserver  -p 7070:8080  -d tomee<br>

To access homepage of the tomcat container<br>
Launch any browser:<br>
public_ip_of_dockerhost:7070<br>

----------------------------------------------------------
Scenario 2:<br>
Start jenkins as a container in detached mode , name is as "devserver", perform port mapping<br>

docker run -d  --name  devserver  -p 9090:8080 jenkins<br>

To access home page of jenkins ( In browser)<br>
public_ip_of_dockerhost:9090<br>

----------------------------------------------------------

Scenario 3:<br>
Start nginx as a container and name as "appserver", run this in detached mode ,   perform automatic port mapping<br> 

Generally we pull the image and run the image<br>

Instead of pulling, i directly used this command<br>  

docker run --name  appserver  -P  -d  nginx<br> 
( if image is not available, it perform pull operation automatically )<br>
( Capital P  , will perform automatic port mapping )<br>

-----------------------------------------------------------------------------
To start mysql  as container, open interactive terminal in it, create a sample table.<br>

docker run  --name  mydb  -d  -e MYSQL_ROOT_PASSWORD=sunil  mysql:5<br>
To check<br>
docker container ls<br>

I want to open bash terminal of  mysql<br>
docker  exec   -it  mydb  bash<br>

To connect to mysql database<br>
mysql  -u  root  -p<br> 

# Multi container architecture using docker
This can be done in  2  ways<br>
1) --link<br>
2) docker-compose<br>

EXample 1: Start two busybox containers and create link between them<br>

Create 1st busy box container<br>
docker run --name c10 -it   busybox<br>
How to come out of the container without exit<br>
( ctrl + p  + q)<br>

Create 2nd busy box container  and establish link to c1 container<br>
docker run --name  c20 --link c10:c10-alias  -it  busybox   ( c10-alias  is  alias name)<br>

How to check  link is established for not?<br>
ping c10<br>

Ctrl +c  ( to come out from ping )<br>
(ctrl + p  + q)<br>

Example 2: Creating development environment using docker<br>
------------------------------------------------------------<br>
Start mysql as container and link it with wordpress container.<br>

Developer should be able to create wordpress website<br>


1) To start mysql as container<br>
docker run --name mydb  -d  -e  MYSQL_ROOT_PASSWORD=sunil  mysql:5<br>

( if container is already in use , remove it using docker rm -f  mydb)<br>

Check whether the container is running or not.<br>
docker container ls<br>

2) To start wordpress container<br>
docker run  --name mysite  -d  -p 5050:80 --link mydb:mysql  wordpress<br>

Check wordpress installed or not.<br>
Open browser<br> 
public_ip:5050<br>
18.138.58.3:5050<br>

# Create LAMP  Architecture using docker

L -- linux<br>
A -- apache tomcat<br>
M -- mysql<br>
P --  php<br>
(Linux os we already have)<br>
1) To start mysql as container<br>
docker run --name mydb  -d  -e  MYSQL_ROOT_PASSWORD=sunil  mysql:5<br>


2) To start tomcat as container<br>
docker run  --name  apache  -d  -p 6060:8080  --link mydb:mysql  tomcat<br>


To see the list of containers<br>
docker container ls<br>

To check if tomcat is linked with mysql<br>
docker inspect apache      ( apache is the name of the container)<br>


3) To start php as container<br>
docker  run --name php  -d --link apache:tomcat  --link mydb:mysql    php<br>


# Create CI-CD environment, where jenkins container is linked with two tomcat containers.<br>

Lets delete all the container<br>
docker rm  -f  $(docker ps -aq)<br>

To start jenkins as a container<br>
docker run  --name  devserver  -d -p 7070:8080 jenkins/jenkins<br>

To check jenkins is running or not?<br>
Open browser<br>
public_ip:7070<br>

We need two tomcat containers  ( qa server and prod server)<br>
docker run --name  qaserver  -d  -p 8080:8080 --link devserver:jenkins tomee<br>

To check the tomcat   use public_ip but port number will be 8080<br>
docker run --name  prodserver  -d  -p 9090:8080 --link devserver:jenkins tomcat<br>


# Creating testing environment using docker:<br>

Create selenium hub container, and link it with two node containers. One node with firefox installed, another node with chrome installed. Tester should be able to run selenuim automation programs for testing the application on multiple browsers.<br>

Search for selenium:<br>
We have a image -  selenium/hub<br>

To start selenium/hub as container<br>
docker run --name  hub  -d -p 4444:4444   selenium/hub<br>


In hub.docker.com<br>
we also have-  selenium/node-chrome-debug    ( It is ubuntu container with chrome)<br>

To start it as a container and link to hub ( previous container)<br>
docker run --name chrome  -d -p 5901:5900  --link hub:selenium   selenium/node-chrome-debug<br>

In hub.docker.com<br>
we also have-  selenium/node-firefox-debug<br>

To start it as a container and link to hub ( It is ubuntu container with firefox)<br>
docker run --name firefox  -d -p 5902:5900  --link hub:selenium   selenium/node-firefox-debug<br>

To see the list of container<br>
docker container ls<br>

Note: firefox and chrome containers are GUI containers.<br>
To see the GUI interface to chrome / firefox container<br>

Download and install vnc viewer<br>
In VNC viewer search bar<br>
public_ip_dockerhost:5901<br>

Password - secret<br>

------------------------------------------------------------------------------------


All the commands we learnt till date are adhoc commands.<br>

In the previous usecase we have installed two containers ( chrome and firefox)<br>
Lets say you need 80 containers?<br>
Do we need to run 80 commands?<br>
 
Instead of 80 commands, we can use docker compose<br>


# Docker compose

This is a feature of docker using which we can create multicontainer architecture using yaml files. This yaml file contains information about the  containers that we want to launch and how they have to be linked with each other.Yaml is a file format. It is not a scripting language.
Yaml will store the data in key value pairs<br>
Lefthand side - Key<br>
Righthand side - Value<br>
Yaml file is space indented.<br>

Sample Yaml file<br>
-------------------------<br>

bahadoorsoft:<br>
 trainers:<br>
  bahadoor: Devops<br>
  daya: Python<br>
 Coordinators:<br>
  sai: Devops<br>
  bahadoor: AWS<br>
...<br>


bahadoorsoft -- root  element<br>

To validate the abvove Yaml file<br>
Open  http://www.yamllint.com/<br>
Paste the above code  -- Go button<br>

------------------------------------------------------------------------------------------------------<br>

# Installing Docker compose

1) Open https://docs.docker.com/compose/install/<br>
2) Go to linux section<br>
Copy and pase the below two commands<br>

sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose<br>
sudo chmod +x /usr/local/bin/docker-compose<br>
	
How to check docker compose is installed or not?<br>

docker-compose  --version<br>









