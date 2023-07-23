### Run alpine based container but let us specify a name of our choice
### Let us create a bunch of files in this container and then use diff command to check
### what has been modified!!
### Alpine image documentation : https://hub.docker.com/_/alpine

```
# Let us first pull the image
docker pull alpine

# Check if the image has been downloaded & also check its 'tag'
docker image ls

# Spin up a new container by specifying a name using --name option
docker run --name my-alp-ctr -itd alpine /bin/sh

# List running containers - Check all attributes - name, cmd, image, status, creation timestamp & name
docker ps

# Let us get into the container & create couple of files in it
docker attach my-alp-ctr
echo "Hello World" >> hello.txt
echo "Greetings!!" >> greetings.txt
exit

# Exit the container or explicitly stop the container
docker stop my-alp-ctr

# Use diff command to find all modifications or changes
docker diff my-alp-ctr

```

Docker diff documentation : https://docs.docker.com/engine/reference/commandline/diff/
