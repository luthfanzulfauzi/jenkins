### Jenkins Master Configuration

Create Docker file
Source : [Jenkins Master Dockerfile] ()
```
vi Dockerfile
```

Build image from Dockerfile
```
docker build -t myjenkins-blueocean:2.429 .
```

Create jenkins docker network
```
docker network create jenkins
docker network ls
```

Run Jenkins Master container
```
docker run --name jenkins-blueocean --restart=on-failure --detach \
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 \
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.429
```

Get Initial Password
```
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword
```

Connect to Jenkins Master
```
https://localhost:8080/
```

Run alpine/socat container
This used to forward traffic from Jenkins to Docker
Reference: [devopsjourney1] (https://github.com/devopsjourney1/jenkins-101)
```
docker run -d --restart=always -p 127.0.0.1:2376:2375 --network jenkins -v /var/run/docker.sock:/var/run/docker.sock alpine/socat tcp-listen:2375,fork,reuseaddr unix-connect:/var/run/docker.sock
docker inspect <container_id> | grep IPAddress
```