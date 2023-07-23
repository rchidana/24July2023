### Run alpine based container but let us specify a name of our choice
### Let the container print some message to stdout
### docker logs can be used to check the logs of any running container
### Alpine image documentation : https://hub.docker.com/_/alpine

```
# Let us first pull the image
docker pull alpine

# Check if the image has been downloaded & also check its 'tag'
docker image ls

# Spin up a new container by specifying a name using --name option
docker run --name sysout-ctr -itd alpine /bin/sh -c "while true; do date; sleep 5;done"

# List running containers - Check all attributes - name, cmd, image, status, creation timestamp & name
docker ps

# One can check the logs from the container using docker logs
docker logs sysout-ctr

# Please stop the container!!!
docker stop sysout-ctr

```

Docker logs documentation : https://docs.docker.com/engine/reference/commandline/logs/
