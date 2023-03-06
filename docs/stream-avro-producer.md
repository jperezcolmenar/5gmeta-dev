# Avro events producer examples
This folder contains avro producer example to produce events.

## Usage


    
- Avro Producer config format to produce an event with avro serializer:
```python
schema_registry_client = SchemaRegistryClient(schema_registry_conf)

avro_serializer = AvroSerializer( schema_registry_client, 
                                  schema_str,
                                  msg_to_dict )

producer_conf = {'bootstrap.servers': args.bootstrap_servers,
                  'key.serializer': StringSerializer('utf_8'),
                  'value.serializer': avro_serializer}

producer = SerializingProducer(producer_conf)
.
.
.
producer.poll(0.0)
```

Usage is: 
```
python3 avro_producer_events.py -b bootstrap_ip:9092 -s http://schema_ip:8081 -t topic
```

Example : 
```
python3 avro_producer_events.py -b 192.168.15.181:9092 -s http://192.168.15.181:8081 -t events_5gmeta
```

