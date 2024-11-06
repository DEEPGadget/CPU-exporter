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
sudo vi CPU-exporter.service
#copy and change path and User!! very important don't forget!!!
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

4. set RaspberryPi Prometheus yaml file
```
cd /etc/prometheus
sudo vi prometheus.yaml
#copy and change IP
  - job_name: CPU-exporter
    # If prometheus-node-exporter is installed, grab stats about the local
    # machine by default.
    static_configs:
      - targets: ['192.168.1.74:8889']

```

5. Check your query
sample result
```
# HELP python_gc_objects_collected_total Objects collected during gc
# TYPE python_gc_objects_collected_total counter
python_gc_objects_collected_total{generation="0"} 344.0
python_gc_objects_collected_total{generation="1"} 33.0
python_gc_objects_collected_total{generation="2"} 0.0
# HELP python_gc_objects_uncollectable_total Uncollectable objects found during GC
# TYPE python_gc_objects_uncollectable_total counter
python_gc_objects_uncollectable_total{generation="0"} 0.0
python_gc_objects_uncollectable_total{generation="1"} 0.0
python_gc_objects_uncollectable_total{generation="2"} 0.0
# HELP python_gc_collections_total Number of times this generation was collected
# TYPE python_gc_collections_total counter
python_gc_collections_total{generation="0"} 42.0
python_gc_collections_total{generation="1"} 3.0
python_gc_collections_total{generation="2"} 0.0
# HELP python_info Python platform information
# TYPE python_info gauge
python_info{implementation="CPython",major="3",minor="8",patchlevel="10",version="3.8.10"} 1.0
# HELP process_virtual_memory_bytes Virtual memory size in bytes.
# TYPE process_virtual_memory_bytes gauge
process_virtual_memory_bytes 1.83525376e+08
# HELP process_resident_memory_bytes Resident memory size in bytes.
# TYPE process_resident_memory_bytes gauge
process_resident_memory_bytes 2.1467136e+07
# HELP process_start_time_seconds Start time of the process since unix epoch in seconds.
# TYPE process_start_time_seconds gauge
process_start_time_seconds 1.73087908118e+09
# HELP process_cpu_seconds_total Total user and system CPU time spent in seconds.
# TYPE process_cpu_seconds_total counter
process_cpu_seconds_total 0.14
# HELP process_open_fds Number of open file descriptors.
# TYPE process_open_fds gauge
process_open_fds 7.0
# HELP process_max_fds Maximum number of open file descriptors.
# TYPE process_max_fds gauge
process_max_fds 1024.0
# HELP cpu_user_usage_percent CPU usage by user mode
# TYPE cpu_user_usage_percent gauge
cpu_user_usage_percent 0.0
# HELP cpu_system_usage_percent CPU usage by system mode
# TYPE cpu_system_usage_percent gauge
cpu_system_usage_percent 0.0
# HELP cpu_nice_usage_percent CPU usage by nice processes
# TYPE cpu_nice_usage_percent gauge
cpu_nice_usage_percent 0.0
# HELP cpu_idle_usage_percent CPU idle time
# TYPE cpu_idle_usage_percent gauge
cpu_idle_usage_percent 0.0
# HELP cpu_total_usage_percent Total CPU usage
# TYPE cpu_total_usage_percent gauge
cpu_total_usage_percent 0.0
# HELP cpu_tctl_temperature_celsius CPU Tctl Temperature in Celsius
# TYPE cpu_tctl_temperature_celsius gauge
cpu_tctl_temperature_celsius 54.2

```
