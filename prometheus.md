 wget https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz
 tar xvfz prometheus-2.52.0.linux-amd64.tar.gz
  mv prometheus-2.52.0.linux-amd64 /etc/prometheus
 nano /etc/systemd/system/prometheus.service
 
 [Unit]
Description=Prometheus
Wants=network-online.target
After=network-online.target
[Service]
ExecStart=/etc/prometheus/prometheus --config.file=/etc/prometheus/prometheus.yml
Restart=always
[Install]
WantedBy=multi-user.target 
systemctl daemon-reload
systemctl enable prometheus
systemctl restart  prometheus



wget https://github.com/prometheus/node_exporter/releases/download/v1.8.0/node_exporter-1.8.0.linux-amd64.tar.gz
tar xvfz node_exporter-1.8.0.linux-amd64.tar.gz
 mv node_exporter-1.8.0.linux-amd64  /etc/node_exporter
 nano /etc/systemd/system/node_exporter.service
systemctl restart node_exporter
systemctl status node_exporter


Node exporter systemd file
============================
[Unit]
Description=Node Exporter
Wants=network-online.target
After=network-online.target
[Service]
ExecStart=/etc/node_exporter/node_exporter
Restart=always
[Install]
WantedBy=multi-user.target


Prometheus scrape file
==========================
global:
  scrape_interval: 15s

scrape_configs:
- job_name: node
  static_configs:
  - targets: ['localhost:9100']

 









 
