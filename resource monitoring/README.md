# Prometheus / Grafana Dashboard

## build as dockerized addition to monitor perfomance of (distributed) [CAPEv2 sandbox ](https://github.com/kevoreilly/CAPEv2) 

After you've created the prometheus.yml file and have deployed the docker-compose, the rest of the steps are as follows:

- Select DataSource on home page. Select Prometheus.
- add in http://prometheus:9090 for single host, or https://hostip:9091 for distributed
- Search for: "node exporter grafana dashboards" on Google
- Look for results on grafana.com
- Find ID of the dashboard you like
(This is the dashboard I like: https://grafana.com/grafana/dashboards/11074)
- Import ID in Grafana

If Grafana is used as a subpath of CAPEv2 e.g. https://mysandbox.com/monitoring
you should add an extra locations block in nginx like so:
``` 
location /monitoring {
        proxy_pass http://127.0.0.1:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
```
note: also dont forget to uncomment the needed environment variables for Grafana in the docker-compose.yml
