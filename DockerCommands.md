# DockerK8s
<p>


# Clean unsed images
  docker image prune -a
  docker volume prune -f
  docker system prune

 
# Push to nexus 
  
 <p> docker login </p>

 sudo docker login -u \<username> -p \<Pass> \<server>:\<port>

<p> Prepare the tag  </p>

  sudo docker tag \<Local Full Image name> \<server>:\<port>/path/\<Image Name>:tag
  
  exmaple :
  
  sudo docker tag dpage/pgadmin4:4.18 \<server>:\<port>
  
 then push : 
 
   sudo docker push  \<server>:\<port>/pgadmin/pgadmin4:4.18
 
 
 
## configure the proxy 
 
    docker pull postgres:latest 
    
 <p> reate a systemd drop-in directory for the docker service:

 <p> 
 <p> in jenkins for example,  no  jobs that running in parallel at time  , duration of each job , active running jobs at time ( it will show the trend of the growing or trade of performance and respond time ,
 <p>                               Respond time of the jenkins page load .
 <p>                              Failed  Build errors what error and frequency for each job ,later we can categorize which failed are related to the platform or anything else .
 <p> 
 <p> 
    sudo mkdir -p /etc/systemd/system/docker.service.d
    
  Create a file named /etc/systemd/system/docker.service.d/http-proxy.conf that adds the HTTP_PROXY environment variable:
  
 <p> 
 
    [Service]
    Environment="HTTP_PROXY=http://proxy.example.com:80"
    
 <p> If you are behind an HTTPS proxy server, set the HTTPS_PROXY environment variable:
 <p> 
 
    [Service]
    Environment="HTTPS_PROXY=https://proxy.example.com:443"
 
 <p> Multiple environment variables can be set; to set both a non-HTTPS and a HTTPs proxy;
 <p> 
 
   [Service]
   Environment="HTTP_PROXY=http://proxy.example.com:80"
   Environment="HTTPS_PROXY=https://proxy.example.com:443"
   
   If you have internal Docker registries that you need to contact without proxying you can specify them via the NO_PROXY environment variable.
 <p> 
 <p> The NO_PROXY variable specifies a string that contains comma-separated values for hosts that should be excluded from proxying. These are the options you can specify to exclude hosts:
 <p> 
 <p> IP address prefix (1.2.3.4)
 <p> Domain name, or a special DNS label (*)
 <p> A domain name matches that name and all subdomains. A domain name with a leading “.” matches subdomains only. For example, given the domains foo.example.com and example.com:
 <p> example.com matches example.com and foo.example.com, and
 <p> .example.com matches only foo.example.com
 <p> A single asterisk (*) indicates that no proxying should be done
 <p> Literal port numbers are accepted by IP address prefixes (1.2.3.4:80) and domain names (foo.example.com:80)
 <p> Config example:
    
    [Service]
    Environment="HTTP_PROXY=http://proxy.example.com:80"
    Environment="HTTPS_PROXY=https://proxy.example.com:443"
    Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp"
 
 # insecure-registries  work wihth http 
 
   edit teh file /etc/docker/daemon.json
   
   {  "insecure-registries" : [ "\<Server Name>:\<port> " , "\<server>:\<port>" ,"\<server>:\<port> "]  }
