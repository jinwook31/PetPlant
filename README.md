# PetPlant

One-person households desire to raise a pet to relief loneliness, but due to the busy lift, they leave their house for long time.
This could cause problem to pet such as separation anxiety.
Therefore, PetPlant provides an pet's status and context by mapping it to a artificial plant.

video

## Pre-requirement
### Hardware Components
#### Sensors
Feather board (ESP8266)

MPU6050

Grove Sound Sensor(https://wiki.seeedstudio.com/Grove-Sound_Sensor/)

[img]
![]()

#### Jetbot Side
Optical fiber

Servo motor

LED (any color is fine!)

3D printed components and pot

[img]
![]()

### Software (Library)
Scikit-learn, pandas, numpy, mpu6050-raspberrypi, Flask

#### Setup
```
pip install pandas, numpy, mpu6050-raspberrypi -y
pip install nose -y
pip install scikit-learn, flask -y
```

## System Flow

### Data Collection
For the data collection to develop an KNN model, we used MPU6050 and Grove sound sensor and uploaded to an application that receive and store the data. 
Codes for the feather board (ESP8266), which sends the data to application, is in both `./Sensor/gyro_toPythonServer` and `./Sensor/sound_toPythonServer` folder.
Also, you could launch the application by @ the '' with @. The application save the data and export it into a csv format.

[img]
![]()

### KNN Clustering with Moving windows
After the data collection, we classified the data into 3 groups. We used time-domain scaled with the stacked moving windows. However, we didn't scaled the time-domain scaled data with Min-Max, due to the single window input in real-time classification. As shown in the figure, it classifies 3 groups well and for the real-time data too.

![](https://raw.githubusercontent.com/jinwook31/PetPlant/master/clustering%20result.PNG)

### Real-Time Classification
For the real-time classifcation, we used the Flask server to implement REST API. As we send the data from the feather board to application in data collection, we changed the ip address to the jetbot and send an json format data to the Flask server.

You could run the server by `python3 server.py` to initate the server that receives data from the sensor and make it as an time-domain scaled window. It classify the status with the KNN model generated previously(shake_classification.pkl) and provide and interaction with manipulating servo moter and LED.

### Interaction
For the interaction, there are total 6 combination (2 led x 3 servo movement). LED represents the voice and servo movement represents the pet tail movement.

## Reference 
[1] https://github.com/vijaykumarwalikar/mpu6050-data-recording-visualization-tool
