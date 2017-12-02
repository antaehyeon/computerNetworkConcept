# Sejong Computer Network
세종대학교 김영복 교수님 컴퓨터 네트워크 기말 정리본 입니다 (PPT 기반, 모르는 내용은 책으로 보충)

## 4단원. 네트워크 계층 (The Network Layer: Data Plane)

목표
: 네트워크 계층이 호스트 사이의 통신 서비스를 어떻게 통과하는지

### 4-1. 네트워크 계층 개요

- 데이터 플랜에 초점을 맞춘 네트워크 계층서비스의 원리 이해
  * network layer 서비스 모델
  * 포워딩 대 라우팅
  * 라우터 작동방법
  * 일반 포워딩
- 인스턴스화, 인터넷에서 구현  

### 네트워크 레이어
![네트워크 레이어](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-4.%20Network%20Layer.gif)
- 전송 구간에서 수신 호스트로의 전송 구간 (transport segment from sending to receiving host)
- 송신측에서 세그먼트를 데이터그램으로 캡슐화
- 수신측에서 세그먼트를 전송계층에 전달
- **모든** 호스트, 라우터의 네트워크 계층 프로토콜
- 라우터는 통과하는 모든 IP 데이터 그램의 **헤더 필드를 검사**

### 2가지 주요 네트워크 계층 기능
1. 네트워크 레이어 기능
    * **포워딩(forwarding)**
      라우터 **입력**에서 적절한 라우터 **출력**으로 패킷 이동
    * **라우팅(routing)**
      출발지에서 목적지까지 패킷으로 이동하는 **경로를 결정**
2. 분석 : 경로를 정하는 것
    * 포워딩(forwarding) - 부분적인
      프로세스의 단일교환을 통한 것(process of getting through single interchange)
    * 라우팅(routing) - 전체적인
      출발지에서 목적지까지의 경로 프로세스

### 네트워크 레이어 : data plane, control plane
1. Data Plane
    * **지역**별, 라우터별 기능
    * 라우터 입력 포트에 도착하는 데이터그램이 라우터 출력 포트로 전달되는 방법을 결정
    * 포워딩(forwarding) 기능
    ![포워딩 기능](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-5.%20forwarding%20function.png)
2. Control Plane
    * 네트워크 **전체** 논리
    * 출발지 호스트에서 목적지 호스트까지의 end-end경로를 따라 라우터간 Datagram이 라우팅 되는 방식을 결정
    * 이중 제어 방식(two control-plane approaches)
      * 전통적인 라우팅 알고리즘 : 라우터에서 구현
      * 소프트웨어 정의 네트워킹(Software-defined networking, SDN) : (원격)서버에서 구현


### 라우터별 제어 계획(Per-router control plane)
![Per-router control plane](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-7.%20Per-router%20control%20plane.gif)
각 라우터의 개별 라우팅 알고리즘 구성요소는 Control Plane에서 상호작용

### 논리적으로 중앙 집중화 된 Control Plane
![Logically centeralized control plane](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-8.%20Logically%20centralized%20control%20plane.png)
고유한(일반적으로 원격) 컨트롤러가 로컬 제어 에이전트(control agents, CAs)와 상호작용


![네트워크 계층](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/network%20layer.png)

### 4-2. 라우터 내부에는 무엇이 있는가?
교수님이 중요하지 않다고 한 부분은 제외되었습니다

### 이더넷 케이블 (UTP) - 어떻게 만드는가 (기말5점)
![4-22. Ethernet Cable (UTP)](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-22.%20Ethernet%20Cable%20(UTP))
해당 라인 순서와 cross cable에 대한부분 숙지

### 라우터 외부 연결
![4-25. Router external connections](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-25.%20Router%20external%20connections)
Console Port : configuration 접속포트



### 5단원. 네트워크 계층: 제어 평면 (The Network Layer: Control Plane)

### 6단원. 링크 계층: 링크, 접속망, 랜(The Link Layer and LANs)
