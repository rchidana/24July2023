### docker by default persists the containers even after they crash, exit or stop
### docker run command has --rm option which will automatically remove the container upon exit

```
# Let us spin up an alpine container with --rm option
# Start this in foreground
docker run --rm --name disappear -it alpine /bin/sh

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