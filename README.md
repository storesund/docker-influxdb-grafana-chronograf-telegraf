# docker-influxdb-grafana-chronograf-telegraf
Docker compose setup for a InfluxDB-Grafana-Chronograf-Telegraf stack that actually works.

The telegraf service will log to the influxdb every 10 seconds. The attached telegraf configuration is from: https://github.com/nicolargo/docker-influxdb-grafana. All data is by default written to a database in influxdb called `telegraf`.

# Getting started
## Get it all up and running
```bash
git clone git@github.com:storesund/docker-influxdb-grafana-chronograf-telegraf.git
cd docker-influxdb-grafana-chronograf-telegraf
docker-compose up -d
```

### Verify that it is running
```bash
docker ps
```

## See it all working
### System telemetry from `telegraf` in `chronograf`
1. Go to http://localhost:8888 to see the welcome guide for chronograf.
1. For the influxdb connection, replace `localhost` in the URL with `influxdb` (the docker bridge network). No need for username/password. The database default should be `telegraf` since it is the only one with data.
1. In the next step, choose the `system` dashboard, as suggested by chronograf.
1. Find the `system` dashboard in the main system, and see all the telemetry from telegraf right away.

### System telemetry from `telegraf` in `grafana`
1. Go to http://localhost:3000 to see the welcome guide for grafana.
1. Log in using username/password "admin"/"admin". Choose a new password on the next screen.
1. Click "Add Datasource" and "InfluxDB".
1. Enter `http://influxdb:8086` for HTTP URL.
1. Enter `telegraf` for "Database". Click "Save and Test".
1. Go to "Explore" and run some test-queries against the `autogen` dataseries.

## Stop and remove everything
```bash
docker-compose stop
docker-compose rm
```
