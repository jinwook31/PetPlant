# PetPlant

One-person households desire to raise a pet to relief loneliness, but due to the busy lift, they leave their house for long time.
This could cause problem to pet such as separation anxiety.
Therefore, PetPlant provides an pet's status and context by mapping it to a artificial plant.

video

## Pre-requirement
### Hardware Components
#### Sensors
Feather board - ESP8266

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
For the data collection to develop an KNN model, we used an application that receive and store the data. 
You could launch the application by @ the ./@@ with @. 
It save the data and export it into a csv format.

[img]
![]()

### KNN Clustering with Moving windows
After the data collection, we classified the data into 3 groups. We used time-domain scaled with the stacked moving windows. However, we didn't scaled the time-domain scaled data with Min-Max, due to the single window input in real-time classification. As shown in the figure, it classifies 3 groups well and for the real-time data too.

[img]
![](https://raw.githubusercontent.com/jinwook31/PetPlant/master/clustering%20result.PNG)

### Real-Time Classification
For the real-time classifcation, we used Flask server to implement REST API.

run server.py to initate the server that receives data from the sensor.

### Interaction
Bark to LED, tail shaking to servo movement

## Reference 
[1] https://github.com/vijaykumarwalikar/mpu6050-data-recording-visualization-tool
