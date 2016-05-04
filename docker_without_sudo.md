# Run `docker` without sudo on Linux

###### 1. Add the docker group if it doesn't already exist
```sh
sudo groupadd docker
```

###### 2. Add the connected user "${USER}" to the docker group. Change the user name to match your preferred user
```sh
sudo gpasswd -a ${USER} docker
```

###### 3. Restart the Docker daemon
```sh
sudo service docker restart
```
If you are on Ubuntu 14.04-15.10* use docker.io instead
```sh
sudo service docker.io restart
```
