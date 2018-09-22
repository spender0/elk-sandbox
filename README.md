# ELK sandbox
### Run ELK on your laptop.
### Get your ELK stack with only one 'docker-compose up' cmd
![alt text](https://lh5.googleusercontent.com/Bg7Zy2Lu0Qj7v4FvIKGqytFx1UlDx0IDwccLCQWAsHZ55qnRRvKLNEzPynjZu41ZfKgJx6rq-VwrXN2B0m1w=w1366-h675-rw)

### Features:
* Best for ELK studying, configuration testing and experiments.
* No installation routine, only docker required.
* No manual steps. All is defined in docker-compose and ELK config files.
* Well commented configuration. 
* Based on official Elastic.co containers https://www.docker.elastic.co and documentation. 

### Requirements:
* Install actual version of docker https://docs.docker.com/install/
* Install actual version of docker-compose https://docs.docker.com/compose/install/#install-compose
* Git https://git-scm.com/book/it/v2/Per-iniziare-Installing-Git

### Run ELK:
* Clone this repository and run docker-compose:
```
git clone https://github.com/spender0/elk-sandbox.git
cd elk-sandbox
docker-compose up -d
```
* Wait untill kibana is up and running:
```
docker ps -af name=elksandbox_kibana_1
```
* Open Kibana http://localhost:5601

### Remove ELK:
* Without dropping the volume containing elasticsearch data:
```
docker-compose down
```
* With dropping the volume:
```
docker-compose down -v
```

### How it works

ELK stack is a great example of Microservices implementation. Each component of ELK stack is responsible for it's own small task. Also all of ELK stack components are well dockerized as they should be in case of Microservices! That is why it is possible to define whole stack as just one docker-compose.yml file and deploy it with just one docker-compose cmd. 

Let's look into this example:

##### Metricsbeat
Beats are just lightweight shippers for logs, metrics and monitoring. 
in this example Metricbeat has been easily and promptly configured for monitoring host and docker service.
Metricbeat can also collect metrics from a pile of services (about 35) such as Apache, HAProxy, Kafka, Kubernetes, PostgreSQL and many others.  

##### Logstash
I cannot describe here all benefits of Logstash, it's name speaks for itself. Just read this https://www.elastic.co/guide/en/logstash/6.4/introduction.html

Logstash has a lot of input and output modules and in this case it is useful for routing logs direcly from docker containers to Logstash's gelf input bypassing writing the logs to local filesystem. It can be usefull when whole environment consists of docker containers only (e.g. Kubernetes) and you don't want to mess with hosts and their local fs to get the logs. Another benefit is decreasing host disk IOPS.

##### Elasticsearch
Elasticsearch is a search and analytics engine which can store, search, and analyze data.

In this example it stores metrics of your laptop and it's docker service as well as logs generated by test container.
 
##### Kibana
Kibana is an open source analytics and visualization platform for Elasticsearch. It is used to search, view, and interact with data stored in Elasticsearch.

In this example you can find metrics of your laptop and it's docker service in "Dashboards" section
Also you can find logs that are generated by test container in "Discover" section.
