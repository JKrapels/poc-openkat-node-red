# OpenKAT Node-RED Proof of Concept
Proof of concept setup to show and test how Boefjes and Whisker from OpenKAT can be created in Node-RED.

## About
This is an open source contribution to [OpenKAT](http://openkat.nl). Using [Node-RED](https://nodered.org/) I have built a Proof of Concept integration to allow for the low-code creation of Boefjes and Whiskers for OpenKAT. The PoC is currently (April 2024) a stand-alone Docker-based Node-RED application, but is ready to interact with OpenKAT using HTTP.

## Installation
Running the PoC is quite simple: run the docker-compose.yml in Docker, or copy its content into a [Portainer](https://www.portainer.io/) stack. Next, you import the content of "flows.json" or "flows-verbose.json" in Node-RED, which will run by default on localhost:1880. I recommend starting with "flows-verbose.json", since it shows the inner workings of the PoC.

## Using the PoC
The PoC consists of two flows: one for Boefjes, and one for Whiskers. The Info and Dashboard flows are supporting. 

## Next steps

