# Listener C<a href="https://www.ohioiot.com"><img src="https://www.ohioiot.com/logo_150.jpg" width="40" ></a>

##### [(back to the Voice Controls organization page)](https://github.com/OhioIoT-Voice-Controls)

This is a container implementation for your custom Vosk listener to run on a Raspberry Pi.

NOTE: Before you proceed here, you should have already taken the build steps in [Listener C Build](https://github.com/OhioIoT-Voice-Controls/Listener-C-Build).

You can see this repo in use in the OhioIoT YouTube video [3 Steps To Your Custom Voice Control](https://youtu.be/_ERvoHMBDac).

## Installation
Plug a USB microphone into a Raspberry Pi that has Docker and Docker Compose installed.  SSH into the Raspberry Pi to continue.

You can run all of these steps at once, but note that you will need to intervene twice - once for `docker login` and once to edit your `docker-compose.yml` to make sure it is pointing to your container image:
```
docker login
git clone https://github.com/OhioIoT-Voice-Controls/Listener-C listener
cd listener
rm README.md
nano docker-compose.yml
nano update
chmod +x update
docker compose up
```
When you see `listening...` in the logs, it means your listener is up and ready.  At this point, speak one of the commands that you defined.  If Vosk successfully catches it, an MQTT message will go out to the broker.  Once you confirm the IP address of your Raspberry Pi, you can connect any other device to the Mosquitto broker, exposed on port 1883.  Your connected devices can subscribe to `voice/command` and hear what you are saying in the incoming message payloads.

When you are comfortable that everything is in order, start running the container in the background:
```
[CTRL]-c
docker compose up -d
```

To edit the commands or MQTT publish topic, go back to [Listener-C-Build](https://github.com/OhioIoT-Voice-Controls/Listener-C-Build) and follow the instructions.  When you have an updated container image, come back to your Raspberry Pi and run:
```
cd ~/listener
./update
```
That's the fastest way to get your updates in.  If you don't require speed, but you do want automation, if Watchtower isn't already running on your Raspberry Pi, uncomment the Watchtower code that you see in the `docker-compose.yml`.  This will check for updates every 10 minutes and pull them down and run them when there are any.

To tear this down when you are done:
```
cd ~/listener_c
docker compose down
cd ..
rm -rf listener_c
```


## Links
- [OhioIoT YouTube Channel](https://www.youtube.com/@ohioiot) - Agenda free tutorials showing you how to get started in IoT
- [OhioIoT GitHub Index](https://github.com/OhioIoT-Examples) - The central index of code examples available on GitHub

## About
<a href="https://www.ohioiot.com"><img src="https://www.ohioiot.com/logo_150.jpg" width="40" ></a>

*OhioIoT is an IoT platform designed for small-scale IoT projects.  For more, check out our website at [www.OhioIoT.com](https://www.ohioiot.com).*

