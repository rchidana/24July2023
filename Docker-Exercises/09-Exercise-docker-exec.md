### docker exec command can be used to fire any commands to a running container

```
# Let us first pull the image
docker pull alpine

# Check if the image has been downloaded & also check its 'tag'
docker image ls

# Spin up a new container by specifying a name using --name option
# But let us NOT specify -i (interactive) and -t (tty/terminal) mode
docker run --name no-it-ctr1 -d alpine /bin/sh -c "while true; do date; sleep 5;done"

# List running containers - Check all attributes - name, cmd, image, status, creation timestamp & name
docker ps

# One can check the logs from the container using docker logs
docker logs no-it-ctr1

# Let us check if we can fire an exec command
docker exec no-it-ctr1 whoami
docker exec no-it-ctr1 ls
docker exec no-it-ctr1 date

# -it option can be used along with exec command to interactively ssh 
docker exec -it no-itr-ctr1 /bin/sh

# All interactions with the container can be carried out without any issues

```

docker exec command reference: https://docs.docker.com/engine/reference/commandline/exec/