# DMS Dataset

The DMS dataset contains messages with information about Driving Monitoring System (DMS) detected.  

## Header

- `protocolVersion`: The version of the protocol used         
- `messageID`: A unique ID for the message
- `stationID`: The ID of the station that detected the DMS

## DMS           

- `timestamp`: The timestamp when the DMS was detected        
- `referencePosition`:                     
    - `latitude`: The latitude of the location of the DMS                     
    - `longitude`: The longitude of the location of the DMS       
- `dms_level`: The level of severity of the DMS (1 to 5)   
- `dms_trigger`:                       
   - The trigger that detected the DMS (e.g. sudden braking, swerving, drowsy.. etc.)