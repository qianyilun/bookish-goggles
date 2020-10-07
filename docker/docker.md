This is the note of a docker lecture, Docker Tutorial for Beginners - A Full DevOps Course on How to Run Applications in Containers, on YouTube. The video link is [here](https://www.youtube.com/watch?v=fqMOX6JJhGo). 

# Docker Basic Commands
In this lecture, we leared how to show all containers, show images, run a container, stop a container, and delete container. 

# Run - PORT mapping

## Run container and access web
``` shell
$ docker run kodekloud/webapp

# output
# * Running on htpp://0.0.0.0:5000/
```

So, how a user can access the web? 

Assume we are using Mac and a Ubuntu is running inside a VritualBox. The docker is running on Ubuntu. 

There are two ways. 
1. Access from inside of the docker host:
	
	Use the IP of the docker container. Every docker container gets an IP assigned by default. In this case, it is `172.17.0.2`. But remember, this is the internal IP and it is only accessible within the docker host. For example, if I run this instance on Ubuntu, I only can access the web by going to `http://172.17.0.2:5000` inside Ubuntu. Considered this is an internal IP, any users out side the docker host (my Mac cannot access it) using this IP. So we need #2. 
		
	- How to get the ip of the docker container?
	- Answer: https://stackoverflow.com/questions/17157721/how-to-get-a-docker-containers-ip-address-from-the-host
		
		```shell
		$ docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_name_or_id>
		```
	- WHat is the docker host? 

2. Access from outside of the docker host (i.e. from my Mac)

	We could use the IP of the docker host (i.e. Ubuntu). For example, `172.16.190.131` is the IP address of Ubuntu. We also need to assign a free port to the host, e.g. `80`, so that user can access the web app outside Ubuntu. We can achieve this using `-p` parameter and running the following mapping port command.

	``` shell
	$ docker run -p 80:5000 kodekloud/webapp
	```

	In this case, we can access `http://172.16.190.131:80` from my Mac browser. This command means forward all traffic to port 5000, the docker container. 

	In this way, you can also run multiple instances and map then to different ports. 

	``` shell
	# Run multiple instances
	$ docker run -p 80:5000 kodekloud/webapp
	$ docker run -p 8000:5000 kodekloud/webapp
	$ docker run -p 8001:5000 kodekloud/webapp
	```

	Or you can run different applications.

	``` shell
	$ docker run -p 80:5000 kodekloud/webapp
	$ docker run -p 8000:5000 kodekloud/webapp
	$ docker run -p 8001:5000 kodekloud/webapp
	# and ...
	$ docker run -p 3306:3306 mysql
	$ docker run -p 8306:3306 mysql
	```

## Run - VOLUME mapping
How data is persisted in a docker container.

Suppose you created a mySQL container and you would like to backup your data inside this container before delete this container. You can run the mySQL container by mapping data outside the container to the container by running the following command.

``` shell
$ docker run -v /opt/datadir:/var/lib/mysql mysql
```

`/opt/datadir` is the directory of the host and `/var/lib/mysql` is the directory inside the docker container. This command means when the container runs, it will implicitly mount the external directory to a folder side the docker container. All your data will be stored outside the container and the data will not be deleted even you remove the container. 

## Inspect container
`docker ps` command is enough to see basic details about containers. But if you would like to see more details, you can use `inspect` command. 

```shell
$ docker inspect <container_name_or_id>
```

It will return all container details in a JSON format. 

## Container logs
How to see logs of a container that runs in the background.

For example, I used `-d` parameter while running the container. It means the container is now in the detach mode and will run in the background. 

``` shell
$ docker logs <container_name_or_id> 
```

# Environment Variables
## Run containers with enviroment variables
Suppose we have an application that consumes a enviornment variable `APP_COLOR`. Use the following command with parameter `-e` to pass in the enviroment variable.

```shell
$ docker run -e APP_COLOR=blue <container_name_or_id>
```

## How to check the enviroment in a container that is running
Use `inspect` to see the details.

```shell
$ docker inspect <container_name_or_id>
```

You should find the value of `Env` in the returned JSON.

```json
[
	{
		"id" : "...",
		"State": "...",
		"...": "...",
		"Config": {
			"Env": [
				"APP_COLOR=blue",
				"xxx"
			],
			"...": "..."
		},
		"...": "..."
	}
]
```

## Quiz question: 
1. Run a container named blue-app using image kodekloud/simple-webapp and set the environment variable APP_COLOR to blue. Make the application available on port 38282 on the host. The application listens on port 8080.

	```shell
	$ docker run -p 38282:8080 -e APP_COLOR=blue --name blue-app kodekloud/simple-webapp
	```

2. Run a container of mysql and rename it as mysql-db. Set the root password as db_pass123.

	```shell
	$ docker run --name mysql-db -e MYSQL_ROOT_PASSWORD=db_pass123 mysql
	```

# Build container from Dockerfile
```shell
# cd to directory contains the Dockerfile
$ docker build -t <image_name_you_want> .
# this will build image with the default tag:latest
```

# Docker Networking
When you installed docker, it creates three networks automatically, `Bridge`, `none`, and `host`. 

`Bridge` is the default network a container gets attached to.  

If you would like to detach the container to other network, you can use the command like this...
```shell
$ docker run --network=none <image_name>
# Or
$ docker run --network=host <image_name> 
```

## Bridge network
A private internal network created by docker on the host. All containers attached to this network and assigned an IP address by default. Containers can access each other using its internal IP if required. By default, there is only VPC inside the bridge. But we can also create multiple VPCs inside the bridge using `network create` command. 

```shell
$ docker network create --driver bridge --subnet 182.18.0.0/16 custom-isolated-network
```

And use `docker network ls` to list all networks. But creating new subnet is not the purpose of this class. Please search mroe online if interested. 

## Host network
Attach containers into host network can allow container to be accessed from the host. But this take out the isolation between the docker host and docker container. And now you cannot run the multiple instances using the same port. 

## None network
The container is not attached to any network. It has no access to external network or any other containers. They are run in the isolated network. 

## How to find the internal IP assigned to a container
Using `inspect` and you can find it in the `NetworkSettings` section. 

```shell
$ docker inspect <container_name_or_id>
```

Output:
```json
[
	{
		"...": "...",
		"NetworkSettings": {
			"...": "...",
			"Networks": {
				"bridge": { // what network is on
					"...": "...",
					"IPAddress": "172.17.0.6", // what IP was assigned to
					"...": "..."
				}
			}
		}
	}
]
```

## Embedded DNS
Docker has embedded a DNS so that containers can access each other using container name. The internal DNS server will map container name to its IP address. 

## Quiz questions
Create a new network named wp-mysql-network using the bridge driver. Allocate subnet 182.18.0.1/24. Configure Gateway 182.18.0.1

	```shell
	$ docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 wp-mysql-network
	```