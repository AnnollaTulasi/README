# Monitoring
* Blackbox testing --we dont't know what is inside
* Whitebox testing -- we know what is inside --memory ,CPU,RAM,Network

# Four Golden signals that are to be measured are:
* Latency
* Errors
* Traffic 
* Saturation

**We use Prometheus,Grafana,ELK for monitoring**
**PROMETHEUS**
- This is agent based
- We have one main server and all the instances which are to be monitored are installed with node_exporter agent
- Time Series Database

Prometheus installation
```
- wget https://github.com/prometheus/prometheus/releases/download/v3.2.1/prometheus-3.2.1.linux-amd64.tar.gz
- tar -xf <tarfile>
-mv <tar> <rename>
```

# Sample service file
```
[Unit]
Description=Prometheus server

[Service]
ExecStart=/opt/prometheus/prometheus --config-file=/opt/prometheus/prometheus.yml

[Install]
WantedBy=multi-user.target
```
- Add the above prometheus service in server path vim /etcd/systemd/system/prometheus.service
- systemctl start prometheus

# NODEEXPORTER SERVICE
```
[Unit]
Description=Node exporter

[Service]
ExecStart=/opt/node_exporter/node_exporter

[Install]
WantedBy=multi-user.target
```

- In prometheus.yml we have scaping component,in that which ever servers are to be checked or scraped has to be added
# Service Discovery,Alert Manager