### Run alpine based container
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

# Attach to your alpine container, using either its unique container ID or its name
docker attach <container-id> or <container-name>

# To detach from within the container, type in the following keys, in quick succession
CTRL P CTRL Q

# Stop a container
docker stop <container-id> or <container-name>

```
