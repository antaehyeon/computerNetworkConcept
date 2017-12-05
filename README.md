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

  ## IP addressing : CIDR
  ![4-43. IP addressing CIDR.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-43.%20IP%20addressing%20CIDR.png)
  * CIDR : Classless InterDomain Routing - 클래스 없는 InterDomain 라우팅
    * 임의의 길이의 서브넷 부분 주소
    * 주소 형식 : a,b,c,d/x (여기서 x는 주소의 서브넷 부분에 있는 # 비트)
  * 해당 /숫자 에 대한 표기 잘 알아두기
  * 위의 사진은 23비트 [111111111][11111111][111111110][000000000] = 255.255.254.0


## IP address : 어떻게 얻는가
  * 호스트에서 IP주소를 가져오는 방법은 무엇입니까?
    * 파일에서 시스템 관리자가 하드코딩
    * DHCP : Dynamic Host configuration Protocol : 서버에서 동적으로 주소 가져오기 (plug-and-play)
      * 자동으로 설정을 했을 때 DHCP를 통해서 서버로부터 받아서 Plug-and-play방식으로 설정

## DHCP: Dynamic Host Configuration Protocol
  * 목표 : 호스트가 네트워크에 가입할 때 네트워크 서버에서 IP주소를 동적으로 가져올 수 있음
    * 사용중인 주소로 임대 계약을 갱신할 수 있음
    * 주소를 재사용 할 수 있음(예: 연결된 상태일 때만 유지)
    * 네트워크 가입을 원하는 모바일 사용자 지원(보다 빠르게)
  * DHCP 개요 (개중요-DHCP 순서에 대한것을 물어볼 수 있음)
    * 호스트에서 DHCP 검색, discover메세지를 선택(옵션)
    * DHCP서버가 DHCP 제공, offer메시지로 응답
    * 호스트가 DHCP 요청, request메세지에 IP주소를 담아 응답
    * DHCP서버가 DHCP 응답, ack메시지에 담아 주소를 보냄
  * DHCP순서에 대한 것을 물어볼 수 있음
  * 왜 요청하고 ack를 보내는가
  * DHCP가 서버를 여러개 가질 수 있음
  * 그러면 IP를 여러개 받음
  * request가 왜 의미를 가지는지

## DHCP client-server scenario
![4-46. DHCP client-server scenario](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-46.%20DHCP%20client-server%20scenario.png)

![4-47. DHCP client-server scenario.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-47.%20DHCP%20client-server%20scenario.gif)

## DHCP: 더 많은 IP주소
  * DHCP는 서브넷에 할당된 IP주소 이상을 반환할 수 있음
    * 클라이언트의 첫번째 홉 라우터 주소
    * DNS서버의 이름 및 IP주소
    * 네트워크 마스크(주소의 네트워크 대 호스트 부분)

## DHCP: 예시
  ![4-50. DHCP example.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-50.%20DHCP%20example.gif)
  * 노트북을 연결하려면 IP주소, 첫번째 홉 라우터 주소, DNS 서버주소를 입력하고 DHCP를 사용함
  * UDP 에서의 DHCP 캡슐화 요청
  * IP 에서의 캡슐화
  * 802.11 Ethernet 에서의 캡슐화
  * DHCP서버를 실행하는 라우터에서 수신된 LAN상의 이더넷 프레임 브로드캐스트(목적지 : FFFF FFFF FFFF)
  * IP 역 다중화 된 이더넷, DHCP로 UDP역 다중화된 이더넷
  * DCP 서버는 클라이언트의 IP주소, 클라이언트의 첫번째 홉 라우터의 IP주소, DNS서버의 이름 및 IP주소를 포함하는 DHCP ACK를 공식화
  * DHCP 서버의 캡슐화, 클라이언트에 전달 된 프레임, 클라이언트에서 DHCP로의 최대화
  * 클라이언트는 IP주소, DNS서버의 이름 및 IP주소, 라우터 첫번째 홉의 IP주소를 알 수 있음

## IP 주소 : 어떻게 얻을 수 있는가? (연습문제 중요)
![4-51. ip addresses how to get one.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-51.%20ip%20addresses%20how%20to%20get%20one.png)
  * 네트워크가 IP주소의 서브넷 부분을 가져오는 방법은 무엇입니까?
  * 공급자 ISP주소의 일부를 할당
  * 어떤 Class인지 (A 클래스, B 클래스)
  * 3구역을 보면서 확인함 (각자 나눠주는 부분이 달라짐)
  * 2^9 bit 컴퓨터들에게 assign 할 수 있는 부분
  * ISP's block 11001000 00010111 00010000 00000000 200.23.16.0/20 수정

## IP addressing : 마지막 단어
  * ISP는 어떻게 주소를 차단하는가?
  * ICANN : Internet Corporation for Assigned
    * 주소 할당
    * DNS 관리
    * 도메인 이름 할당, 분쟁 해결

## NAT : network address translation
![4-55. NAT.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-55.%20NAT.png)

* 로컬 네트워크를 떠나는 모든 데이터그램에는 동일한 단일 소스 NAT IP주소가 있음 (138.76.29.7, 다른 소스 포트번호)
* 해당 네트워크에서 출발지 또는 목적지가 있는 데이터그램은 출발지,도착지에 대해서 10.0.0/24 주소를 가짐
* Public(왼쪽) - Private(오른쪽) 전환을 NAT가 담당
* 맨 오른쪽 (10.0.0.1~3) 은 Private 주소

* motivation : 로컬네트워크는 외부세계에 관한 하나의 IP주소만 사용
  * ISP에서 필요하지 않은 주소 범위 : 모든 장치에 대해 하나의 IP 주소
  * 외부 세계에 알리지 않고 로컬 네트워크에 있는 장치의 주소를 변경할 수 있음
  * 로컬 네트워크의 장치 주소를 변경하지 않고 ISP를 변경할 수 있음
  * 명시적으로 주소를 지정할 수 없는 로컬 네트워크 내부장치, 외부에서 볼 수 없음(보안적)
  * 한개의 외부 IP로 여러대의 장치를 이용할 수 있어 IP 부족현상에 대해 도움
  * 외부 IP가 변경되어도, 내부의 Private IP는 변경되지 않음

* implementation : NAT 라우터는 반드시
  * 나가는 datagram : 나가는 데이터그램의 (출발지 IP주소, 포트번호)를 (NAT IP 주소, 새 포트번호)로 바꾸면 원격 클라이언트/서버는 (NAT IP주소, 새 포트번호)를 목적지주소로 사용하여 응답                                                                                                                                                                     
  * 모든 (출발지 IP주소, 포트번호#)에서 (NAT IP주소, 새 포트번호) 변환 쌍(NAT 변환표에서)을 기억
  * 들어오는 데이터그램 : 모든 수신 데이터그램의 목적지 필드를 NAT테이블에 상응하는(출발지 IP주소, 포트번호)로 대체(NAT IP주소, 새 포트번호)

  ![4-58.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-58.gif)

* 16비트 포트번호 필드
  단일 LAN측 주소로 60,000개의 동시연결
  속도가 느리지만 IP부족현상을 매우 완화시키기 때문에 사용
* NAT는 논쟁의 여지가 있음
  * 라우터는 3계층까지만 처리
  * 주소부족은 IPv6에 의해 해결되어야함
  * 종단간 논쟁을 위반
    * 앱 디자이너가 (예: P2P 애플리케이션) NAT가능성을 고려
  * NAT traversal : 클라이언트가 NAT 뒷단 서버에 연결하려면 어떻게 해야합니까?

  ## IPv6 : motivation(동기, 자극, 유도)
  * 초기 동기 부여 : 32비트 주소공간이 곧 할당될 예정
  * 추가 동기
    * 헤더 포맷이 빠르게 처리/포워딩 되는데 도움
    * QoS를 용이하게 하기위한 변경

  * IPv6 데이터그램 형식
    * 40 바이트 헤더 고정길이
    * 파편화 불가

  * IPv6 데이터그램 포맷 (매우중요-기말1문제)
  ![4-62.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-62.png)
    * 우선순위 : Flow에서 데이터 그램간의 우선순위 식별
    * 흐름 레이블 : 동일한 Flow의 데이터 그램 식별
    * 다음 헤더 : 데이터의 상위 계층 프로토콜 식별
    * source, destination address가 128bit 인 부분 (32byte = 8/8/8/8)

  * IPv4의 기타 변경 사항
    ![4-64.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-64.gif)
    * checksum : 각 홉(hop)에서 처리시간을 줄이기 위해 완전히 제거
    * 옵션 : 허용되었지만 헤더 외부 및 다음 헤더필드로 표시
    * ICMPv6 : 새로운 버전의 ICMPv6
      * 추가 메세지 유형 (예. 너무 큰 패킷)
        * 패킷이 너무 큰 경우 ICMP프로토콜을 거쳐 사이즈를 조절 후 재전송
      * 멀티캐스트 그룹관리 기능

    * IPv4에서 IPv6로 전환
      * no 'Flag days'
      * 네트워크가 IPv4 및 IPv6 혼합 라우터와 어떻게 작동합니까?
    * **터널링(tunneling)** : IPv4 라우터간에 IPv4 데이터 그램에서 페이로드로 전달되는 IPv6 데이터 그램

  ## 터널링
  ![4-66.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-66.gif)

  ## IPv6 : 양자(adoption)
  * 구글 : 8%의 고객이 IPv6를 통해 서비스에 액세스
  * NIST : 모든 미국 정부 도메인 중 1/3은 IPv6 가능
  * 장기간 시간 동안 배치 및 사용
    * 20년간 애플리케이션의 수준 변화 (Facebook, skype, 스트리밍 미디어 등)

## 4-4 일반화된 전달 및 SDN (Generalized Forward and SDN)
![4-69.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-69.png)
  * 경기, 시합(match)
  * 활동 (action)
  * 실행중인 동작에 대한 오픈소스 사례

  ## 일반화된 전달 및 SDN (Generalized Forward and SDN)
  * 각 라우터는 논리적으로 중앙집중화된 라우팅 컨트롤러에 의해서 계산되고 분배되는 **플로우 테이블** 을 포함

## 개방형 흐름 데이터 평면 추상화
![4-70.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-70.png)
  * flow : 헤더필드에 의해 정의
  * 일반화된 포워딩 : 간단한 패킷 처리 규칙
    * 패턴 : 패킷 헤더필드의 값을 일치시킴
    * 일치하는 패킷의 경우 활동 : drop, forward, modify, (send) match packet
    * 우선순위 : 중복된 패턴을 분리 / 겹치는 패턴의 모호성을 없앰
    * 카운터 : 바이트# 그리고 패킷#
  * 라우터의 플로우 테이블 (컨트롤러에 의해 계산되고 분배 됨) 은 라우터의 match+action 룰을 정의

## OpenFlow : Flow Table 항목
![4-72.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-72.png)

## example
![4-73.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-73.png)

  * [ACTION] IP주소가 51.6.0.8이면 port 6 으로 보냄
  * [FORWARD] TCP 포트 22 로 향하는 모든 데이터그램을 전달(차단) X
  * [FORWARD] 호스트 128.119.1.1 이 보낸 몯든 데이터 그램을 전달(차단) X
  * [ACTION] MAC 주소(22:A7:23:II:EI:02)로 부터의 레이어 2 프레임

## OpenFlow 추상화(abstraction)
  * match+action : 서로 다른 종류의 장치를 통합
  * Router
    * match : 가장 긴 목적지 IP prefix
    * action : 링크 전송
  * Switch
    * match : 대상 MAC 주소
    * action : 전달 또는 홍수
  * Firewall
    * match : IP주소 및 TCP/UDP 포트번호
    * action : 허락 또는 거절
  * NAT
    * match : IP 주소 및 포트
    * action : 주소 및 포트 다시쓰기(rewrite)
  * 서로 다른종류의 네트워크장비를 만들 수 있음

## OpenFlow 예제
  * Example : 호스트 H5 및 H6의 데이터그램을 SI를 통해 H3 또는 H4로 보내야하며 거기에서 S2까지 보내야합니다.
![4-76.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-76.png)

## Chapter 4 : 완료!
  * Q. 어떻게 전달 테이블 (대상 기반 전달) 또는 흐름 테이블 (일반 전달) 계산합니까?
  * A. control plane (다음 챕터)



### 5단원. 네트워크 계층: 제어 평면 (The Network Layer: Control Plane)

### 6단원. 링크 계층: 링크, 접속망, 랜(The Link Layer and LANs)
