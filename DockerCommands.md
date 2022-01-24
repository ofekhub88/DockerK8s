# DockerK8s
<p>



# Clean unsed images
  docker image prune -a
  docker volume prune -f
  docker system prune

 
# Push to nexus 
  
 <p> docker login </p>

 sudo docker login -u \<username> -p \<Pass> \<server>:\<port>

 Prepare the tag  
  sudo docker tag \<Local Full Image name> \<server>:\<port>/path/\<Image Name>:tag
  exmaple :
  <p>
  sudo docker tag dpage/pgadmin4:4.18  \<server>:\<port>
 then push 
   sudo docker push  \<server>:\<port>/pgadmin/pgadmin4:4.18
