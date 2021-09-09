# Ejemplo basico del stack Prometheus/PushGateway/Grafana

Ejemplo básico:
https://devconnected.com/monitoring-linux-processes-using-prometheus-and-grafana/ 

Info sobre pushwateways
https://github.com/prometheus/pushgateway#about-the-job-and-instance-labels 

![prometheus](https://user-images.githubusercontent.com/61946077/132702080-03804e4d-d320-41d5-8a54-c424a982904c.png)
![pushWorkflow](https://user-images.githubusercontent.com/61946077/132702083-cf3068ea-c39d-4e78-88d5-d5967d75e6dc.png)
![metrics](https://user-images.githubusercontent.com/61946077/132702079-8ba10b49-d795-4179-81ce-d58744409739.png)


## Ejecución de componenetes sobre contenedores
https://hub.docker.com/r/prom/prometheus 

### Installing Docker PROMETHEUS 

docker pull prom/prometheus 

sudo docker run  --name prometheus -d -p 9090:9090  -v /home/henry/Repositorios/isbel/veramonitor/src/prometheus/db:/prometheus -v /home/henry/Repositorios/isbel/veramonitor/src/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml -v /home/henry/Repositorios/isbel/veramonitor/src/prometheus/targets.json:/etc/prometheus/targets.json prom/prometheus --config.file=/etc/prometheus/prometheus.yml 

 

#### Note: Para montar volumenes persistentes hay que habilitar los permisos respectivos en el filesystem host 

 

Para saber el usuario bajo el cual corre la aplicacion ejecutar 

sudo docker inspect prom/prometheus | grep -A2 -i "user" 

En este caso como el usuario es nobody se saca el UID de la siguiente manera: 

sudo docker run –name prometheus prom/prometheus 

sudo docker exec -it prometheus /bin/sh 

Cat /proc/sys/fs/overflowuid 

exit 

sudo chown -Rv 65534:65534 ./db 

### Installing Docker PUSH GATEWAY 


sudo docker run --name pushgateway -d -p 9091:9091 prom/pushgateway 

### Installing Docker Grafana 
Sudo docker run -d --name=grafana -p 3000:3000 grafana/grafana 
