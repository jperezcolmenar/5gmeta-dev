# CAM Dataset 

The CAM dataset contains messages with information captured by Cooperative Awareness Messages (CAM). 

## Header 

- `protocolVersion`: The version of the protocol used    
- `messageID`: A unique ID for the message
- `stationID`: The ID of the station that captured the CAM  

## CAM  

- `generationDeltaTime`: Time since last CAM message  

### basicContainer

- `stationType`: The type of the station that captured the CAM
- `referencePosition`:
    - `latitude`: The latitude of the station
    - `longitude`: The longitude of the station
    - `positionConfidenceEllipse`: Confidence ellipse of the position
       - `semiMajorConfidence`: Major axis confidence
       - `semiMinorConfidence`: Minor axis confidence
       - `semiMajorOrientation`: Major axis orientation            
    - `altitude`:
        - `altitudeValue`: The altitude value 
        - `altitudeConfidence`: Confidence in the altitude

### highFrequencyContainer        

- `heading`:    
    - `headingValue`: The heading value   
    - `headingConfidence`: Confidence in the heading value       
- `speed`: 
    - `speedValue`: The speed value 
    - `speedConfidence`: Confidence in the speed value
- `driveDirection`: The drive direction (forward, backward,unavailable)           
- `vehicleLength`:    
    - `vehicleLengthValue`: The length of the vehicle      
    - `vehicleLengthConfidenceIndication`: Confidence in the vehicle length           
- `vehicleWidth`: The width of the vehicle
- `longitudinalAcceleration`:           
    - `longitudinalAccelerationValue`: The longitudinal acceleration value
    - `longitudinalAccelerationConfidence`: Confidence in the longitudinal acceleration      
- `curvature`:    
    - `curvatureValue`: The curvature value   
    - `curvatureConfidence`: Confidence in the curvature value
- `curvatureCalculationMode`: How the curvature was calculated     
- `yawRate`:             
    - `yawRateValue`: The yaw rate value  
    - `yawRateConfidence`: Confidence in the yaw rate value           
- `accelerationControl`: Acceleration control status        
- `lanePosition`: The lane position of the vehicle