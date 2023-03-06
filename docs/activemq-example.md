# Produce and Consumer Examples
## Description
As discussed in the previous section,  [***/activemq_clients***](https://github.com/5gmetadmin/message-data-broker/tree/main/examples/activemq_clients) provides examples how to produce (cits/image) data from a Sensor&Device to the MEC using python AMQP [Qpid Proton](https://qpid.apache.org/proton/index.html) reactor API with ActiveMQ. 

In this section, we will discuss the examples in further detail.

## Required packages
- Linux distribution
- Python version 3.5+
- You have successfully installed [python-qpid-proton](https://pypi.python.org/pypi/python-qpid-proton) - including any of its [dependencies](https://github.com/apache/qpid-proton/blob/master/INSTALL.md)


Refering the examples presented, following are some essential parameters while producing data on the 5GMETA platform:

- ***source_id***: a Unique Identifier to distinguish the source of generated data.
- ***tile***: Tile of the source from where the data is being generated in form of QuadKey code. e.g. 1230123012301230 (must be 18 chars in [0-3])
- ***datatype***: should be one of the allowed datatype [cits, video, image]
- ***sub_datatype***: depends upon on the datatype e.g. cam, denm, mappem



## Generic producer structure

A typical producer will contain the following fields, as it can be seen in the [examples](https://github.com/5gmetadmin/message-data-broker/blob/main/examples/activemq_clients):

- ***Discovery Registration API*** : This API helps you connect your S&Ds and push data to the MEC within a specified tile.


- Getting tile of the source from its current GPS position: 

```tileTmp = Tile.for_latitude_longitude(latitude=latitude, longitude=longitude, zoom=18) ```

    
- Getting the **message-broker access** from the **MEC** within the **previous tile**:
```
service="message-broker"

messageBroker_ip, messageBroker_port = discovery_registration.discover_sb_service(tile,service)
```

- Getting AMQP **Topic** and **dataFlowId** to **push** data into the **Message Broker**:
```
dataflowId, topic = discovery_registration.register(dataflowmetadata,tile)

opts.address="amqp://"+username+":"+password+"@"+messageBroker_ip+":"+str(messageBroker_port)+":/topic://"+topic

jargs = json.dumps(args)
```

## Usage

Let's take an example of CITS message producer as shown here in [sender.py](https://github.com/5gmetadmin/message-data-broker/blob/main/examples/activemq_clients/cits_sender_python/sender.py) for reference.

- Pass the latitude and longitude GPS position of your sensor device as shown here in :
```
# Geoposition - Next steps: from GPS device.
latitude = 43.3128
longitude = -1.9750

```
- Replace with your ***metadata*** in this section shown below. 

```
dataflowmetadata = {
    "dataTypeInfo": {
        "dataType": "cits",
        "dataSubType": "json"
    },
    "dataInfo": {
        "dataFormat": "asn1_jer",
        "dataSampleRate": 0.0,
        "dataflowDirection": "upload",
        "extraAttributes": None,
    },
    "licenseInfo": {
        "licenseGeolimit": "europe",
        "licenseType": "profit"
    },
    "dataSourceInfo": {
        "sourceTimezone": 2,
        "sourceStratumLevel": 3,
        "sourceId": 1,
        "sourceType": "vehicle",
        "sourceLocationInfo": {
            "locationQuadkey": tile,
            "locationCountry": "ESP",
            "locationLatitude": latitude,
            "locationLongitude": longitude
        }
    }   
}
```
- Use the sample [content.py](https://github.com/5gmetadmin/message-data-broker/blob/main/examples/activemq_clients/cits_sender_python/content.py) to generate your messages. Here as you can see the ***msgbody** contains the CITS message.  
```
def messages_generator(num, tile, msgbody='body_cits_message'):
    messages.clear()
    
    #print("Sender prepare the messages... ")
    for i in range(num):        
        props = {
                    "dataType": "cits",
                    "dataSubType": "cam",
                    "dataFormat":"asn1_jer",
                    "sourceId": 1,
                    "locationQuadkey": tile+str(i%4),
                    "body_size": str(sys.getsizeof(msgbody))
                    }

        messages.append( Message(body=msgbody, properties=props) )

```

### Steps to run examples

- Modify [**address.py**](https://github.com/5gmetadmin/message-data-broker/blob/main/examples/activemq_clients/cits_sender_python/address.py) to put the ***appropriate ip***, ***port*** and ***topic*** given by **your message broker** or run with options:

- Additional arguments as highlighted below could be parsed to the [sender.py](https://github.com/5gmetadmin/message-data-broker/blob/main/examples/activemq_clients/cits_sender_python/sender.py) :
    ```
    - h, --help            show this help message and exit
    - a ADDRESS, --address=ADDRESS
        = address to which messages are sent (default amqp://5gmeta-user:5gmeta-password@192.168.15.34:5673/topic://cits)
    - m MESSAGES, --messages=MESSAGES
        = number of messages to send (default 100)
    - t TIMEINTERVAL, --timeinterval=TIMEINTERVAL
        = messages are sent continuosly every time interval seconds (0: send once) (default 10) 
    ```
- In one terminal window run wither of the sender scripts **depending upon whether you are running your S&D connected to an database or not**. You can add additional arguments as shown before:
    ```python3 sender.py``` or ```python3 sender_with_sd_database_support.py```

    Example output can be seen below:

    ![Sender example](images/sender_data_broker.png)





- If you want to do some debugging and check if your messages are being sent run in another terminal to receive messages (you have to modify **address.py** in order to put the ***appropriate ip***, ***port*** and ***topic*** given by **your message broker**) :

    Run ```python3 receiver.py``` to see the received messages on the subscribed AMQP topic.

    ![Receiver example](images/receiver_data_broker.png)

- Use the ActiveMQ admin web page to check Messages Enqueued / Dequeued counts match. 

- You can control which AMQP server the examples try to connect to and the messages they send by changing the values in **config.py**

- ***NB:*** You have to take into account that any modification made on dataflowmetadata must be applied too into the content.py file in order to generate the appropriate content.

## Pseudo movement example

This example demonstrates data being produced by a moving sensor device.

- Added some movement around a fixed GPS position in order to simulate movement.
    -  Example:

       - [cits_send_moving_location.py](cits_send_moving_location.py)

This way we can move around a MEC that covers tiles:

* 031333123201033
* 031333123201211

and a ***secondary one*** that covers tiles:

* 031333123201212
* 031333123201213
* 031333123201223
* 031333123202223

## Other resources
***The initial example for this client is at the link: https://github.com/apache/activemq/tree/main/assembly/src/release/examples/amqp/python***

    - *https://qpid.apache.org/releases/qpid-proton-0.36.0/proton/python/docs/tutorial.html*
    - *https://access.redhat.com/documentation/en-us/red_hat_amq/6.3/html/client_connectivity_guide/amqppython*

