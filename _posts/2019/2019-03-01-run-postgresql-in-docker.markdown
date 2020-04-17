---
title: "Run PostgreSQL in Docker"
date: "2019-03-01 15:49"
categories: ["PostgreSQL", "Docker", "Docker SSL Error", "SSL Error", "Ceterficate Error"]
---

It's easy and environment independent to run the PostgreSQL Docker.
* Get rid of the environment mess up while upgrading to a newer version
* Better management via Docker

### Command to Run the PostgreSQL Docker
```bash
docker run --name ${name} -e POSTGRES_PASSWORD=${PW} -e POSTGRES_USER=${USER} -e POSTGRES_DB=${DEFAULT DATABSE} --mount type=bind,source=${SOURCE ABS PATH},target=${TARGET PATH IN THE DOCKER} -p 5432:5432 -d postgres:latest
```

For more inforation about the offical PostgreSQL Docker image, check in [https://hub.docker.com/\_/postgres](https://hub.docker.com/\_/postgres).

If you encounter SSL error, try following steps to  resolve it.
```bash
  # copy the last PEM encoding certificate data
  openssl s_client -showcerts -connect www.example.com:443
  # append the PEM data to the file
  /usr/local/share/ca-certificates
  # update the certificates and restart the Docker service to take effetc
  sudo update-ca-certificates
  sudo service docker restart # or
  sudo systemctl restart docker
```

