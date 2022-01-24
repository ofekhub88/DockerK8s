# DockerK8s
<br>



# Clean unsed images
 <br> docker image prune -a
 <br> docker volume prune -f
 <br> docker system prune

 
# Push to nexus 
 <br> 
 <br> docker login 
 <br> 
 <br> sudo docker login -u \<username> -p <Pass> <server>:port
 <br> 
 <br> P repare the tag 
  sudo docker tag \<Local Full Image name> <server>:port/path/<Image Name>:tag
 <br> exmaple :
 <br> sudo docker tag dpage/pgadmin4:4.18 <server>:port
 <br> then push 
 <br> sudo docker push <server>:port/pgadmin/pgadmin4:4.18
 <br> 
 <br> 
 
## configure the proxy 
 
 <br> docker pull postgres:latest
 <br> reate a systemd drop-in directory for the docker service:

 <br> 
 <br> in jenkins for example,  no  jobs that running in parallel at time  , duration of each job , active running jobs at time ( it will show the trend of the growing or trade of performance and respond time ,
 <br>                               Respond time of the jenkins page load .
 <br>                              Failed  Build errors what error and frequency for each job ,later we can categorize which failed are related to the platform or anything else .
 <br> 
 <br> 
 <br> sudo mkdir -p /etc/systemd/system/docker.service.d
 <br> Create a file named /etc/systemd/system/docker.service.d/http-proxy.conf that adds the HTTP_PROXY environment variable:
 <br> 
 <br> [Service]
 <br> Environment="HTTP_PROXY=http://proxy.example.com:80"
 <br> If you are behind an HTTPS proxy server, set the HTTPS_PROXY environment variable:
 <br> 
 <br> [Service]
 <br> Environment="HTTPS_PROXY=https://proxy.example.com:443"
 <br> Multiple environment variables can be set; to set both a non-HTTPS and a HTTPs proxy;
 <br> 
 <br> [Service]
 <br> Environment="HTTP_PROXY=http://proxy.example.com:80"
 <br> Environment="HTTPS_PROXY=https://proxy.example.com:443"
 <br> If you have internal Docker registries that you need to contact without proxying you can specify them via the NO_PROXY environment variable.
 <br> 
 <br> The NO_PROXY variable specifies a string that contains comma-separated values for hosts that should be excluded from proxying. These are the options you can specify to exclude hosts:
 <br> 
 <br> IP address prefix (1.2.3.4)
 <br> Domain name, or a special DNS label (*)
 <br> A domain name matches that name and all subdomains. A domain name with a leading “.” matches subdomains only. For example, given the domains foo.example.com and example.com:
 <br> example.com matches example.com and foo.example.com, and
 <br> .example.com matches only foo.example.com
 <br> A single asterisk (*) indicates that no proxying should be done
 <br> Literal port numbers are accepted by IP address prefixes (1.2.3.4:80) and domain names (foo.example.com:80)
 <br> Config example:
 <br> 
 <br> [Service]
 <br> Environment="HTTP_PROXY=http://proxy.example.com:80"
 <br> Environment="HTTPS_PROXY=https://proxy.example.com:443"
 <br> Environment="NO_PROXY=localhost,127.0.0.1,docker-registry.example.com,.corp"
 
 # insecure-registries  work wihth http 
 
 <br>  edit teh file /etc/docker/daemon.json
 <br>   {
    "insecure-registries" : [ ""Server Name: port " , "Server Name: port " ,""Server Name: port "]
}
