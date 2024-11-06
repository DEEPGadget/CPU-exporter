# **Prerequisite setup**
```
pip install psutil
pip install prometheus_client
```

# **How to Use**
1. install
```
git clone https://github.com/DEEPGadget/CPU-exporter.git
```

2. You need to register the service in /etc/systemd/system 

```
cd /etc/systemc/system 
sudo vi CPU-exporter.service (copy and change path and User!! very important don't forget!!!)

Description=CPU Temperature Exporter
After=network.target

[Service]
ExecStart=/usr/bin/python3 /path/CPU-exporter.py
WorkingDirectory=/path/sg-tt04
StandardOutput=inherit
StandardError=inherit
Restart=always
User=Your Server User

[Install]
WantedBy=multi-user.target

3. Configure the service to start on boot
```
sudo systemctl daemon-reload
sudo systemctl enable CPU-exporter.service
sudo systemctl status CPU-exporter.service
```

4. set RaspberryPi Prometheus yaml file and change IP
```
cd /etc/prometheus
sudo vi prometheus.yaml  (copy)

  - job_name: CPU-exporter
    static_configs:
      - targets: ['192.168.1.74:8889']

```

5. Check your query
```
curl http://yourIP:8889/metrics
```
