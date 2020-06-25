# PetPlant

One-person households desire to raise a pet to relief loneliness, but due to the busy lift, they leave their house for long time.
This could cause problem to pet such as separation anxiety.
Therefore, PetPlant provides an pet's status and context by mapping it to a artificial plant.

[img]

## Pre-requirement
### Hardware Components
#### Sensors
Feather board - ESP8266

MPU6050

Grove Sound Sensor(https://wiki.seeedstudio.com/Grove-Sound_Sensor/)

#### Jetbot Side
Optical fiber
![](https://ae01.alicdn.com/kf/HTB1MD4_PFXXXXXTaXXXq6xXFXXXD/led.jpg){: width="50%" height="50%"}

Servo motor

LED


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
For the data collection, we used an application that receive and store @. <app or code link> csv format

### KNN Clustering with Moving windows
3 groups with the windows. However, we didn't scaled with Min-Max, due to the single window input in real-time classification.

### Real-Time Classification
For the real-time classifcation, we used Flask server to implement REST API.

run server.py to initate the server that receives data from the sensor.

### Interaction
Bark to LED, tail shaking to servo movement

## Reference 
[1] https://github.com/vijaykumarwalikar/mpu6050-data-recording-visualization-tool
