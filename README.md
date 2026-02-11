 # Dummy Systemd Service – Linux Background Service Project
 
  ## Overview

This project demonstrates how to create, configure, and manage a custom systemd service in Linux. The service runs a simple Bash script in the background that logs a message every 10 seconds, simulating a long-running application.

The main goal of this project is to gain hands-on experience with:

* Creating systemd services

* Managing background processes

* Enabling services at boot

* Monitoring logs using journalctl

* Debugging and restarting failed services

* This project was implemented and tested on an AWS EC2 Linux instance, accessed via SSH from a local machine.

## Technologies Used

1. Linux (systemd-based distribution)

2. Bash Scripting

3. systemd

4. AWS EC2

5. SSH

6. Git & GitHub
## Bash Script (dummy.sh)

This script runs continuously and writes a log message every 10 seconds.

```
#!/bin/bash

while true
do
    echo "Dummy service is running...." >> /var/log/dummy-service.log
    sleep 10
done
```

## Systemd Service File (dummy-service.service)

This file defines how the service is managed by systemd.

Location:

```
/etc/systemd/system/dummy-service.service

```
### Service File
~~~
[Unit]
Description=Dummy Background Service for testing
After=network.target

[Service]
ExecStart=/usr/local/bin/dummy.sh
Restart=always
RestartSec=5
User=root

[Install]
WantedBy=multi-user.target
~~~

## Installation & Setup
1️⃣ Make Script Executable
~~~
sudo chmod +x /usr/local/bin/dummy.sh
~~~

2️⃣ Reload systemd
~~~
sudo systemctl daemon-reload
~~~
3️⃣ Enable Service on Boot
~~~
sudo systemctl enable dummy-service
~~~
4️⃣ Start the Service
~~~
sudo systemctl start dummy-service
~~~
▶️ Service Management Commands
~~~
Start Service
sudo systemctl start dummy-service
~~~

Stop Service
~~~
sudo systemctl stop dummy-service
~~~
Enable on Boot
~~~
sudo systemctl enable dummy-service
~~~
Disable on Boot
~~~
sudo systemctl disable dummy-service
~~~
Check Status
~~~
sudo systemctl status dummy-service
~~~
📊 Log Monitoring
View Logs in Real-Time
~~~
sudo journalctl -u dummy-service -f
~~~
View Log File
~~~
cat /var/log/dummy-service.log
~~~
☁️ Deployment Environment

Platform: Amazon Web Services (AWS EC2)

OS: Linux (systemd enabled)

Access Method: SSH

Development Machine: Local Laptop

This setup simulates a real-world cloud server environment.

## 📷 Screenshots
### Service status output
<img width="1917" height="274" alt="Screenshot 2026-02-11 231001" src="https://github.com/user-attachments/assets/60c7ca45-790f-4146-9429-e066c5628ba6" />

### Log file content

<img width="1382" height="21" alt="Screenshot 2026-02-11 231355" src="https://github.com/user-attachments/assets/47b4db61-9205-449d-8f6e-82521066b715" />

### Journalctl output

<img width="1915" height="938" alt="Screenshot 2026-02-11 231627" src="https://github.com/user-attachments/assets/1a51c0af-117b-4ec8-b957-3e6c59a1bf6c" />

