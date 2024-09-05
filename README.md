# PID 제어를 이용한 자율주행 로봇의 경로 추적 및 군집주행


## 프로젝트 소개
레고 마인드스톰 EV3 로봇을 활용한 자율주행 로봇의 경로 추적 및 군집주행 프로젝트입니다. PID 제어를 통해 경로를 추적하며, 초음파 센서를 사용하여 안전거리를 유지하고 군집주행을 수행합니다.


## 시스템 설계
<details>
<summary>PID 제어를 이용한 경로 추적</summary>  자율주행 로봇은 목표 경로를 따라가기 위하여 조향 조작이 필요합니다. PID(Proportional Integral Derivative) 제어기를 활용하여 자율주행 로봇이 트랙을 정확하게 따라가도록 설계하였습니다. PID 제어기의 제어식은 다음과 같습니다.

  
![image](https://github.com/user-attachments/assets/685f3f88-f1af-4e9e-99eb-13d185c46d9f)


로봇마다 PID 제어 이득의 최적화된 값이 다르므로 수동 튜닝을 통하여 각 로봇에 맞게 최적화된 값을 구하였습니다. 


![image](https://github.com/user-attachments/assets/811efa4b-ca42-4599-9dc5-85fa6055db60)

이러한 제어 이득 값들은 각 로봇의 특성과 주행 환경에 맞게 조정된 값으로 안정적인 주행을 위해 설정되었습니다.
</details>



## 프로젝트 결과 영상
[![Watch the video](https://img.youtube.com/vi/KbpQ3JgK9nE/0.jpg)](https://youtu.be/KbpQ3JgK9nE)


위 이미지를 클릭하면 결과 영상을 확인할 수 있는 YouTube 페이지로 이동합니다.
