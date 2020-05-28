--
Readme.txt for System Alerting and Monitoring (SAM) bundle

SAM is an easy-to-use cluster monitoring solution for InterSystems IRIS® 
data platform version 2020.1 and later. SAM leverages the open-source 
technologies Prometheus and Grafana, augmenting their features with 
enterprise resiliency to provides a cohesive view of your application 
infrastructure.

You can deploy SAM by running one docker-compose command. The 
docker-compose.yml file defines all the needed containers and components, 
making SAM easy to set up.

For the complete documentation, visit:
   https://docs.intersystems.com/sam/csp/docbook/Doc.View.cls?KEY=ASAM


PREPARE TO PULL CONTAINERS
----------
There are 3 requirements for a successful automated run of SAM:
   1. Have Docker Compose v1.25+ installed on the Docker Engine v19.3+. 
      Depending on your platform:		 
      a. On Linux, you must install Docker Compose, as well as the
         Docker Engine. For instructions, visit:
            https://docs.docker.com/compose/install/
      b. Docker Compose is included in Docker Desktop. To install, see:
            Docker Desktop for Windows:
               https://docs.docker.com/docker-for-windows/install/
            Docker Desktop for Mac:
               https://docs.docker.com/docker-for-mac/install/
   2. Have access to the InterSystems SAM container in a container registry.
      The InterSystems SAM container is available from the WRC download page 
      (and will soon be available on Docker Hub).
   3. Have access to Docker Hub (https://hub.docker.com/). If you do not 
      have an account, you must create one.


UNZIP AND UNTAR
----------
Uncompress the distribution file, as shown below:
   $ tar zpxvf SAM-<version>.tar.gz


RUN THE DOCKER-COMPOSE BUNDLE
----------
To run SAM, user docker-compose or enter the following in the command line:
   $ cd SAM-<version>
   $ ./start.sh

The first time you run SAM, Docker takes several seconds 
(depending on your network) to pull the various containers. 
When the command is finished (and on subsequent runs), you should 
see the following lines confirming that SAM is up and running:
   Creating sam_iris_1 ... done
   Creating sam_prometheus_1 ... done
   Creating sam_grafana_1    ... done
   Creating sam_alertmanager_1 ... done
   Creating sam_nginx_1      ... done

You can verify that all four containers are running by via docker ps, such as:
$ docker ps
CONTAINER ID        IMAGE                                              COMMAND                  CREATED             STATUS                   PORTS                                                  NAMES
389b58657d96        nginx:1.17.9-alpine                                "nginx -g 'daemon of…"   3 minutes ago       Up 3 minutes             80/tcp, 0.0.0.0:8080->8080/tcp                         sam_nginx_1
1b50ea425058        grafana/grafana:6.7.1                              "/run.sh"                3 minutes ago       Up 3 minutes             3000/tcp                                               sam_grafana_1
d2c825f9d220        prom/alertmanager:v0.20.0                          "/bin/alertmanager -…"   3 minutes ago       Up 3 minutes             9093/tcp                                               sam_alertmanager_1
18ba4eed08dd        prom/prometheus:v2.17.1                            "/bin/prometheus --w…"   3 minutes ago       Up 3 minutes             9090/tcp                                               sam_prometheus_1
5bc04b24c221        intersystems/sam:1.0.0.63                          "/iris-main"             3 minutes ago       Up 3 minutes (healthy)   2188/tcp, 51773/tcp, 52773/tcp, 53773/tcp, 54773/tcp   sam_iris_1

If you need to shut down SAM, use the following script:
   $ ./stop.sh


CONNECT TO SAM WITH YOUR BROWSER
----------
In your preferred web browser, visit:
	http://<ip-address-of-host-where-SAM-runs>:8080/api/sam/app/index.csp


LEARN MORE ABOUT SAM
----------
SAM documentation:
      https://docs.intersystems.com/sam/csp/docbook/Doc.View.cls?KEY=ASAM

IRIS native Prometheus exporter documentation:
      https://docs.intersystems.com/irislatest/csp/docbook/DocBook.UI.Page.cls?KEY=GCM_rest

--
