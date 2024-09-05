# PID 제어를 이용한 자율주행 로봇의 경로 추적 및 군집주행


## 프로젝트 소개
레고 마인드스톰 EV3 로봇을 활용한 자율주행 로봇의 경로 추적 및 군집주행 프로젝트입니다. PID 제어를 통해 경로를 추적하며, 초음파 센서를 사용하여 안전거리를 유지하고 군집주행을 수행합니다.


## 시스템 설계
<details>
<summary>PID 제어를 이용한 경로 추적
</summary>
  

>자율주행 로봇은 목표 경로를 따라가기 위하여 조향 조작이 필요합니다.
>PID(Proportional Integral Derivative) 제어기를 활용하여 자율주행 로봇이 트랙을 정확하게 따라가도록 설계하였습니다. PID 제어기의 제어식은 다음과 같습니다.

  
![image](https://github.com/user-attachments/assets/685f3f88-f1af-4e9e-99eb-13d185c46d9f)


>로봇마다 PID 제어 이득의 최적화된 값이 다르므로 수동 튜닝을 통하여 각 로봇에 맞게 값을 설정하였습니다.


![image](https://github.com/user-attachments/assets/811efa4b-ca42-4599-9dc5-85fa6055db60)
</details>


<details>
<summary>군집주행 알고리즘
</summary>
>초음파 센서를 사용하여 로봇 간 거리를 실시간으로 측정하고, 그 거리에 따라 로봇의 속도를 조절하여 군집 주행을 가능하게 합니다.

  
![image](https://github.com/user-attachments/assets/10dcd28f-b090-4dfd-8aa5-b8cb95f36e44)


>이 알고리즘의 핵심은 로봇 간 거리 측정과 이에 따른 속도 조절입니다. 먼저, 초음파 센서를 이용해 앞 차량과의 거리를 실시간으로 측정합니다(1행). 이 거리가 설정된 최소 안전거리인 35cm 이하로 줄어들면 속도를 약 0.12m/s 로 감소시켜 거리를 유지하고, 27cm 이하로 줄어들 경우에는 정지하도록 설계하였습니다(4-8 행). 로봇 간 거리가 35cm 이상으로 벌어지면 후행로봇의 속도를 약 0.17m/s 로 증가시켜 35cm 의 거리를 유지하면서 군집 주행이 가능하도록 설계하였습니다(10-11 행). 

</details>

<details>
<summary>신호등 인식
</summary>
>자율주행 로봇이 신호등을 인식하고 이에 따라 행동할 수 있도록 로봇에 장착된 카메라를 이용하여 이미지 분류 모델을 구축하였습니다. 
>이 모델은 CNN(Convolutional Neural Network)을 활용하여 신호등 이미지를 학습시켰고 클래스의 개수는 총 2 개이며 Red 이미지와 Green 이미지 각각 1500 장을 training data 로 사용하였습니다. training data 내에서 훈련 데이터와 검증 데이터로 나누어 그 비율을 8:2 로 지정하였고 Red 224 장과 Green 222 장 총 446 장을 test data 로 구성하였습니다. 로봇에 장착된 카메라를 통해 신호등을 인식하고 신호에 따라 로봇이 적절히 반응할 수 있도록 구현하였습니다.
</details>

## 프로젝트 결과 영상
[![Watch the video](https://img.youtube.com/vi/KbpQ3JgK9nE/0.jpg)](https://youtu.be/KbpQ3JgK9nE)


위 이미지를 클릭하면 결과 영상을 확인할 수 있는 YouTube 페이지로 이동합니다.
