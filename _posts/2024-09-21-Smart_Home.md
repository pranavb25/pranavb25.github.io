---
title: My smart home stack
description: Home automation, ad blocking, media streaming and much more.
categories: [Tech, Smart Home]
tags: [home assistant, iot, automation, raspberrypi]     # TAG names should always be lowercase
---


I've been intermittently building smart devices and tinkering with the IoT ecosystem since ~ 2015. Over the past year, I've added a lot of services to what is now my smart home stack.

To start off with, here's a summary:

**Services**:
1. **Home Assistant** - for everything smart home
2. **AdGuard** - network wide ad and tracker blocking
3. **Portainer** - docker container management
4. **Watchtower** - automated updates
5. **Dashdot** - CPU, storage, network stats
6. **Homarr** - highly configurable dashboard
7. **Media / Arr stack**
	1. **Radarr** - manage movies
	2. **Sonarr** - manage shows
	3. **Bazarr** - manage subtitles
	4. **Prowlarr** - manage indexers
	5. **Transmission** - torrents
	6. **Jellyfin** - consume media
	7. **Jellyseer** - discover media
8. **Random**
	1. **Stirling PDF** - powerful pdf operations
	2. **Mealie** - recipe management 

Most, if not all of the above are managed via docker containers.

**Hardware**:
1. **Raspberry Pi** 4, 8GB - runs everything, managed headless
2. **256GB SSD** - should've gone with a much higher capacity. Planning expansion now
3. **Sonoff Zigbee dongle** - enable Zigbee. [Link](https://robu.in/product/sonoff-zigbee-3-0-usb-dongle-plus-zbdongle-e/)
4. **Philips Hue** smart bulb - uses Zigbee
5. **Wipro Smart bulb** - uses WiFi
6. **ESP32** - enables creation and addition of random smart devices

Now into the specifics:

## Home Assistant

![Home Assistant dashbaord](/assets/img/posts/HA.png)
*My current HA dashboard (majorly WIP) which basically contains toggles for bulbs and sensor readings. The same is available on both iOS and Android as well*

My main reasons for hopping on the HA bandwagon were:

1. Aversion to using multiple vendor apps for controlling devices + prevention of vendor lock-in
	1. With my HA app, I can control a Philips bulb, a Wipro bulb, a Sonoff sensor and more from the same place.
2. Desire to contain device and sensor data flow within local network
	1. None of my smart devices need any external connectivity
3. Open source and limitlessly tweakable

That being said, I feel I've barely scratched the surface of what all HA has to offer. Up until now, I've mainly used it to control smart lights and monitor temp and humidity sensors.

Both of these, I've enabled via Zigbee and WiFi integrations. 

## Zigbee - for smart lights and sensors

* Enabled via MQTT, Zigbee2MQTT + Sonoff Zigbee router stick that goes into the Pi
* A Philips Hue bulb acts as a router as well and helps establish connection with the Sonoff temp and humidity sensor

![Zigbee devices](/assets/img/posts/Zigbee.png)
*The above snippet from the Zigbee2MQTT panel shows how the Philips node connects to the main router while also acting as a router and helping establish a connection with the sensor.*

## WiFi and LocalTuya - for smart lights

* The other smart light I have is from Wipro and the hack used to get that onto HA was to use the LocalTuya integration.

## ESPHome

* I've also configured an ESP32 together with ESPHome to add a few sensors e.g. Sound. Haven't used this much till now.

## Media Server

*Disclaimer: Purely for educational purposes*

This was more of a weekend build and I also felt guilty about leaving too much unused RAM on the pi, so felt like an opportune time.

Here's how the stack looks like:

![Media stack](/assets/img/posts/MediaStack.png)

The above image and installation steps, including docker compose files etc are given [here](https://zerodya.net/self-host-jellyfin-media-streaming-stack/). One change I made was to use Prowlarr instead of Jackett because the automatic addition of indexes felt a lot quicker.

Things I like:
* For series, new episodes can be monitored automatically and be made available when ready.
* Artwork, metadata, ratings, cast etc are all displayed with a good enough UI.
* Jellyfin has client apps for mobile and TV both. It's pretty basic but works just fine.

Main challenge here is that most indexers are private. Yet to find the best work around here. I did try exploring Usenet but honestly haven't had the time to integrate and explore it yet.

Here's how the stack appears on my main dashboard (built on Homarr):

![Media stack apps](/assets/img/posts/Media.png)
*Homarr automatically displays the container health via the green dot at the bottom. This comes in handy for quick troubleshooting*


![Media download stats](/assets/img/posts/Downloads.png)
*The Homarr <> Prowlaar and Transmission are quite helpful and display indexer health, download stats etc.*

## Monitoring

![Homarr stats](/assets/img/posts/Stats.png)
*Section of my Homarr setup displaying stats from Dashdot and AdGuard*


* ***Portainer** helps get visibility into container health. Occasionally I need to restart some unstable ones.

![Portainer](/assets/img/posts/Portainer.png)

* ***Watchtower** helps auto update docker containers. Since I'm not running mission critical stuff, I'm not afraid of things breaking. I do however plan to optimize the watchtower config so that odds of unexpected breakages reduce. 

* ***Dashdot** helps monitor CPU,  storage and network stats

* ***Homarr** allows me to view the entire stack along with some neat charts etc. 
	* Also has a section for container management which is quick and handy.
	* Also has neat widgets and integrations for common services like Transmission, Dashdot, Jellyseer etc.

That's a wrap on the current state! 

## Future plans

1. **More lights and switches** added to the HA network.
2. **Local [voice](https://www.home-assistant.io/voice_control/) control**. This is far from being a seamless Alexa / Siri replacement but still progressing at a decent pace.
3. **[PiVPN](https://www.pivpn.io/) integration**: This will allow me to connect to my system from anywhere. I will also be able to tap into my home's AdGuard config remotely.
4. **Custom ESP32 builds**: I've been wanting to integrate sound and light sensors into the system. Clubbed with temp, humidity and data from my Ultrahuman ring, I want to see what data patterns emerge.
	1. UH also seems to be exposing an API to interested people. Planning to hit them up to see if I can make the data flow into my system.