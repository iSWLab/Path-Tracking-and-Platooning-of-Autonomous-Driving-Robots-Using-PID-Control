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


![image](https://github.com/user-attachments/assets/811efa4b-ca42-4599-9dc5-85fa6055db60)


>로봇마다 PID 제어 이득의 최적화된 값이 다르므로 수동 튜닝을 통하여 각 로봇에 맞게 값을 설정하였습니다.





![image](https://github.com/user-attachments/assets/b1eb64d3-258d-4802-8dc6-7a890f565a5c)

<blockquote>
LSA(Light Sensor Array)센서를 사용하여 각 센서가 측정한 조도 값을 리스트 형태로 저장하고 활용하며 각 센서에서 얻은 값을 기반으로 오차값을 계산합니다.
  
8 개의 센서 값 중에서 왼쪽 끝 2 개의 값의 평균을 이용한 오차값은 다음과 같습니다.
</blockquote>


![image](https://github.com/user-attachments/assets/d913325b-0685-48db-af4a-8c2eae4646da)


<blockquote>
여기서 th 란 목표값을 나타내며, 이는 로봇이 센서를 통해 트랙에서 측정한 흰색 선의 값을 나타냅니다. 중앙의 오차값(error2), 오른쪽의 오차값(error3)도 이와 같이 계산됩니다. 

이 오차값들은 로봇이 트랙 위에서 벗어나지 않도록 조작량을 결정하는데 활용하고 조작량은 PID 제어 식에 따라 계산됩니다. 이 공식을 통해 각 오차값에 대한 3 가지 조작량이 생성되며, 로봇의 움직임을 섬세하게 제어하여 트랙을 정확하게 주행할 수 있도록 합니다.
</blockquote>


![사진](https://github.com/user-attachments/assets/80cec2a4-b0e2-4910-94d2-616699f29cdd)


<blockquote>
Algorithm1 은 3 가지 조작량의 사용 기준을 나타냅니다. 왼쪽 끝의 0 번 센서, 중앙의 3 번 및 4 번 센서, 그리고 오른쪽 끝의 7 번 센서를 기준으로 정해집니다. 로봇에 장착된 센서마다 측정 값이 다르기 때문에, 측정 후에 적절한 기준을 설정해야 합니다.
</blockquote>

</details>


<details>
<summary>군집주행 알고리즘</summary>
<blockquote>
초음파 센서를 사용하여 로봇 간 거리를 실시간으로 측정하고, 그 거리에 따라 로봇의 속도를 조절하여 군집 주행을 가능하게 합니다.
</blockquote>

![image](https://github.com/user-attachments/assets/10dcd28f-b090-4dfd-8aa5-b8cb95f36e44)

<blockquote>
이 알고리즘의 핵심은 로봇 간 거리 측정과 이에 따른 속도 조절입니다. 
  
먼저, 초음파 센서를 이용해 앞 차량과의 거리를 실시간으로 측정합니다(1행). 이 거리가 설정된 최소 안전거리인 35cm 이하로 줄어들면 속도를 약 0.12m/s로 감소시켜 거리를 유지하고, 27cm 이하로 줄어들 경우에는 정지하도록 설계하였습니다(4-8행). 로봇 간 거리가 35cm 이상으로 벌어지면 후행 로봇의 속도를 약 0.17m/s로 증가시켜 35cm의 거리를 유지하면서 군집 주행이 가능하도록 설계하였습니다(10-11행).
</blockquote>
</details>

<details>
<summary>신호등 인식</summary>
<blockquote>
자율주행 로봇이 신호등을 인식하고 이에 따라 행동할 수 있도록 로봇에 장착된 카메라를 이용하여 이미지 분류 모델을 구축하였습니다. 

  
이 모델은 CNN(Convolutional Neural Network)을 활용하여 신호등 이미지를 학습시켰고 클래스의 개수는 총 2 개이며 Red 이미지와 Green 이미지 각각 1500 장을 training data 로 사용하였습니다. training data 내에서 훈련 데이터와 검증 데이터로 나누어 그 비율을 8:2 로 지정하였고 Red 224 장과 Green 222 장 총 446 장을 test data 로 구성하였습니다. 로봇에 장착된 카메라를 통해 신호등을 인식하고 신호에 따라 로봇이 적절히 반응할 수 있도록 구현하였습니다.
</blockquote>
</details>


## 실험 방법
<blockquote>
앞서 설계한 자율주행 및 군집주행 시스템을 통합하여 검증하기 위해 실험 트랙에서 구동을 진행하였습니다.
</blockquote>
<details>
<summary>실험 도구</summary>

  
![image](https://github.com/user-attachments/assets/cd8ef478-4fd8-4874-a3f7-7360b7d5389d)

<blockquote>
본 연구에 사용한 선행 로봇(좌)과 후행 로봇(우)입니다. 후행 로봇은 선행 로봇과의 거리를 측정하기 위해 초음파 센서가 앞쪽에 장착되어 있고 라인을 추적하기 위해 이용하는 LSA 센서도 앞쪽 하부에 장착되어 있습니다.
</blockquote>


![image](https://github.com/user-attachments/assets/2eccd59e-8f7e-48a2-aca7-feef7c84d017)


<blockquote>
실험을 확인하기 위한 트랙입니다. 초록색 선은 선행 로봇의 출발 지점을, 빨간색 선은 후행 로봇의 출발 지점을 나타냅니다. 노란색 선은 신호등을 인식하기 위해 멈추어야 하는 지점을 나타내고 파란색 선은 서행 구역을 표시합니다.
</blockquote>



![image](https://github.com/user-attachments/assets/3297b4b9-320e-4866-ac3d-d5b856767627)


<blockquote>
 로봇이 신호등을 인식하고 이에 맞춰 주행을 제어할 수 있도록 두 가지 형태(원형, 사각형)의 신호등을 설정하였습니다. 신호등은 감지 센서에 의해 작동됩니다.
</blockquote>
</details>

## 실험 결과


![image](https://github.com/user-attachments/assets/a0b77754-a40e-4818-ab64-607cbe0c96fc)


<blockquote>
선행 로봇이 경로 추적을 할 때 PID 제어 적용 전(좌)과 후(우)를 비교한 데이터 입니다. 
  
 x 축은 로봇의 트랙 2 바퀴 완주 시간을 나타낸 것이고 y 축은 2. PID 제어를 이용한 경로 추적 및 군집주행 시스템 설계에서의 error2 를 나타냅니다. 
 
 그래프에서 볼 수 있듯이, PID 를 적용하지 않는 경우 일정한 패턴 없이 error 값이 급격하게 변동하며 불안정적인 주행을 보여줍니다. 이는 직선 구간과 코너 구간에서 흰색 선을 정확하게 추적하지 못 하고 있다는 것을 나타냅니다. 또한, 로봇이 트랙을 벗어나는 문제가 발생하여 벗어난 로봇을 트랙으로 옮겨주는 작업이 필요했습니다. 따라서 PID 제어 전 주행에서는 시간이 더 소요되며 비효율적이라는 것을 알 수 있었습니다. PID 를 적용하는 경우 error 값이 비교적 일정한 패턴으로 유지되며, 직진 구간에서 급격한 변동 없이 흰색 선을 잘 따라가고 있는 것을 보여줍니다. 코너 구간에서 흰색 선을 잠시 벗어났지만 곧바로 다시 흰색 선으로 돌아와 안정적으로 주행하며 이는 PID 제어가 효과적으로 작동하고 있음을 나타냅니다.
</blockquote>

![image](https://github.com/user-attachments/assets/17dacbee-4da5-47d4-b9b3-db69a9ad2f70)


<blockquote>
위 사진은 실험에서 두 로봇이 동시에 출발한 후, 서로 적절한 거리를 유지하며 주행하는 모습을 확인하였습니다. 이를 통해 시스템의 자율주행과 군집주행 기능이 실험 환경에서도 성공적으로 동작함을 확인하였습니다.
</blockquote>

## 프로젝트 결과 영상 
[![Watch the video](https://img.youtube.com/vi/KbpQ3JgK9nE/0.jpg)](https://youtu.be/KbpQ3JgK9nE)


위 이미지를 클릭하면 결과 영상을 확인할 수 있는 YouTube 페이지로 이동합니다.
