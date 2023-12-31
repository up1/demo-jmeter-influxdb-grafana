# Workshop Performance Testing with Apache JMeter (Distributed testing)
* Apache JMeter
* InfluxDB 2
* Grafana
* Docker compose

## Step to run

1. Build image
```
$docker compose build
```

2. Start Influxdb (Database to store test result from Apache JMeter)
```
$docker compose up -d influxdb
$docker compose ps
$docker compose logs --follow
```

3. Start Grafana (Dashboard of test result)
```
$docker compose up -d grafana
$docker compose ps
$docker compose logs --follow
```

Access to Grafana eith url = http://localhost:3000
* user=admin
* password=admin

4. Run test plan with Apache JMeter
* [Influx DB v2.0 listener plugin for Apache JMeter](https://github.com/mderevyankoaqa/jmeter-influxdb2-listener-plugin)
* Config backend listener with InfluxDB 2
```
$jmeter -n -t google.jmx -l ./log.jtl -j ./result.log

or 

$docker compose up jmeter --remove-orphans
```


![alt text](https://github.com/up1/demo-jmeter-influxdb-grafana/blob/main/jmeter-backend.png?raw=true)
