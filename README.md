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
![4-22. Ethernet Cable (UTP)](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-22.%20Ethernet%20Cable%20(UTP).png)
해당 라인 순서와 cross cable에 대한부분 숙지

### 라우터 외부 연결
![4-25. Router external connections](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-25.%20Router%20external%20connections.png)
Console Port : configuration 접속포트

## 4-3. IP : Internet Protocl
1. datagram 포맷
2. 세분화(fragmentation)
3. IPv4 주소지정(addressing)
4. 네트워크 주소 변환
5. IPv6

## 인터넷 네트워크 레이어
![4-29. The Internet network layer.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-29.%20The%20Internet%20network%20layer.png)
* 호스트, 라우터 네트워크 레이어 기능

* 라우터가 라우팅을 하면서 사용하는 알고리즘
  * Routing Information Protocol, RIP
  * Open Shortest Path First, OSPF
  * Border Gateway Protocol, BGP

## IP 데이터그램(datagram) 포맷 (기말 2문제)
![4-30. IP datagram format](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-30.%20IP%20datagram%20format.png)

* TTL : 최대 남은 홉 수 (각 라우터에서 감소, 128 - 127 - 126 ... 1)
* upper layer : 데이터를 위로 전달(payload)하는 상위 계층 프로토콜
* for fragmentation/reassembly (분열/재조립을 위한) : 4Byte = 1Word

## IP fragmentation, reassembly
![4-31. IP fragmentation, reassembly](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-31.%20IP%20fragmentation,%20reassembly.gif)

* 네트워크 링크에는 MTU(maxtransfer size)가 있으며 최대의 링크 레벨, 프라임 레벨 존재
  * 다양한 링크 유형, 다양한 MTU
* 그물망 내에 큰 IP데이터그램이 나뉘어져 있음
  * 데이터그램은 여러개의 데이터그램
  * 최종 목적지에서만 "재제출" 됨
  * 관련된 조각을 식별하기 위해 사용되는 IP헤더 비트
* fragmentation
  * in : 하나의 큰 Datagram
  * out : 3개의 작은 datagram
    해당 datagram에 각각의 헤더가 추가됨

## IP fragmentation, reassembly
![4-32. IP fragmentation, reassembly.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-32.%20IP%20fragmentation,%20reassembly.png)

## IP addressing: introduction
![4-34. IP addressing.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-34.%20IP%20addressing.png)
  * IP address
    32-bit 호스트 식별자, 라우터 인터페이스
  * interface
    호스트/라우터와 물리적 링크 간 연결
      * 라우터는 일반적으로 여러개의 인터페이스를 가지고 있음
      * 일반적으로 호스트는 하나 또는 두개의 인터페이스가 있음 (예: 유선 이더넷, 무선 802.11i)
  * 각 인터페이스와 관련된 IP주소

  * Q. 인터페이스가 실제로 어떻게 연결되어 있습니까?
  * A. 챕터5와 6에서 배움
  * For now. 하나의 인터페이스가 다른 인터페이스에 연결되어 있는지 걱정할 필요가 없습니다 (방해 라우터가 없음)

  * 각 컴퓨터는 스위치 또는 무선 WiFi에 연결될 수 있음
      * 이더넷 스위치로 연결된 유선 이더넷 인터페이스
      * WiFi 기지국에 연결된 무선 WiFi 인터페이스

## Subnet
  * IP address
    * 서브넷 파트 - 높은 순서 비트
    * 호스트 파트 - 낮은 순서 비트
  * 서브넷은 무엇인가요?
    * IP주소의 동일한 서브넷을 가진 장치 인터페이스
    * **라우터를 끼지 않고** 물리적으로 서로 연결할 수 있음
  * receipe
  ![4-37. Subnets.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-37.%20Subnets.png)
    * 서브넷을 결정하고 호스트 또는 라우터에서 각 인터페이스를 분리하고 격리된 네트워크 섬을 만듬
    * 격리 된 각 네트워크를 **서브넷**이라고 함
    * **ipconfig**
    * /24 = 서브넷 용도로 사용한다
      11111111 11111111 111111111 00000000
    * subnet mask: /24
      항상 24비트는 아님, 조절할 수 있음

    ![4-38. Subnet.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-38.%20Subnet.png)
      * 해당 서브넷은 6개로 구성
      * 가운데의 3개의 선은 별도의 Subnet으로 구성됨

  ## Class A, B, C, D, and E IP Address
  ![4-39. Class A, B, C, D, and E IP Address.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-39.%20Class%20A,%20B,%20C,%20D,%20and%20E%20IP%20Address.png)
  * 해당 IP Address를 통해서 각 IP의 Class를 파악할 수 있음
  * 클래스 D 주소는 멀티캐스트 그룹에 사용되므로, 네트워크 및 호스트 주소를 분리하기 위해 octets나 bit를 할당할 필요가 없음
  * 클래스 E 주소는 연구용으로만 사용

  ## IPv4 Addressing (Class)
  ![4-40. IPv4 Addressing (Class)](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-40.%20IPv4%20Addressing%20(Class).png)
  * Class A : 16,777,216
  * Class B : 65,535
  * Class C : 254
  * 127.x.x.x 주소 범위는 루프백 주소로 예약되어 있음
  * 테스트 및 진단 목적으로 사용

  ## Reserved IP Addressing
  ![4-41. Reserved IP Addresses](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-41.%20Reserved%20IP%20Addresses.png)
  * 특정 호스트 주소는 예약되어 있으며 네트워크 장치에 할당 할 수 없음
  * 모든 호스트 비트 위치에 2진 O (binary Os)가 있는 IP주소는 네트워크 주소용으로 예약되어 있음
  * 모든 호스트 비트 위치에 바이너리가 있는 IP주소는 네트워크 주소용으로 예약되어 있음

  ## Private IP Addresses (기말출제 1문제)
  ![4-42. Private IP Addresses](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-42.%20Private%20IP%20Addresses.png)
  * 공인 IP주소가 글로벌하고 표준화되어 있으므로 공용 네트워크에 연결하는 2대의 컴퓨터가 동일한 IP주소를 가질 수는 없음
  * 그러나, 인터넷에 연결되지 않은 개인 네트워크는 사설 네트워크 내의 각 호스트가 고유한 경우 호스트 주소를 사용할 수 있음
  * RFC 1918은 개인, 내부용으로 3개의 IP주소 블럭을 따로 설정
  * 개인 주소를 사용하여 네트워크를 인터넷에 연결하려면 네트워크 주소변환(Network Address Translation, NAT)을 사용하여 개인 주소를 공용 주소로 변환해야 함
  * A Class는 어떤것이 사설주소인가? 알아야 됨!
  * 해당 그림은 표준으로 세워놓은 IP주소











### 5단원. 네트워크 계층: 제어 평면 (The Network Layer: Control Plane)

### 6단원. 링크 계층: 링크, 접속망, 랜(The Link Layer and LANs)
