
## Parking Lot Detector (PLD) Description
PLD uses deep learning and computer vision algorithms to detect parking spaces from infrastructure/traffic cameras


## Data Fields Description
In this section we will understand the PLD data in further details. PLD data schema can be found here [here](https://github.com/5gmetadmin/5gmeta-dev/blob/main/datasets/cits-unimore-modena-pld.json)

PLD data message starts with a `header` section which is standard across all the platform, but has a unique `messageID`

```JSON
{
    "header": {
        "protocolVersion": 2,
        "messageID": 41,
        "stationID": 3907
    },
```

The actual PLD message starts from this key/value pair `pld`:

```JSON
"pld": {
            "sourceid": 92050,
            "sourcegps": [40487111,79494789],
            "timestamp": 1684077089,
            "spaces": [
            {
                "spaceid": 0,
                "space": [
                    44656399,
                    10929777
                ],
                "prediction": 0
            },
            {
                "spaceid": 1,
                "space": [
                    44656526,
                    10929629
                ],
                "prediction": 1
            }
            ]

        }

```

1. `sourceid`: Refers to the unique camera ID of the infrastructure camera
2. `sourcegps`: Refers to the GPS position of the infrastructure camera `[latitude,longitude]`
3. `timestamp`: This field refers to the timestamp when the PLD detections were generated.
4. `spaces`: This is a `list` of key/value pairs of the detected parking spaces. Every parking space in here has three parameters:
    1. `spaceid`: Unique identifier for each parking space.
    2. `space`: The GPS position ([lat, long]) of the centroid of the parking space.
    3. `prediction`: This is a binary value determining the current occupancy status of the parking space. `0` stands for a free spot and `1` is for an occupied parking space.
    
