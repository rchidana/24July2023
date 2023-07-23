### Run alpine based container but let us specify a name of our choice
### If containers are started without -i (interactive) & -t (tty or terminal) mode
### The containers will not accept any inputs from the terminal
### Alpine image documentation : https://hub.docker.com/_/alpine

```
# Let us first pull the image
docker pull alpine

# Check if the image has been downloaded & also check its 'tag'
docker image ls

# Spin up a new container by specifying a name using --name option
# But let us NOT specify -i (interactive) and -t (tty/terminal) mode
docker run --name no-it-ctr -d alpine /bin/sh -c "while true; do date; sleep 5;done"

# List running containers - Check all attributes - name, cmd, image, status, creation timestamp & name
docker ps

# One can check the logs from the container using docker logs
docker logs no-it-ctr

# Let us check if we can login/attach to the container & type in any inputs/commands
docker attach no-it-ctr

# Are you able to type in any command? exit the container

```

Let us explore another docker command 'exec' that can be used with -it option to interact with containers
