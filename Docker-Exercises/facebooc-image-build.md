### Exercise to build an image for an opensource Facebooc Clone
### Source Code Reference : https://github.com/rchidana/facebooc
### instructions to Build this code : https://github.com/rchidana/facebooc/blob/master/README.md

```

# Let us spin up an empty container (name it 'fb') that is powered by ubuntu image
# Host Port 8085 is mapped to container port 16000 but any other available Host Port can be used 

docker run -itd --name fb -p 8085:16000 ubuntu bash

# Check if this container is running without any issues
docker ps

# Let us clone facebooc source code locally
git clone https://github.com/rchidana/facebooc.git

# Copy the source code (facebooc folder) to the running container (fb) under /opt folder
docker cp facebooc fb:/opt

# Let us get into the container & start building our application
docker exec -it fb bash

# The following commands are all run inside the 'fb' container
apt-get update
apt-get install -yq build-essential make libsqlite3-dev sqlite3

cd facebooc
make all

# Check for 'facebooc' binary within the bin folder
ls bin
bin/facebooc

```

### Check if facebooc application is accessible by opening a browser and hitting the url : http://<IP-ADDRESS-OF-YOUR-VM>:8085

### if everything looks good, let us create an image from our 'fb' container

```
# These commands are to be run outside 'fb' container

docker ps
docker container commit fb facebooc:v1 
docker images

# If you want to push this image to Dockerhub, pre-fix this image with your <dockerhub-id>

docker tag facebooc:v1 <your-dockerhub-id>/facebooc:v1
docker tag facebooc:v1 anandr72/facebooc:v1

docker push anandr72/facebooc:v1

```
