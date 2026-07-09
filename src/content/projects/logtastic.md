---
title: "Logtastic"
description: "Meshtastic Logging and API"
pubDate: 2026-07-09 12:00:00
---

I have been experimenting with LoRa radios, which are low powered devices that transmit data over sub-gigahertz radio frequency bands. LoRa tech is used by governments and industry to monitor machines and sensors over a long range. LoRa radios are usually packaged alongside a microcontroller, such as the ESP32. I'm using my LoRa device to join my city's Meshtastic network, which can act as an emergency communication network across neighborhoods. A local mesh network is useful during utility outages and weather emergencies.

Logtastic is a small scale project to use a Raspberry Pi to capture and log Meshtastic network traffic. All node traffic is logged to a local SQLite database. A small web server and API is served from the Pi to give the node owner visibility to network events.