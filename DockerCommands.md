# DockerK8s
<p>



# Clean unsed images
  docker image prune -a
  docker volume prune -f
  docker system prune

 
# Push to nexus 
  
 <p> docker login </p>

 sudo docker login -u \<username> -p \<Pass> \<server>:\<port>
 <p> Prepare the tag  /p<>
 sudo docker tag \<Local Full Image name> <server>:<port>/path/<Image Name>:tag
 
