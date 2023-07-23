### Run alpine based container but let us specify a name of our choice
### Alpine image documentation : https://hub.docker.com/_/alpine

```
# Let us first pull the image
docker pull alpine

# Check if the image has been downloaded & also check its 'tag'
docker image ls

# Spin up a new container by specifying a name using --name option
docker run --name my-ctr -itd alpine /bin/sh

# List running containers - Check all attributes - name, cmd, image, status, creation timestamp & name
docker ps

# attach to the container using its name
docker attach my-ctr

# The container can now be managed & controlled by using its name - my-ctr

```
