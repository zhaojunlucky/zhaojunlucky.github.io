---
date: 2017-12-25 14:35:37 +0800
categories: docker uwsgi
title: Docker Usage
update: 2018-12-11 09:57:01 +0800
---

### Run a MySQL Container
```
docker run --name={name} -p {host port}:3306 -e MYSQL_ROOT_PASSWORD={mysql root password} -e MYSQL_ROOT_HOST=localhost -d mysql/mysql-server:{mysql version} --config-entry-key=value
```

- Check container logs
  `docker logs {name}`
- Restore from dump files
  `cat {dump file} | docker exec -i {name} mysql -u{user} -p{pass} {database}`
- Enter MySQL console
  `docker exec -it {name} mysql -u{user} -p{pass}`

### Build a docker image
`docker build --force-rm=true -t {tag} {docker file directory}`

### Run a docker container with volume mount
`docker run --name={name} --privileged=true --detach=true -d {name} -h {docker hostname} --volume "/host/src":"/docker/target":rw -d {tag}`

### Run uwsgi in upstat mode in docker
`nohup uwsgi --master --emperor /etc/uwsgi/vassals --die-on-term --uid www-data --gid www-data --logto {log location} &`

### Login to a register repository
* Run `docker login <repository url>` will prompt to input the username and password if needed
* Check `/etc/docker/certs.d/` to add repository URL's cerficate if it's a self-signed cerficate

### Open bash with user 'root' in a running Container
Simply run `docker run -u 0 -it {container name} bash`

### One liner to stop / remove all of Docker containers
* `docker stop $(docker ps -a -q)`
* `docker rm $(docker ps -a -q)`

### Use bind mount
* `docker run {other args} --mount type=bind,source={host folder},target={docker folder},readonly`, readonly means only can read.

### Remove all dangling images
Simply run `docker rmi $(docker images -f "dangling=true" -q)`

### Remove all images
Simple run `docker image prune -a`
