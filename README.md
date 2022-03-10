##Day with Grafana Install as Monitor all Node 

#Day 1 : Install prometheus in Main Node "https://prometheus.io/download/#prometheus"

Install node_exporter In Main Node " https://prometheus.io/download/#node_exporter"

Command : 
```
wget prometheus.tar.gz 
tar -xvf prometheus.tar.gz
cd prometheus
```



#Day 2 : Select Node2,,3,4,5,6,
Install node_exporter In All Node " https://prometheus.io/download/#node_exporter"


Command : 
```
wget node_exporter.tar.gz
tar -xvf node_exporter.tar.gz
cd node_exporter
sudo ./node_exporter  run this For all Node 
```
Note : If you want to run it as background then 
```
nohup ./node_exporter & 

```

> to verfiy : 192.168.15.5:9100/metrics 

> Note : Must be Off Firewalld or ufw 


#Day 3 : 

> Config main node as prometheus 
```
vim /prometheus.yml 
```
```
scrape_configs:
- job_name: 'prometheus'
  static_configs:
  - targets: ['localhost:9090']
- job_name: 'Node-exporter'
  static_configs:
  - targets: ['23.92.xx.xx:9100','192.210.xx.xx:9100','172.245.xx.xx:9100','192.3.xx.xx:9100','192.3.xx.xx:9100','5.255.xx.xx:9100']
```

>Now Start  prometheus

```
./prometheus
```
if you want to run it as background then 
```
nohup ./prometheus & 
``` 

then check : 23.92.xx.xx:9090/targets
If all are Up Then Back to  Main Node 


#Day 4 : Install Grafana to Main Node 


```
vim /etc/yum.repos.d/grafana.repo
```
```
[grafana]
name=grafana
baseurl=https://packages.grafana.com/enterprise/rpm
repo_gpgcheck=1
enabled=1
gpgcheck=1
gpgkey=https://packages.grafana.com/gpg.key
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
```
```
sudo yum install grafana-enterprise
```
> Start the server with systemd
 To start the service and verify that the service has started:
```
sudo systemctl daemon-reload
sudo systemctl start grafana-server
sudo systemctl status grafana-server
```
Configure the Grafana server to start at boot:
```
sudo systemctl enable grafana-server
```

```
Now Login Grafana as Main_nodeIP:3000 
Email / username : admin 
Pass : admin 
```

Now add prometheus as data Source 

http://main_nodeIP:9090

Save & Test 


#Day 5 : Now Import a Dashboard From Grafana ID : 1860

> Now Check Your Grafana is Ready to Monitor 


> Help me to Setup This Video : https://youtu.be/G5ar-evGJzE

