# Dokerfile example #
***
FROM jenkins/jenkins:2.263.3-jdk11

USER root

RUN chmod 777 /home

RUN ln -s /var/jenkins_home /home/jenkins

USER jenkins


================================
docker build . \n
docker images \n
docker tag jenkins/jenkins  <NexusDockerImagePath:2.263.3-jdk11
docker push  <NexusDockerImagePath:2.263.3jdk11>
  ***


# Create from container

docker commit <Vontainer name >
 
 docker imgaes 
 
 ( the new created image look like ) 
 
< None >   <none>     3368fcdd1edd   33 minutes ago   1.91GB
 
 docker tag 3368fcdd1edd < Your new Registry name with tag >
 
 docker push 
 
