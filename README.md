# System Alerting and Monitoring (SAM) 
System Alerting and Monitoring or SAM is an easy-to-use cluster monitoring solution for InterSystems IRIS® data platform version 2020.1 and later. 
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
      You can download InterSystems SAM Community Edition container from  
      - [InterSystems WRC download page](https://wrc.intersystems.com/wrc/coDistribution.csp) (select the Containers button) or  
      - pull it from [Docker Hub](https://hub.docker.com/_/intersystems-system-alerting-and-monitoring)  
   3. Have access to Docker Hub (https://hub.docker.com/). If you do not have an account, you should create one.


## CLONE or DOWNLOAD the TARBALL
Either git-clone this repository or download the tarball + uncompress & untar it, as shown below  
- please make sure to include the **p** switch below as to maintain the correct file privileges  
   ```$ tar zpxvf sam-<version>.tar.gz```


## RUN THE DOCKER-COMPOSE BUNDLE
To run SAM you just need to issue a *docker-compose* command. Simpler yet, use the wrapper *start.sh* and *stop.sh* scritps we provide for your convenience. Type the following at the prompt:

```
$ cd sam-<version>
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
Creating sam_alertmanager_1 ... done  
Creating sam_nginx_1      ... done  
```   
   
You can verify that all four containers are running by via *docker ps*, such as:
```  
$ docker ps
CONTAINER ID        IMAGE                                               COMMAND                  CREATED              STATUS                        PORTS                                                  NAMES
78ebb8f7cee3        nginx:1.17.9-alpine                                 "nginx -g 'daemon of…"   About a minute ago   Up About a minute             80/tcp, 0.0.0.0:8080->8080/tcp                         sam_nginx_1
d73234723046        prom/alertmanager:v0.20.0                           "/bin/alertmanager -…"   About a minute ago   Up About a minute             9093/tcp                                               sam_alertmanager_1
90450018cab1        grafana/grafana:6.7.1                               "/run.sh"                About a minute ago   Up About a minute             3000/tcp                                               sam_grafana_1
12a47da64b2c        prom/prometheus:v2.17.1                             "/bin/prometheus --w…"   About a minute ago   Up About a minute             9090/tcp                                               sam_prometheus_1
9d4dac95921a        store/intersystems/sam:1.0                          "/iris-main"             About a minute ago   Up About a minute (healthy)   2188/tcp, 51773/tcp, 52773/tcp, 53773/tcp, 54773/tcp   sam_iris_1
```  


To shut down SAM run:  
```$ ./stop.sh```


## CONNECT TO SAM WITH YOUR BROWSER
In your browser, visit:  
	```http://<ip-address-of-host-where-SAM-runs>:8080/api/sam/app/index.csp```  
You'll be prompted to login. You can use standard InterSystems IRIS credentials like _SYSTEM/SYS. You'll be prompted to change the password.

## LEARN MORE ABOUT SAM
[SAM documentation](https://docs.intersystems.com/sam/csp/docbook/Doc.View.cls?KEY=ASAM)

[IRIS native Prometheus exporter documentation](https://docs.intersystems.com/irislatest/csp/docbook/DocBook.UI.Page.cls?KEY=GCM_rest)

---
