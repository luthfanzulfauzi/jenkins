FROM jenkins/agent:alpine-jdk11
USER root
RUN apk add python3
RUN apk add py3-pip
RUN apk add pytest
RUN apk add junit
RUN pip install pyinstaller
apk add binutils
USER jenkins