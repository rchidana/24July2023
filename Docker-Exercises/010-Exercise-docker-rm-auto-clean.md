### docker by default persists the containers even after they crash, exit or stop
### docker run command has --rm option which will automatically remove the container upon exit

```
# Let us spin up an alpine container with --rm option
# Start this in foreground
docker run --rm --name disappear -it alpine /bin/sh

# Type in few commands inside the container & then exit
exit

# Check if you can find 'disappear' container!!
docker ps -aq

```

docker exec command reference: https://docs.docker.com/engine/reference/commandline/exec/