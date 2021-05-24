# Pi

This folder describes the setup and the configuration of the Raspberry Pi
which reguraly queries the printer for statistics over SNMP and publishes 
the metrics over MQTT protocol.

## Setup

It is conveninet to use printer-specific defition installed via
[MIB](https://en.wikipedia.org/wiki/Management_information_base)
for the SNMP queries.

In our specific setup, we use HP printer and therefore corresponding defitions

[http://www.circitor.fr/Mibs/Mib/H/HP-LASERJET-COMMON-MIB.mib
](http://www.circitor.fr/Mibs/Mib/H/HP-LASERJET-COMMON-MIB.mib)


## Telegraf

- **file:** [telegraf.conf](./telegraf.conf)
- **likely location:** `/etc/telegraf/telegraf.conf`
- **configuration:**
	- line 86: `servers = ["filip.hlasek.org:1883"]` - MQTT server address
	- line 100: `username = "MQTT_USERNAME"` - MQTT server username
	- line 101: `password = "MQTT_PASSWORD"` - MQTT server password
	- line 138: `agents = ["10.0.0.50"]` - printer address
	- line 145 onwards: printer-specific SNMP queries
