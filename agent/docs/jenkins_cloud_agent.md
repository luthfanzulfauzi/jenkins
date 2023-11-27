### Jenkins Cloud Agent

Create Docker file
Source : [Jenkins Cloud Agent Dockerfile](https://github.com/luthfanzulfauzi/jenkins/blob/main/agent/config/Dockerfile)
```
vi Dockerfile
```

Build image from Dockerfile
```
docker build -t luthfanfauzi/jenkins-slave:alpine-jdk11-py-v2 .
docker build -t <dockerhubuser>/<repository>:<imagetag> .
```

Push image to docker hub repository
```
docker login
docker push luthfanfauzi/jenkins-slave:alpine-jdk11-py
docker push <dockerhubuser>/<repository>:<imagetag>
```

Configure Jenkins Cloud Agent

Docker Cloud Details, for docker host URI use IP from alpine/socat container.
![dockerclouddetails](dockerclouddetails.png "Docker Cloud Details")

Docker Agent Template
![dockeragenttemp](dockeragenttemp.png "Docker Agent Template")