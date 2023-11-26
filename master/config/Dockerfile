FROM  jenkins/jenkins:2.429-jdk11
USER root
RUN apt-get update && apt-get install -y lsb-release
RUN for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do apt-get remove $pkg; done
RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg
RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list
RUN apt-get update && apt-get install -y docker-ce docker-ce-cli && usermod -aG docker jenkins
RUN apt-get install -y python3
USER jenkins
RUN jenkins-plugin-cli --plugins "blueocean:1.27.8 docker-workflow:1.29"