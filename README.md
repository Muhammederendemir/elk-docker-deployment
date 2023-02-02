# 🎯 ELK Docker Deployment


## 📦 Project Architecture

![ELK Arch](https://github.com/Muhammederendemir/elk-docker-deployment/blob/main/docs/image/ELK-Arch.png)



## 🤔 What is ELK

**ELK** stands for **Elasticsearch**, **Logstash**, and **Kibana**. ELK is an open-source data indexing, collection, and analytics solution for data mining, visualization, and reporting. **Elasticsearch** is a database that can index and search data quickly and scalably. **Logstash** is a data source used to collect, transform, and send data to Elasticsearch. **Kibana** is a web interface used to visualize Elasticsearch data, create interactive reports, and explore data. **ELK system** is a useful solution for organizations that collect a high volume of log files and other data on a daily basis and wish to analyze them.




## 🤙🏼 Used Technologies

**Technologies:** 
- Docker
- Docker Compose

**3.Party Tools:** 
- Elasticsearch:
    - docker.elastic.co/elasticsearch/elasticsearch:7.10.0
- Logstash;
    - docker.elastic.co/logstash/logstash:7.10.0
- Kibana;
    - docker.elastic.co/kibana/kibana:7.10.0
## 👌🏼 Deployment

We can customize the **./logstash/config/logstash.yml** file.

```json
input {
  tcp{
	port => 5000
	codec => json
  }
}
 
output {
 
  elasticsearch {
    hosts => "elasticsearch:9200"
	index => "springboot-%{app}"
  }
} 
```
To summarize the **logstash.conf** file, This Logstash configuration file listens to incoming data over a TCP port and sends it to Elasticsearch. It also processes the data in JSON format.

In the input section, the tcp input is defined and the inputs are read from port **5000**. The codec for the inputs is also defined as json.

In the output section, Elasticsearch is defined as the destination for the data and the Elasticsearch host is set to **elasticsearch:9200**. Additionally, the Elasticsearch index name is defined as **"springboot-%{app}"** and the variable **%{app}** can change based on the "app" field in the inputs, allowing the data to be indexed separately for different applications.

We can customize the **./logstash/pipeline/logstash.conf** file.

 ```json
# Set Logstash HTTP API host
http.host: "0.0.0.0"

# Set the location of Logstash pipeline configurations
path.config: /usr/share/logstash/pipeline

# Set the Elasticsearch hosts to which Logstash will send monitoring data
xpack.monitoring.elasticsearch.hosts: [ "localhost:9200" ]

```
The following Logstash YAML configuration file sets several Logstash settings:

- The **http.host** setting sets the host for the Logstash HTTP API to listen on. Its value "0.0.0.0" specifies that the API should listen on all available network interfaces.
- The **path.config** setting specifies the location of Logstash pipeline configurations.
- The **xpack.monitoring.elasticsearch.hosts** setting is used to set the Elasticsearch hosts to which Logstash will send monitoring data.


It can be customized based on the comment lines found in the **docker-compose.yaml** file and then run this project to deploy.

```bash
  docker-compose up -d
```

  
## 🤟🏼 Run it on your computer

Clone the project

```bash
  git clone 
```

Go to the project directory

```bash
  cd 
```

Run 3rd Party products with Docker

```bash
  docker-compose up -d 
```



  
##  🫳🏼 Associated Projects

Here are some related projects


  