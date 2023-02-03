# Run Docker commands without sudo

##### 1. Add the `docker` group if it doesn't already exist

```console
$ sudo groupadd docker
```

##### 2. Add the connected user `$USER` to the docker group

Optionally change the username to match your preferred user.

```console
$ sudo gpasswd -a $USER docker
```

**IMPORTANT**: Log out and log back in so that your group membership is re-evaluated.

##### 3. Restart the `docker` daemon

```console
$ sudo service docker restart
```

If you are on Ubuntu 14.04-15.10, use `docker.io` instead:

```console
$ sudo service docker.io restart
```
#### 4. Change the context from Docker Desktop to Engine
If you installed Docker Desktop first, then removed it and installed the Docker Engine, you may need to switch the Docker context with this command:

$ docker context use default

Because Docker Desktop switches context before startups and shutdowns not to interfere Docker Engine. So context might be kept incorrectly after removing Docker Desktop. A related article: https://www.howtogeek.com/devops/how-to-troubleshoot-cannot-connect-to-the-docker-daemon-errors/

https://stackoverflow.com/questions/73671461/docker-not-working-without-sudo-in-ubuntu-22-04
