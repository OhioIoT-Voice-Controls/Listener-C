# Listener C<a href="https://www.ohioiot.com"><img src="https://www.ohioiot.com/logo_150.jpg" width="40" ></a>

##### [(back to the Voice Controls organization page)](https://github.com/OhioIoT-Voice-Controls)

This is a container implementation for your custom Vosk listener to run on a Raspberry Pi.  

You can see this repo in use in the OhioIoT YouTube video [3 Steps To Your Custom Voice Control](https://youtu.be/_ERvoHMBDac).

## Installation
Plug a USB microphone into a Raspberry Pi that has Docker and Docker Compose installed.  SSH into the Raspberry Pi and run the following commands:
```
git clone https://github.com/OhioIoT-Voice-Controls/Listener-C listener
cd listener
rm README.md
```
Edit your docker-compose file to make it point to the actual location of your container image in Docker Hub
```
nano docker-compose.yml
```
Log in to your Docker Hub account so WatchTower can pull updates from your account:
```
docker login
```
Run the system:
```
docker compose up
```
When you see the log `listening...` in the logs, it means your listener is up and listening.  At this point, speak one of the commands that you defined.  If Vosk successfully catches it, an MQTT message will go out to the broker.  Once you confirm the IP address of your Raspberry Pi, you can connect any other device to the Mosquitto broker, exposed on port 1883.  Your connected devices can subscribe to `voice/command` and hear what you are saying in the incoming message payloads.

To edit the commands or MQTT publish topic, pull the accompanying repo [Listener-C-Build](https://github.com/OhioIoT-Voice-Controls/Listener-C-Build) and follow the instructions.  The provided `docker-compose.yml` runs Watchtower to automatically update your running containers.  But in many cases, it's inconvenient waiting for that update to run.  So, you can, alternatively run the provided update script to pull and restart your listener container.  Be sure to update the script to point to your actual Docker Hub account and container image name before running:
```
cd ~/listener
./update
```
When you are comfortable that everything is in order, start running the container in the background:
```
docker compose up -d
```



## Links
- [OhioIoT YouTube Channel](https://www.youtube.com/@ohioiot) - Agenda free tutorials showing you how to get started in IoT
- [OhioIoT GitHub Index](https://github.com/OhioIoT-Examples) - The central index of code examples available on GitHub

## About
<a href="https://www.ohioiot.com"><img src="https://www.ohioiot.com/logo_150.jpg" width="40" ></a>

*OhioIoT is an IoT platform designed for small-scale IoT projects.  For more, check out our website at [www.OhioIoT.com](https://www.ohioiot.com).*

