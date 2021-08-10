# kibana-setup-all
Kibana, Elastic, Log Stash, APM Server, APM Agent

Download all jars

Start Elastic elasticsearch-7.13.2 : /bin/.elasticsearch
http://localhost:9200
http://localhost:9200/_cat/indices

Change Property in config/kibana.yml
elasticsearch.hosts: ["http://localhost:9200"]
Start Kibana kibana-7.13.2-linux-x86_64
bin/.kibana
http://localhost:5601/
APM and Dashboard can see here


Log stash
logstash.conf

# Sample Logstash configuration for creating a simple
# Beats -> Logstash -> Elasticsearch pipeline.

input {
  tcp {
    port => 5044
    codec => json

  }
}

output {
  elasticsearch {
    hosts => ["http://localhost:9200"]
    index => "micro-%{appName}"
    #user => "elastic"
    #password => "changeme"
  }
}
Start logstash-7.13.2 
/bin/.logstash



APM Server
Check apm-server.yml having following property enabled
output.elasticsearch:
  # Array of hosts to connect to.
  # Scheme and port can be left out and will be set to the default (`http` and `9200`).
  # In case you specify and additional path, the scheme is required: `http://localhost:9200/path`.
  # IPv6 addresses should always be defined as: `https://[2001:db8::1]:9200`.
  hosts: ["localhost:9200"]

start apm-server-7.14.0-linux-x86_64 
./apm-server -e

APM Client
elastic-apm-agent-1.25.0.jar
java -javaagent:/home/techg/Desktop/ALL/software/elastic-apm-agent-1.25.0.jar -Delastic.apm.service_name=spring-boot-aop-test -Delastic.apm.application_packages=test,test.ashishjaintechg -Delastic.apm.server_url=http://localhost:8200 -jar /home/techg/Desktop/ALL/stsworkspace/spring-boot-aop-test/target/spring-boot-aop-test-0.0.1-SNAPSHOT.jar

or 
create a property file named elasticapm.properties in the same folder where jar is
service_name
application_packages
server_url









