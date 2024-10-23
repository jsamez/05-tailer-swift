# 스마트 캐리어 프로젝트

## 팀명: 5조 | 테일러스위프트

### 목차
1. [개요](#개요)
2. [목표](#목표)
3. [시스템 아키텍처](#시스템-아키텍처)
4. [개발 진행 상황](#개발-진행-상황)
5. [결과](#결과)
6. [고찰](#고찰)
7. [향후 과제](#향후-과제)
8. [발표 자료](#발표-자료)
---

## 개요
스마트 캐리어 프로젝트는 시장에서 무거운 장바구니를 들고 다니는 할머니와 어머니를 보며 영감을 받았습니다. 자녀들이 도울 수 있는 경우도 있지만, 그렇지 못할 때는 자주 쉬어가며 힘들게 장을 보시는 모습을 보고, 자율주행 장바구니가 있다면 좋겠다는 생각을 하게 되었습니다.

현대의 객체 인식 기술은 다양한 환경에서 사람의 위치를 추적하고 그 거리를 정확하게 측정하는 데에 어려움이 있습니다. 특히, 사람들이 밀집된 환경이나 불규칙한 조명 아래에서 신뢰할 수 있는 정보를 제공하는 것이 중요하며, 사용자가 이동 방향을 실시간으로 확인할 수 있는 시스템이 필요합니다.

---

## 목표
이 프로젝트의 목표는 다음과 같습니다:

- 실시간으로 사람의 위치와 거리를 탐지하여 추적.
- 이동하는 인물의 방향에 따라 추적하며 객체의 거리를 측정하는 시스템 개발.

---

## 시스템 아키텍처

![아키텍쳐](images/아키텍쳐.png)

![구성도](images/구성도.png)

![flow_chart](images/flow_chart.drawio.png)

---

## 개발 진행 상황

![간트차트](images/ganttchart.png)

---

## 결과

![객체 인식](images/Object_Detection.gif)
- 다음 프레임에도 사용자를 인식하기 위해 IOU방식을 채택해서 진행함.
- 이때 사용자를 완전히 가리거나, 사용자 위치에 다른사람이 있을경우 다른 사람을 사용자로 인식함.

![거리 추정](images/Depth_Estimaion.gif)
- monodepth모델의 경우 상대적인 거리를 추정하는 모델이라 depth의 값이 갑자기 변화하는 문제가 발생함.
- Cropped image를 사용하여 사용자만 있는 사진을 입력하여 사용자만의 거리를 측정하게 함.
- 이 과정에서 노이즈가 발생, 가우시안 블러를 이용하여 노이즈를 제거함
- RGB chanel 보다 Blue chanel만 을 이용하여 값을 안정화함.

![방향 추정](images/Direction_Estimation.gif)
- 초기 구성에서 방향의 판단을 바운딩 박스가 전부 특정영역에 들어와야 다른 방향으로 가는걸인식
- 이 과정에서 팔을 벌렸을때 바운딩 박스가 넘어 가지 않아 회전이 늦게 되는 문제가 발생
- MediaPipe의 poseestimation을 이용하여 어깨를 추측하여 바운딩 박스의 크기를 고정
- 바운딩 박스보단 어깨의 중심이 어느 영역에 위치했는가를 추정하여 방향을 결정 -> 딜레이가 줄어듬

![명령 전송](images/Forward_and_Stop.gif)
- 시간관계상 서버를 통한 통신은 제작이 불가능 하여 테스트때 사용하던 Rc car앱의 Bluetooth protocol를 이용하여 구현

---

## 고찰

---

## 향후 과제

---
## 발표 자료
https://docs.google.com/presentation/d/1gs7zfCVsGriqfyBAdbsQSrKQAs58_GKxZbZFjJTXn0Q/edit?usp=sharing


