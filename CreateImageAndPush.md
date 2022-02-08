# Dokerfile example
FROM jenkins/jenkins:2.263.3-jdk11

USER root

RUN chmod 777 /home

RUN ln -s /var/jenkins_home /home/jenkins

USER jenkins


================================
<b>
docker build . \n
docker images \n
docker tag jenkins/jenkins  <NexusDockerImagePath:2.263.3-jdk11
docker push  <NexusDockerImagePath:2.263.3jdk11>
  </b>
