---
layout: post
title:  "MQTT with wemos & win10"
date:   2019-10-14 16:00:00 +0800
categories: note
tags: [MQTT, Arduino]
---
## [About MQTT](https://en.wikipedia.org/wiki/MQTT)  
## [Get started with Wemos D1 R2](https://gist.github.com/carljdp/e6a3f5a11edea63c2c14312b534f4e53)
## [Mosquitto (MQTT broker)](https://mosquitto.org/)
Make sure the service named **Mosquitto Broker** is running on your computer.  
> mosquitto_sub -h "localhost" (-p "9487" -u "username" -P "pwd") -t "topic/#" (-d)  
> mosquitto_pub -h "localhost" (-p "9487" -u "username" -P "pwd") -m "Publishing Message" -t "topic/"  

## [PubSubClient (arduino library)](https://pubsubclient.knolleary.net/)
[example for esp8266](https://github.com/knolleary/pubsubclient/blob/master/examples/mqtt_esp8266/mqtt_esp8266.ino)
