### Pause a running container (no real time uase case for this though)
### Alpine image documentation : https://hub.docker.com/_/alpine

```
# Let us first pull the image
docker pull alpine

# Check if the image has been downloaded & also check its 'tag'
docker image ls

# Spin up a new container in interactive, tty and detached (daemon) mode
docker run -itd alpine /bin/sh

# List running containers - Check all attributes - name, cmd, image, status, creation timestamp & name
docker ps

# Container can be paused using pause command
docker pause <container-id> or <container-name>

```
