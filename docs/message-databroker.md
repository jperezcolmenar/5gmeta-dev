# Message Data Broker
## Description
Message Data Broker is the module used in 5GMETA Cloud platform to stream the messages from Sensors&Devices to the 5G MECs (Multi-access edge computing).

### Installation
Installation requirements can be found in the repository.

- Clone the repository using ```git clone https://github.com/5gmetadmin/message-data-broker.git```

## Table of Contents
This repository contains the following modules: 

- An ActiveMQ ***Message Broker*** ([link](https://github.com/5gmetadmin/message-data-broker/tree/main/src)) - which is deployed in the MEC 
- **Examples** of sender and receiver in python

Note: Detailed instructions to build the ActiveMQ source code are available [here](https://github.com/5gmetadmin/message-data-broker/tree/main/src#readme).

## Development instructions for Message Data Broker

Message Broker can be found in the ***/src*** folder

Steps to run: 

* sudo docker-compose up -d
* open http://<ip>:8161
    * manage ActiveMQ broker
    * admin/admin
    * you can see created topics


## Required packages
- pip dependencies
- python-qpid-proton 


## Examples

In the ***/examples/activemq_clients*** you will find sample code for different types of AMQP producers as follows:

- ***cits_sender_python***: a python sender and receiver that run an AMQP sender simulating a number of vehicles that send messages with some properties attached.

- ***image_sender_python***: a python sender and receiver that run an AMQP sender simulating a number of vehicle that sends images (different size, but all the same)

- ***cits_receiver_python***: a python example to receive messages from AMQP events

These producer/consumer examples are described in detail in the following section. 



