### Run alpine based container but let us specify a name of our choice
### Container can be stopped & restarted by using its name or id
### Alpine image documentation : https://hub.docker.com/_/alpine

```
# Let us first pull the image
docker pull alpine

# Check if the image has been downloaded & also check its 'tag'
docker image ls

# Spin up a new container by specifying a name using --name option
docker run --name named-ctr -itd alpine /bin/sh

# List running containers - Check all attributes - name, cmd, image, status, creation timestamp & name
docker ps

# Let us stop the container
docker stop named-ctr
docker ps

# We can restart an exited container, either by its name or id
docker start named-ctr

# The container can now be managed & controlled by using its name - my-ctr

```
