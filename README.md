# System Alerting and Monitoring (SAM) 
System Alerting and Monitoring or SAM is an easy-to-use cluster monitoring solution for InterSystems IRIS® data platform version 2019.4 and later. 
SAM leverages the open-source technologies Prometheus and Grafana, augmenting their features with enterprise resiliency to provides a cohesive view of your application infrastructure.

You can deploy SAM by running one *docker-compose* command. The docker-compose.yml file defines all the needed containers and components, 
making SAM easy to set up.

For the complete documentation, visit the [System Alerting and Monitoring guide](https://docs.intersystems.com/sam/csp/docbook/Doc.View.cls?KEY=ASAM).


## PREPARE TO PULL CONTAINERS
There are 3 requirements for a successful automated run of SAM:  
   1. Have Docker Compose v1.25+ installed on the Docker Engine v19.3+. Depending on your platform:  
      * On Linux, you must install Docker Compose, as well as the Docker Engine. For instructions, visit [Docker Compose install](https://docs.docker.com/compose/install/)  
      * On desktops, Docker Compose is included with Docker Desktop, so by installing it you have all the necessary components. Head over to the respective platform link if you need to install it:  
      - [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)   
      - [Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)  
   2. Have access to the InterSystems SAM container in a container registry.
      You can pull InterSystems SAM Community Edition container from  
      - [InterSystems WRC download page](https://wrc.intersystems.com/wrc/coDistribution.csp) or  
      - [Docker Hub](https://hub.docker.com/_/intersystems-system-alerting-and-monitoring)  
   3. Have access to Docker Hub (https://hub.docker.com/). If you do not have an account, you must create one.


## UNZIP AND UNTAR
Uncompress the distribution file, as shown below  
   ```$ tar zpxvf SAM-<version>.tar.gz```


## RUN THE DOCKER-COMPOSE BUNDLE
To run SAM you just need to issue a docker-compose command. Simpler yet, use the wrapper *start.sh* and *stop.sh* scritps we provide for your convenience. Type the followong at the prompt:

```
$ cd SAM-<version>
$ ./start.sh
```
   
The first time you run SAM, Docker takes several seconds 
(depending on your network) to pull the various containers. 
When the command is finished (and on subsequent runs), you should 
see the following lines confirming that SAM is up and running:   
```  
Creating sam_iris_1 ... done  
Creating sam_prometheus_1 ... done  
Creating sam_grafana_1    ... done   
Creating sam_nginx_1      ... done  
```   
   
You can verify that all four containers are running by via docker ps, such as:
```  
$ docker ps
CONTAINER ID        IMAGE                                              COMMAND                  CREATED             STATUS                   PORTS                                                  NAMES
389b58657d96        nginx:1.17.9-alpine                                "nginx -g 'daemon of…"   3 minutes ago       Up 3 minutes             80/tcp, 0.0.0.0:8080->8080/tcp                         sam_nginx_1
1b50ea425058        grafana/grafana:6.7.1                              "/run.sh"                3 minutes ago       Up 3 minutes             3000/tcp                                               sam_grafana_1
18ba4eed08dd        prom/prometheus:v2.17.1                            "/bin/prometheus --w…"   3 minutes ago       Up 3 minutes             9090/tcp                                               sam_prometheus_1
5bc04b24c221        intersystems/sam:1.0.0.63                          "/iris-main"             3 minutes ago       Up 3 minutes (healthy)   2188/tcp, 51773/tcp, 52773/tcp, 53773/tcp, 54773/tcp   sam_iris_1
```  


To shut down SAM run:  
```$ ./stop.sh```


## CONNECT TO SAM WITH YOUR BROWSER
In your preferred web browser, visit:  
	```http://<ip-address-of-host-where-SAM-runs>:8080/api/sam/app/index.csp```
You'll be prompted to login. You can use standard InterSystems IRIS credentials like _SYSTEM/SYS and then be prompted to change the password.

## LEARN MORE ABOUT SAM
[SAM documentation](https://docs.intersystems.com/sam/csp/docbook/Doc.View.cls?KEY=ASAM)

[IRIS native Prometheus exporter documentation](https://docs.intersystems.com/irislatest/csp/docbook/DocBook.UI.Page.cls?KEY=GCM_rest)

---
