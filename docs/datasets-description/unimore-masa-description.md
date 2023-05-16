# MASA Dataset

The MASA dataset contains messages with information about road users (vehicles, pedestrians, etc.) detected in Modena, Italy.  

## Header

- `protocolVersion`: The version of the protocol used.        
- `messageID`: A unique ID for the message
- `stationID`: The ID of the station that detected the road users.

## MASA   

### Parameters

- `source_idx`: The index of the detector that captured the information.         
- `timestamp`: The timestamp when the road users were detected.

### Road Users                     

- `category`: The category of the road user (e.g. car, pedestrian, etc.)
- `latitude`: The latitude of the road user                   
- `longitude`: The longitude of the road user       
- `speed`: The speed of the road user in km/h.       
- `orientation`: The orientation of the road user in degrees.
- `cam_id`: The ID of the camera that detected the road user.
- `object_id`: A unique ID for the road user.