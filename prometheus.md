#Kubernetes cluster is up and running

###Open ports 9090,9100,3000
 
 ```sh
wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
```
```sh
 tar xvfz prometheus-2.52.0.linux-amd64.tar.gz
```

```sh
  mv prometheus-2.52.0.linux-amd64 /etc/prometheus
```
```sh
 nano /etc/systemd/system/prometheus.service
```
```sh 
 [Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target
[Service]
ExecStart=/etc/prometheus/prometheus --config.file=/etc/prometheus/prometheus.yml
Restart=always
[Install]
WantedBy=multi-user.target 
```

```sh
systemctl daemon-reload
```
```sh
systemctl enable prometheus
```
```sh
systemctl restart  prometheus
```
```sh
systemctl status  prometheus
```
Check in browser with Ip:9090

# Install node_exporter

```sh
wget https://github.com/prometheus/node_exporter/releases/download/v1.8.0/node_exporter-1.8.0.linux-amd64.tar.gz
```
```sh
tar xvfz node_exporter-1.8.0.linux-amd64.tar.gz
```
```sh
 mv node_exporter-1.8.0.linux-amd64  /etc/node_exporter
```
```sh
 nano /etc/systemd/system/node_exporter.service
``` 


Node exporter systemd file
============================
```sh
nano /etc/systemd/system/node_exporter.service
```
```sh
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target
[Service]
ExecStart=/etc/node_exporter/node_exporter
Restart=always
[Install]
WantedBy=multi-user.target
```
```sh
systemctl enable node_exporter
```
```sh
systemctl restart node_exporter
```
```sh
systemctl status node_exporter
```
check in broswer with ip:9100

Prometheus scrape file
==========================
```sh
rm -rf /etc/prometheus/prometheus.yml
```
```sh
sudo vi /etc/prometheus/prometheus.yml
```
```sh
global:
  scrape_interval: 15s

scrape_configs:
- job_name: node
  static_configs:
  - targets: ['localhost:9100']
```

# Install grafana
```sh
sudo apt-get install -y apt-transport-https software-properties-common wget
```
```sh
sudo mkdir -p /etc/apt/keyrings/
```
```sh
wget -q -O - https://apt.grafana.com/gpg.key | gpg --dearmor | sudo tee /etc/apt/keyrings/grafana.gpg > /dev/null
```
```sh
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

````
```sh
echo "deb [signed-by=/etc/apt/keyrings/grafana.gpg] https://apt.grafana.com beta main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
```
# Updates the list of available packages
```sh
sudo apt-get update
```
# Installs the latest OSS release:
```sh
sudo apt-get install grafana
```
# Installs the latest Enterprise release:
```sh
sudo apt-get install grafana-enterprise
```

(or)
Grafana installation

```sh
wget https://dl.grafana.com/oss/release/grafana_8.5.10_amd64.deb
```
```sh
sudo dpkg -i grafana_8.5.10_amd64.deb
```
```sh
sudo apt-get install -f  # To resolve any dependencies
```

```sh
curl -I https://packages.grafana.com/oss/deb
```
```sh
sudo systemctl start grafana-server
```
```sh
sudo systemctl enable grafana-server
```


# Install helm3

Download scripts 


```sh
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
```

provide permission
```sh
sudo chmod 700 get_helm.sh
```
Execute script to install
```sh
sudo ./get_helm.sh
```
Verify installation
```sh
helm version --client
```

```sh
helm repo add stable https://charts.helm.sh/stable
```

```sh
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
```sh
helm search repo prometheus-community
```
Prometheus and grafana helm chart moved to kube prometheus stack
 
Create Prometheus namespace
```sh
kubectl create namespace prometheus
```
 

## Install kube-prometheus-stack
Below is helm command to install kube-prometheus-stack. The helm repo kube-stack-prometheus (formerly prometheus-operator) comes with a grafana deployment embedded.
```sh
helm install stable prometheus-community/kube-prometheus-stack -n prometheus
``` 
Lets check if prometheus and grafana pods are running already
```sh
kubectl get pods -n prometheus
``` 

```sh
kubectl get svc -n prometheus
``` 


This confirms that prometheus and grafana have been installed successfully using Helm.

In order to make prometheus and grafana available outside the cluster, use Load Balancer or NodePort instead of ClusterIP.

Edit Prometheus Service
```sh
kubectl edit svc stable-kube-prometheus-sta-prometheus -n prometheus
```

 
Edit Grafana Service
```sh
kubectl edit svc stable-grafana -n prometheus
```

 
Verify if service is changed to Load Balancer and also to get the Load Balancer URL.


```sh
kubectl get svc -n prometheus
``` 

Access Grafana UI in the browser


# How to Create Kubernetes Monitoring Dashboard?
#For creating a dashboard to monitor the cluster:

#Click '+' button on left panel and select ‘Import’.

#Enter 12740 dashboard id under Grafana.com Dashboard.

#Click ‘Load’.

#Select ‘Prometheus’ as the endpoint under prometheus data sources drop down.

#Click ‘Import’.

#This will show monitoring dashboard for all cluster nodes

# How to Create Kubernetes Cluster Monitoring Dashboard?
#For creating a dashboard to monitor the cluster:

#Click '+' button on left panel and select ‘Import’.

#Enter 3119 dashboard id under Grafana.com Dashboard.

#Click ‘Load’.

#Select ‘Prometheus’ as the endpoint under prometheus data sources drop down.

#Click ‘Import’.

#This will show monitoring dashboard for all cluster nodes

# Create POD Monitoring Dashboard
#For creating a dashboard to monitor the cluster:

#Click '+' button on left panel and select ‘Import’.

#Enter 6417 dashboard id under Grafana.com Dashboard.

#Click ‘Load’.

#Select ‘Prometheus’ as the endpoint under prometheus data sources drop down.

#Click ‘Import’.

 




 









 
