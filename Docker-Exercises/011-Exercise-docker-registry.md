### Exercise to start local registry server using registry:v2
### Dockerhub Documentation https://hub.docker.com/_/registry

```
# Create a volume to store registry images

docker volume create registry_data
docker volume ls
docker inspect registry_data 

# Spin up local registry server on any port, let us use 8085
docker run -d -p 8085:5000 --restart=always --name registry -v registry_data:/var/lib/registry registry:2
docker ps

# Check the logs for any error
docker logs registry

# Open a browser and navigate to the registry URLs
http://localhost:8085/v2
http://localhost:8085/v2/_catalog

# For now, our registry server is empty
# Let us tag one of our local image and push it to our local registry
docker tag alpine:latest localhost:8085/alpine:latest
docker push localhost:8085/alpine:latest

# Check the registry contents using a browser
http://localhost:8085/v2
http://localhost:8085/v2/_catalog

# You can also inspect the local volume and check out its contents as well
docker inspect registry_data


```

### Further documentation : https://hub.docker.com/_/registry 