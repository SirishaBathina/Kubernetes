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





 
