# Docker Installation Instructions for Ubuntu 22.04

Detailed PDFs for DevOps Tools from my Corp Training Sessions can be found here : 
https://drive.google.com/drive/folders/1spz_bxLOic4Bit7-YNni72YAqtWaskSX?usp=sharing <br>

Docker Playground : https://labs.play-with-docker.com/ (Dockerhub credentials required) <br>
K8s Playground : https://killercoda.com/login (Gmail, GitHub & GitLab credentials work) <br>

My YouTube Channel for reference : https://www.youtube.com/channel/UC-Hv6dZTH_9rj_nezOSa9Iw <br>

### Installing Latest Docker CE on Ubuntu:

### Update Ubuntu Libraries
```
sudo apt-get update
```


### Install Latest version of Docker CE
```
sudo apt-get install docker.io
```

### Check if docker service is running
```
sudo systemctl status docker
```

### If not running, start it
```
sudo systemctl start docker
```

### Add ubuntu user rps to docker user group
```
sudo usermod -aG docker ubuntu (username)
```

### Open a new Terminal (duplicate Putty session)

### OR refresh docker group with the command (so that the usermod takes effect)

```
newgrp docker
```

### Check if docker is running
```
docker version
```

### Run Docker hello-world image
```
docker run -it hello-world
```


### For installing specific Docker version, check out docker documentation : https://docs.docker.com/engine/install/ubuntu/
