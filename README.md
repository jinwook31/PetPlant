# PetPlant

As the number of one-person households is increasing, some are experiencing psychological issues such as depression, loneliness, and lack of social interaction. They are trying to address these issues through raising pets, as studies have shown that doing so may be helpful in dealing with such problems. However, there are many reason that people can’t spend their time with their pet allday, such as life pattern, work, school. Therefore there is a clear needs that they want to know how their pets are doing while they are out.

However, most of the IoT products for pet care are based on a built-in camera to let users monitor their pet. The built-in cameras have caused various issues related to privacy concerns and lack of awareness of the system presence, which leads to anxiety and discontinued usage of the product. One of the comments with this was that they ‘pull the IoT camera plug off when they arrive home’, due to the sense of someone might watch the video.

Therefore, PetPlant provides an pet's status and context by mapping it into a artificial plant.

![](https://raw.githubusercontent.com/jinwook31/PetPlant/master/final%20image.PNG)

Demo Link: https://youtu.be/UauxqAE8PQg

## Pre-requirement
### Hardware Components
#### Sensors
Feather board (ESP8266)

MPU6050

Grove Sound Sensor(https://wiki.seeedstudio.com/Grove-Sound_Sensor/)

![](https://raw.githubusercontent.com/jinwook31/PetPlant/master/sensor%20image.PNG)

#### Jetbot Side
Optical fiber

Servo motor

LED (any color is fine!)

3D printed components and pot

![](https://raw.githubusercontent.com/jinwook31/PetPlant/master/structure.PNG)

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
Also, you could launch the web application by running the `df` with the HTML web server. The application helps you to save the data and export it into a csv format.

![](https://raw.githubusercontent.com/jinwook31/PetPlant/master/application%20image.PNG)

### KNN Clustering with Moving windows
After the data collection, we classified the data into 3 groups. From other MPU library that supports recoding [1], you could build your own model by using `python3 ./KNN_MPU/knnClassificaition.py` and `python3 ./KNN_MPU/realTime (Direct Connection).py` to test the real-time data on the model in local environment. 

We used time-domain scaled with the stacked moving windows. However, we didn't scaled the time-domain scaled data with Min-Max, due to the single window input in real-time classification. As shown in the figure, it classifies 3 groups well and for the real-time data too.

![](https://raw.githubusercontent.com/jinwook31/PetPlant/master/clustering%20result.PNG)

### Real-Time Classification
The overall aglorithm for real-time uses queue. As the figure below, it gets 1 input and check the status when the queue contatins proper lenght of data. After classification, it reacts depending on the result and removes oldest 2 data from the queue.

![](https://raw.githubusercontent.com/jinwook31/PetPlant/master/Queue.JPG)

For the real-time classifcation, we used the Flask server to implement REST API. As we send the data from the feather board to application in data collection, we changed the ip address to the jetbot and send an json format data to the Flask server.

You could run the server by `python3 ./Real Time Class w Server/server.py` to initate the server that receives data from the sensor and make it as an time-domain scaled window. It classify the status with the KNN model generated previously(shake_classification.pkl) and provide and interaction with manipulating servo moter and LED.

### Interaction
For the interaction, there are total 6 combination (2 led x 3 servo movement). LED represents the voice and servo movement represents the pet tail movement.

## Reference 
[1] https://github.com/vijaykumarwalikar/mpu6050-data-recording-visualization-tool
