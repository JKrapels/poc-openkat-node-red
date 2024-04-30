# OpenKAT Node-RED Proof of Concept
Proof of concept setup to show and test how Boefjes and Whisker from OpenKAT can be created in Node-RED.

## About
This is an open source contribution to [OpenKAT](http://openkat.nl). Using [Node-RED](https://nodered.org/) I have built a Proof of Concept integration to allow for the low-code creation of Boefjes and Whiskers for OpenKAT. The PoC is currently (April 2024) a stand-alone Docker-based Node-RED application, but is ready to interact with OpenKAT using HTTP.

## Installation
Running the PoC is quite simple: run the docker-compose.yml in Docker, or copy its content into a [Portainer](https://www.portainer.io/) stack. Next, you import the content of "flows.json" or "flows-verbose.json" in Node-RED, which will run by default on localhost:1880. I recommend starting with "flows-verbose.json", since it shows the inner workings of the PoC.

## How it works
The PoC consists of two main flows: one for Boefjes, and one for Whiskers. The Info and Dashboard flows are supporting. Flows-verbose.json contains an interactive dashboard, which you can access at localhost:1880/ui. You can use this dashboard to explore the example Boefje and Whisker and check the raw HTTP requests.

### Boefjes flow
The Boefjes flow contains two groups for the OpenKAT input and output, "BoefjeTasks IN from OpenKAT" and "Raw data OUT to Bytes" respectively. Every Boefje has its own group, with a Link in and Link out. BoefjeTasks are currently received on port 1995 as HTTP, and output to Bytes is send using an HTTP POST to port 1997. More details on the flows and creating your own Boefjes can be found in the Flow documentation. (double click on the flow in Node-RED)

BoefjeTasks are currently HTTP posts with the following JSON object as the body of the request:
```JavaScript
{
  Boefje: BOEFJE_ID,
  input_ooid: {
    OBJECT_TYPE: VALUE
    }
}
```

Ouput to Bytes are currently HTTP posts with the following JSON object as the body of the request:
```JavaScript
{
  produced: RAW_DATA,
  boefje: BOEFJE_ID,
  arguments: JSON_OBJECT
}
```

### Whisker flow
The Whiskers flow contains two groups for the OpenKAT input and output, "NormalizerTasks IN from OpenKAT" and "objectData data OUT to Octopoes" respectively. Every Whisker has its own group, with a Link in and Link out. NormalizerTasks are currently received on port 1997 as HTTP, and output to Octopoes is send using an HTTP POST to port 1998. More details on the flows and creating your own Whiskers can be found in the Flow documentation. (double click on the flow in Node-RED)

NormalizerTasks are currently HTTP posts with the following JSON object as the body of the request:
```JavaScript
{
  produced: RAW_DATA,
  boefje: BOEFJE_ID,
  arguments: JSON_OBJECT
}
```
Note: In the PoC, this is the same message and format as the output to Bytes. This is due to the fact that Whiskers use raw data from Bytes, and the PoC does not contain an instance of Bytes.

Output to Octopoes are currently HTTP posts with the following JSON object as the body of the request:
```JavaScript
{
  Finding: JSON_OBJECT,
  normalizer: NORMALIZER_ID,
  arguments: JSON_OBJECT
}
```

## Next steps
The obvious next step would be to connect the Node-RED container to OpenKAT. For this, two challenges have to be overcome:
1. Update the Node-RED flows to correctly accept and BoefjeTasks and NormalizerTasks, and ouput the right data to Bytes and Octopoes.
2. Create a Node-RED Boefje and Node-RED Whisker in the OpenKAT KAT-alogus, where configuration for the Node-RED modules can be done.
