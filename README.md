# multiples-sensor-mqtt-mongo

# 🚀 A sample application built that shows how MQTT could be used to manage a multiples sensor sent data to a server, which will record it into da mongo and influxdb data base 🚀

https://github.com/coding-to-music/multiples-sensor-mqtt-mongo

From / By https://github.com/agneisilva

https://github.com/agneisilva/Multiples-sensor-mqtt-mongo

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/multiples-sensor-mqtt-mongo.git
git push -u origin main
```

# MQTT Multiples sensor Example Application

A sample application built that shows how MQTT could be used to manage a multiples sensor sent data
to a server, which will record it into da mongo and influxdb data base

##RUN

for localhost porpose use command line for start mqtt container and mongodb

docker run --name mongodb -p 27017:27017 -d mongo

docker run -it -d -p 1883:1883 -p 9001:9001 eclipse-mosquitto

docker run -d -p 8086:8086 influxdb:latest

docker ps -a

MAKE SURE both mongodb, influxdb and mosquitto service broker container are running before run server and sensor

```
docker-compose up
```

Output

```
Creating network "multiples-sensor-mqtt-mongo_bridge-network" with driver "bridge"
Creating influxdb  ... done
Creating mongo     ... done
Creating mosquitto ... done
Creating sensors   ... done
Creating server    ... done
Attaching to influxdb, mosquitto, mongo, server, sensors
```

```
docker ps
```

Output

```
CONTAINER ID   IMAGE                      COMMAND                  CREATED         STATUS         PORTS                                           NAMES
8d9d3560c52a   server                     "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes                                                   server
cd80a16a81dd   sensors                    "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes                                                   sensors
203c661d7a38   mongo:latest               "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   0.0.0.0:27017->27017/tcp, :::27017->27017/tcp   mongo
828bad6bedf8   eclipse-mosquitto:latest   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:1883->1883/tcp, :::1883->1883/tcp       mosquitto
7642b5dde135   influxdb:latest            "/entrypoint.sh infl…"   2 minutes ago   Up 2 minutes   0.0.0.0:8086->8086/tcp, :::8086->8086/tcp       influxdb
```

![Docker PS](doc/docker_ps.png)

## Starting SERVER

access server folder and run:

```
cd server

npm install
```

```
node server.js
or
npm run start
```

![Server saving data](doc/server_saved_data.png)

## Starting Sensor

access sensor folder and run:

```
cd ../sensor

npm install

npm run start

# or
node simulateMultiplesSensor.js 5
```

![Started 5 sensor async](doc/started_5_sensor.png)

where "5" is the number of sensor you want to simulate. You can use any positive number you want.
the more, more it will be sensors initialized in your memory.

You can use CymaticLabs.InfluxDB.Studio project to select data in influxdb
[InfluxDB Studio](https://github.com/CymaticLabs/InfluxDBStudio)
![InfluxDb Studio](doc/InfluxDBStudio.png)

and

Use Mongo Compass Comunity to select data in MongoDb
[InfluxDB Studio](https://www.mongodb.com/products/compass)
![Mongo Compass](doc/mongoCompass.png)

Docker Commands:

cd .\server
docker build . -t server

cd .\sensor
docker build . -t sensors

docker-compose -f docker-compose.yml --no-ansi build --no-cache
docker-compose -f docker-compose.yml up -d --no-build --force-recreate --remove-orphans
docker-compose -f docker-compose.yml down

netstat -a -b -n -o > ports_running.txt

docker exec -it 333c8bb35283 bash
docker exec -it 333c8bb35283 /bin/bash
docker exec -it 333c8bb35283 /bin/sh

docker logs --tail 50 --follow --timestamps 333c8bb35283

docker-compose -f docker-compose.yml logs -f server sensors
