# Consumer and Event Producer Examples
In this section, ww walkthrough the Kafka consumer examples. Three sample consumer examples are provided within the [repo](https://github.com/5gmetadmin/stream-data-gateway/tree/main/examples/consumer) for cits, video and image datatypes respectively.

## Required packages to be installed

```pip3 install -r examples/requirements.txt```

### More dependencies (apt-get):

* python3-qpid-proton
* python3-avro
* python3-confluent-kafka
* gstreamer1.0-plugins-bad
* gstreamer1.0-libav
* python3-gst-1.0

Also install with pip3:

* kafka-python
* numpy
## Usage

### *Consumer instructions*
- Use [platform-client](https://github.com/5gmetadmin/stream-data-gateway/tree/main/utils/platform-client) to receive appropriate topics and IPs and ports to be used.

- Select the suitable consumer as per the produced data and use as follows: 
```
python3 cits-consumer.py topic platformaddress bootstrap_port registry_port

``` 
or

```
python3 video-consumer.py platformaddress bootstrap_port topic dataflow_id

```
#### More examples
There are other such examples that are complete and don't need to use external util to get topic and ip/port to access the system.

* [cits/cits-kafka-consumer.py](https://github.com/5gmetadmin/stream-data-gateway/blob/main/examples/consumer/cits/cits-kafka-consumer.py)
* [image/image-kafka-consumer.py](https://github.com/5gmetadmin/stream-data-gateway/blob/main/examples/consumer/image/image-kafka-consumer.py)
* Avro Producer: [producer/avro_producer_events.py](https://github.com/5gmetadmin/stream-data-gateway/blob/main/examples/producer/avro_producer_events.py)


