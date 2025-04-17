# Task7-demo
Monitor System Resources Using Netdata


Step 1: Install Docker (if not already installed)
Ubuntu/Debian:
sudo apt update
sudo apt install docker.io
Start Docker & enable on boot:
sudo systemctl start docker
sudo systemctl enable docker


Step 2: Run Netdata using Docker
docker run -d \
  --name=netdata \
  -p 19999:19999 \
  -v netdataconfig:/etc/netdata \
  -v netdatalib:/var/lib/netdata \
  -v netdatacache:/var/cache/netdata \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  -v /etc/os-release:/host/etc/os-release:ro \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  netdata/netdata
This will run Netdata on port 19999.


Step 3: Access Netdata Dashboard
Open your browser and go to:
http://localhost:19999
Or use your server IP:
http://<your-server-ip>:19999
You should see a real-time dashboard showing:
CPU usage
RAM & swap
Disk I/O
Network traffic
App-specific metrics (e.g., MySQL, NGINX if installed)


Step 4: Take a Screenshot
Once the dashboard loads:
Take a screenshot showing active metrics
Make sure key sections (CPU, memory, disk, network) are visible
This screenshot is your required deliverable.
Great! Here's how we can extend or enhance your Netdata monitoring setup:
Optional Enhancements for Your Netdata Monitoring

1. Enable Email or Slack Alerts
Netdata supports notifications when system metrics exceed defined thresholds.
Configure alarms in Netdata’s configuration (health.d/*.conf)
For Slack:
docker exec -it netdata bash
vi /etc/netdata/health_alarm_notify.conf
Set:
SEND_SLACK="YES"
SLACK_WEBHOOK_URL="https://hooks.slack.com/services/your/webhook/url"

2. Monitor Specific Apps
If you’re running services like MySQL, NGINX, or Redis, Netdata can monitor those too.
Just make sure they’re installed/running on the host machine. Netdata will auto-detect most of them.

3. Export Metrics to Prometheus or Grafana
If you're using a broader monitoring stack:
Netdata can export metrics to Prometheus
Use Grafana to build custom dashboards from Netdata data

4. Secure Your Dashboard
If you’re using Netdata in production or public cloud:
Use a reverse proxy (Nginx or Caddy) to password-protect it
Or bind Netdata to localhost and access via SSH tunnel

5. Collect Historical Metrics
Free Netdata provides only live monitoring. For historical data:
Use Netdata Cloud (free tier available)
Or set up metrics exporting (e.g., to InfluxDB, Prometheus)

 Here are a few enhancement paths you can choose from. Pick one (or more), and I’ll guide you through setup:
1. Set up Slack notifications for alerts
Get notified if CPU, RAM, or disk usage spikes.

2. Enable monitoring for specific services (MySQL, NGINX, etc.)
Useful if you want to track app-specific metrics.

3. Secure your Netdata dashboard
Use NGINX + password, or SSH tunnel for safe remote access.

4. Send metrics to Grafana via Prometheus
For beautiful custom dashboards and historical data tracking.

5. Connect to Netdata Cloud
Easy way to see multiple systems and access historical data.
