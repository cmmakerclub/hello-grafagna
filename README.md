# hello-grafana


# influxdb: 
```
docker run -d --restart always -it  \
  -p 8086:8086 \
  -p 8083:8083 -e INFLUXDB_ADMIN_ENABLED=true \
  -v $PWD/influxdb:/var/lib/influxdb \
  --name influxdb \
  influxdb
```

# grafana:
```
docker run -d --restart always -it \
  -p 80:3000  \
  --name=grafana \
  -v $PWD/grafana:/var/lib/grafana \
  -e "GF_SERVER_ROOT_URL=http://grafana.cmmc.io" \
  -e "GF_SECURITY_ADMIN_PASSWORD=cmmcadmin" \
  -e "GF_INSTALL_PLUGINS=grafana-clock-panel,grafana-simple-json-datasource" \
  grafana/grafana
  ```


# telegraf-mqtt

```
docker run -d --restart always -it \
    -v $PWD/mqtt-telegraf.conf:/etc/telegraf/telegraf.conf:ro \
    --net=container:influxdb \
    --name telegraf-mqtt \
    telegraf
```
