# DockerK8s

Docer file exmaple :

Dockerfile

FROM jenkins/jenkins:2.249.2-jdk11
USER root 

RUN chmod 777 /home

RUN ln -s /var/jenkins_home /home/jenkins

USER jenkins
