# Server

The server part of the project is deployed on a public IP unix machine
using a traditional Telegraf-InfluxDB-Granafa stack with mosquitto
as an MQTT data broker.

## Mosquitto

Use `mosquitto_passwd` to set up username and password authentication for the MQTT server.

- **file:** [mosquitto.conf](./mosquitto.conf)
- **likely location:** `/etc/mosquitto/conf.d/default.conf`


## Telegraf

- **file:** [telegraf.conf](./telegraf.conf)
- **likely location:** `/etc/telegraf/telegraf.conf`
- **configuration:**
	- line 93: `urls = ["http://127.0.0.1:8086"]` - InfluxDB address
	- line 97: `database = "INFLUX_DATABASE_NAME"` - InfluxDB database name
	- line 131: `password = "TELEGRAF_INFLUX_PASSWORD"` - InfluxDB password
	- line 176: `servers = ["tcp://127.0.0.1:1883"]` - MQQT server address
	- line 218: `username = "MQTT_USERNAME"` - MQTT username
	- line 219: `password = "MQTT_PASSWORD"` - MQTT password


## InfluxDB

- **file:** not provided, default configuraton is fine
- **likely location:** `/etc/influxdb/influxdb.conf`

```
$ curl -XPOST "http://localhost:8086/query" \
 --data-urlencode "q=CREATE USER admin WITH PASSWORD 'ADMIN_PASSWORD' WITH ALL PRIVILEGES"

$ influx

> CREATE USER telegraf WITH PASSWORD 'TELEGARF_INFLUX_PASSWORD';

> CREATE USER grafana WITH PASSWORD 'GRAFANA_INFLUX_PASSWORD';
```


## Grafana

The Grafana configuration is possibly the most interesting part
of the project. It lives in its own subfolder [./grafana/](./grafana/).


## Routing

- **file:** [routing.conf](./routing.conf)
- **likely location:** `/etc/apache2/sites-enabled/grafana.conf`, `/etc/apache2/sites-available/grafana.conf`
- **configuration:**
	- line 2: `ServerAdmin YOUR_EMAIL_ADDRESS` - email address
	- line 3: `ServerName your.domain.org` - domain name
