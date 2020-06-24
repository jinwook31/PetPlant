# PetPlant

One-person households desire to raise a pet to overcome loneliness but due to the @@,
Target: 원격에 있는 동물에 대한 그리움을 느끼는 사람들 
1인가구로 집을 자주 비우는 사람
본가에서 멀리 떨어진 곳에서 생활하는 사람

Therefore, PetPlant is an @@.
반려동물의 행동을 실시간으로 감지하고 사용자에게 물리적인 피드백을 제공하는 Home Robot

Interaction Modality
꼬리 흔들기 -> 꼬리와 비슷한 움직임
짖기 -> led의 밝기 변화
두가지 modality를 동시에 (혹은 복합적으로) 전달할 수 있는 방법 탐색

## Pre-requirement
### Hardware Components
#### Sensors
Feather board - ESP8266

MPU6050

Grove Sound Sensor(https://wiki.seeedstudio.com/Grove-Sound_Sensor/)

#### Jetbot Side
LED stripe

Servo motor


### Software (Library)
Scikit-learn, pandas, numpy, mpu6050-raspberrypi, Flask


#### Setup
```
pip install pandas, numpy, mpu6050-raspberrypi -y
pip install nose -y
pip install scikit-learn, flask -y
```

## System Flow

### Context Mapping

### Data Collection
For the data collection, we used an application that receive and store @. <app or code link> csv format

### KNN Clustering with Moving windows
3 groups with the windows. However, we didn't scaled with Min-Max, due to the single window input in real-time classification.

### Real-Time Classification
For the real-time classifcation, we used Flask server to implement REST API.

run server.py to initate the server that receives data from the sensor.

### Interaction

## Reference 
[1] https://github.com/vijaykumarwalikar/mpu6050-data-recording-visualization-tool
