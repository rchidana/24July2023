### Docker Exercises


Check if Docker service is running on Ubuntu Linux <br>

```
sudo systemctl status docker
```

Start Docker service in case its down<br>

```
sudo systemctl start docker
```

Check Docker version<br>

```
docker version
```

Getting Help on any docker command<br>

```
docker help
docker <command> --help
```


Spin up a new container and run 'hello-world' image in it<br>

```
docker run hello-world
```

Spin up a new container, run alpine image in an Interactive & TTY mode and run in daemon (background mode)<br>

```
docker run -itd alpine /bin/sh
```

Spin up a container with a specific name - 'my-container' and run with alpine in it<br>

```
docker run -itd --name my-container alpine /bin/sh
```

Check on all "RUNNING" container(s) <br>

```
docker ps
```

Check the status of all (RUNNING, EXITED, CRASHED etc) containers <br>

```
docker ps -a
```

Stop a "RUNNING" container <br>

```
docker stop <container-id>
```

Pause a "RUNNING" container <br>

```
docker pause <container-id>
```

Un-Pause a "RUNNING" container <br>

```
docker unpause <container-id>
```

Start a "STOPPED" or "EXITED" container <br>

```
docker start <container-id>
```

Attach to a running container (assumption : the container is started in Interactive & tty mode and has a linux shell to interact <br>

```
docker attach <container-id>

```

Fire a command against a running container <br>

```
docker exec -it <container-id> <command>
```

Check container Logs <br>
```
docker logs <container-id>
```

Run an Alpine container so that it prints time stamp every 5 secs and then check its log <br>

```
docker run -itd alpine /bin/sh -c "while true;do date;sleep 5;done"
docker ps
docker logs <container-id>
```

Inspect any Docker element to get all kinds of Useful information <br>

```
docker inspect <container-id>
docker inspect <volume-name>
docker inspect <image-name>:<tag>
```

Docker images can be saved in 'tar' format so that it can be shared without having a need for Docker Registry <br>
The following command will save alpine:latest image in a tar file (alpine.tar) <br>

```
docker save alpine:latest --output alpine.tar
```

docker load command can be used to import the image from the tar file <br>

```
docker load -i <tar-file>
docker load -i alpine.tar
```

Building image from the default Dockerfile <br>

```
docker build . -t <your-image-name>:<tag>
```

To build image from any file (not the default Dockerfile) <br>

```
docker build . -f <name-of-Docker-file> -t <your-image-name>:<tag>
```

To create an image from a container <br>
```
docker container commit <container-name> <your-image-name>:<tag>
```

To login to DockerHub <br>
```
docker login
# Provide your DockerHub credentials
```

To push an image to Dockerhub <br>
```
docker push <your-docker-id>/<image>:<tag>
```

Images can be re-named using 'tag' command <br>

```
docker tag <image>:<tag> <new-image-name>:<new-tag>
docker tag my-alp:latest anandr72/my-alp:latest
```

Create volume <br>

```
docker volume create <volume-name>
docker inspect <volume-name>
```

Spin up a container by linking a volume <br>

```
docker run -itd --name <container-name> -v <volume-name>:/<path-inside-container> <image>:<tag> <command> <args>

```

Bind Mount an existing folder inside a container <br>
```
docker run -itd --name <container-name> -v </path/to/folder>:/<path-inside-container> <image>:<tag> <command> <args>
```

Mount volumes from named containers using --volumes-from <br>

```
docker run -itd --name <container-name> --volumes-from <other-container-which-has-volumes> <image>:<tag> <command> <args>
```

Exposing or Publishing Container Ports <br>
```
docker run -d -p <host-port>:<container-port> <image>:<tag>

# Eg : To run nginx on host machine port 8080
docker run -d -p 8080:80 nginx
```

Deleting Docker Elements <br>

```
docker rm <container-id>
docker rmi <image-name>
docker volume rm <volume-name>
```

Get Docker events for a specific time frame <br>
```
docker events --since '2022-12-01'
# various filters can be added
docker events --filter 'event=stop'
docker events --filter 'image=alpine'
docker events --filter 'type=volume'
```

Top command can get your required statistics of any container <br>

```
docker top <container>
```

Stats command can be used to obtain live resource usage statistics for any container <br>
```
docker stats

# For only few containers
docker stats <container-1> <container-2>
# Various filters can be applied to get specific stats - .CPUPerc, .MemUsage, .MemPerc, .NetIO, .BlockIO
docker stats --format "{{.Container}}: {{.CPUPerc}}"
```
