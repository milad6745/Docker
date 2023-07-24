# push to docker hub
**login to docker**
```
docker login
username : milad6745
pass : m****5
```
**create tag and push to docker hub**
```
docker tag <container name> <username>/containername:v1
docker tag nginx:latest milad6745/newnginx:v1 #  push to docker hub
```
**pull from docker hub**
```
docker pull milad6745/newnginx:v1
```
