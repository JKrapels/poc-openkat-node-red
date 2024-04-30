# OpenKAT Node-RED Proof of Concept
Proof of concept setup to show and test how Boefjes and Whisker from OpenKAT can be created in Node-RED.

## About
This is an open source contribution to [OpenKAT](http://openkat.nl). Using [Node-RED](https://nodered.org/) I have built a Proof of Concept integration to allow for the low-code creation of Boefjes and Whiskers for OpenKAT. The PoC is currently (April 2024) a stand-alone Docker-based Node-RED application, but is ready to interact with OpenKAT using HTTP.

## Installation
Running the PoC is quite simple: run the docker-compose.yml in Docker, or copy its content into a [Portainer](https://www.portainer.io/) stack. Next, you import the content of "flows.json" or "flows-verbose.json" in Node-RED, which will run by default on localhost:1880. I recommend starting with "flows-verbose.json", since it shows the inner workings of the PoC.

## How it works
The PoC consists of two main flows: one for Boefjes, and one for Whiskers. The Info and Dashboard flows are supporting.

### Boefjes flow
The Boefjes flow contains two groups for the OpenKAT input and output, "BoefjeTasks IN from OpenKAT" and "Raw data OUT to Bytes" respectively. BoefjeTasks are currently received on port 1995 as HTTP, and output to Bytes is send using an HTTP POST to port 1997. More details on the flows and creating your own Boefjes can be found in the Flow documentation. (double click on the flow in Node-RED)

BoefjeTasks are currently HTTP posts with the following formatting as the body of the request:
'''JavaScript
{
  Boefje: "001hibpwnd",
  input_ooid: {
    SHA1_hash: "8be3c943b1609fffbfc51aad666d0a04adf83c9d"
    }
}
'''

### Whisker flow
The Whiskers flow contains two groups for the OpenKAT input and output, "NormalizerTasks IN from OpenKAT" and "objectData data OUT to Octopoes" respectively. NormalizerTasks are currently received on port 1997 as HTTP, and output to Octopoes is send using an HTTP POST to port 1998. More details on the flows and creating your own Whiskers can be found in the Flow documentation. (double click on the flow in Node-RED)


## Next steps
The obvious next step would be to connect the Node-RED container to OpenKAT. For this, two challenges have to be overcome:
1. Update the Node-RED flows to correctly accept and BoefjeTasks and NormalizerTasks, and ouput the right data to Bytes and Octopoes.
2. Create a Node-RED Boefje and Node-RED Whisker in the OpenKAT KAT-alogus, where configuration for the Node-RED modules can be done.
