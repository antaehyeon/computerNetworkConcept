  <!-- # Sejong Computer Network -->
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
  * 각 라우터의 개별 라우팅 알고리즘 구성요소는 Control Plane에서 상호작용

### 논리적으로 중앙 집중화 된 Control Plane
![Logically centeralized control plane](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-8.%20Logically%20centralized%20control%20plane.png)
* 고유한(일반적으로 원격) 컨트롤러가 로컬 제어 에이전트(control agents, CAs)와 상호작용


![네트워크 계층](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/network%20layer.png)

### 4-2. 라우터 내부에는 무엇이 있는가?
  * 교수님이 중요하지 않다고 한 부분은 제외되었습니다

### 이더넷 케이블 (UTP) - 어떻게 만드는가 (기말5점)
![4-22. Ethernet Cable (UTP)](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-22.%20Ethernet%20Cable%20(UTP).png)
  * 해당 라인 순서와 cross cable에 대한부분 숙지

### 라우터 외부 연결
![4-25. Router external connections](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/4-25.%20Router%20external%20connections.png)
  * Console Port : configuration 접속포트

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
  * DHCP 개요 (기말 매우 중요-DHCP 순서에 대한것을 물어볼 수 있음)
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

# 5단원. 네트워크 계층: 제어 평면 (The Network Layer: Control Plane)
  * 챕터 목표 : 네트워크 제어면의 원리 이해
  * 기존 라우팅 알고리즘
  * SDN 컨트롤러 관리
  * 인터넷 제어 메세지 프로토콜
  * 네트워크 관리

  * 그리고 인터넷에서의 그들의 즉각적인 이행
    * OSPF, BGP, OpenFlow, ODL 및 ONOS컨트롤러, ICMP, SNMP


 ## 5-1. introduction : 도입

 ## 네트워크계층 기능
  * 리콜 : 두개의 네트워크 계층 기능
    * [data plane]포워딩(forwarding) : 라우터의 입력에서 적절한 라우터의 출력으로 패킷 이동
    * [control plane]라우팅(routing) : 출발지에서 목적지까지 패킷에 의해 취해진 경로를 결정
  * 네트워크 제어 평면을 구조하하기위한 두 가지 접근법
    * 라우터 단위 제어(전통적)
    * 논리적으로 중앙화 된 제어 (소프트웨어 정의된 네트워킹)

  ## 라우터 단위 제어(Pre-router control plane)
  * 각 라우터의 개별 라우팅 알고리즘 구성요소가 제어평면에서 상호작용하여 전달 테이블을 계산
  * [챕터4 라우터별 제어계획 그림 참고](https://github.com/antaehyeon/computerNetworkConcept#라우터별-제어-계획per-router-control-plane)

  ## 논리적으로 중앙집중화 된 제어평면
  * 고유한 (일반적으로 원격) 컨트롤러는 라우터의 로컬제어 에이전트(Control agents, CAs)와 상호작용하여 전달 테이블을 계산
  * [챕터4 논리적으로 중앙집중화된 제어계획 그림참고](https://github.com/antaehyeon/computerNetworkConcept#논리적으로-중앙-집중화-된-control-plane)

  ## 5-2. 라우팅 프로토콜
  * 연결 상태
  * 거리 벡터

  ## 라우팅 프로토콜
  * 라우팅 프로토콜 목표 : 라우터의 네트워크를 통해 호스트를 수신 호스트에 이르기까지 "양호한(good)" 경로(동등한, 라우터)를 결정
  * 경로 : 라우터 패킷의 순서는 주어진 초기 출발지 호스트에서 지정된 최종 목적지 호스트로 이동하는 과정을 거침
  * "양호(good)" : 최소 비용, 가장 빠른, 최소 혼잡
  * 라우팅 : "TOP10" 네트워킹 대회!
  * 각각의 good 기준이 다른점을 파악
    * 서울에서 부산으로 갈때 라우팅 경로의 차이가 생길 수 있음

  ## 네트워크의 추상화 그래프
  * 그래프 추상화(graph abstraction)는 P2P와 같은 다른 네트워크 환경에서 유용하며, 여기서 N은 피어세트이고 E는 TCP연결 세트

  ## 그래프 추상화 : 비용
  * Q. u와 z 사이의 최소 비용 경로는 무엇입니까?
  * A. 라우팅 알고리즘(routing algorithm) : 최소 비용 경로를 찾는 알고리즘

  ## 라우팅 알고리즘 정의
  * Q. 글로벌 또는 분산화 정보?
    * 글로벌
      * 모든 라우터에는 완벽한 토플로지(topology), 링크 비용 정보가 있음
      * 링크 상태 알고리즘

    * 분산된 (decentralized)
      * 라우터는 물리적으로 연결된 이웃을 알고, 이웃과 비용을 연결
      * 반복적인 계산과정 및 이웃과의 정보 교환
      * 거리 벡터 알고리즘
  * Q. 정적 또는 동적?
    * 정적
      * 시간 흐름이 시간 경과에 따라서 천천히 변화
      * 경로가 빠르게 변화
        * 주기적인 갱신
        * 링크 비용 변화에 대응

  ## 5-3. 인터넷에서의 intra-AS 라우팅 OSPF(기말)


  ## 확장 가능한 라우팅 만들기
  * 모든 라우터가 동일 해야함
  * 네트워크 "flat" 실제로는 사실이 아님

  * scale : 수십억의 목적지를 가진
    * 라우팅 테이블에 모든 대상을 저장할 수 없음
    * 라우팅 테이블 교환은 링크가 될 것

  * 행정 차지(administrative autonomy)
    * 인터넷 = 네트워크의 네트워크
    * 각 네트워크 관리자는 자체 네트워크에서 라우팅을 제어할 수 있음

  ## 확장 가능한 라우팅에 대한 인터넷 접근 방식
  * 라우터를 "자율 시스템(autonomous system, AS, 도메인)"으로 알려진 영역으로 집합

  * intra-AS 라우팅
    * 호스트간 라우팅, 동일한 AS의 라우터
    * AS의 모든 라우터는 일부 도메인 내 프로토콜을 실행해야함
    * 다른 AS에 있는 라우터는 다른 도메인 내부 라우팅 프로토콜을 실행할 수 있음
    * 게이트웨이 라우터 : 자체 AS의 "가장자리"에는 다른 AS의 라우터에 대한 링크가 있음

  * inter-AS 라우팅
    * AS 사이의 라우팅
    * 게이트웨이는 도메인간 라우팅(intra-도메인 라우팅도 물론)

  ## 상호연결된 ASes
  ![5-15.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-15.png)
  * 인트라 및 AS간 라우팅 알고리즘으로 구성된 전달 테이블(forwarding table)
    * 내부 AS 라우팅은 AS 내 목적지에 대한 항목을 결정
    * 외부 목적지에 대한 AS 간 및 내부 AS 결정항목
    * 3개의 ASes를 LG, SK, KT라 가정하고 각각의 라우터에서 forwarding table 을 업데이트 하는 방식

  ## Inter-AS 작업
  ![5-16.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-16.png)
  * AS1 라우터가 AS1 외부로 향하는 데이터그램을 받았다 가정
  * 라우터는 게이트웨이 라우터로 패킷을 전달해야 하지만 어느 라우터를 사용해야 하는가?
  * AS1 라우터가 반드시 해야하는
    * AS3 를 통해 AS2 가 어느정도까지 도달할 수 있는지 익히기
    * AS1의 모든 라우터에 도달 가능성 정보를 전파(도달할 수 있는 정보를 가지고 있어야 함)
  * AS간 라우팅 작업

  ## Intra-AS 라우팅
  * 내부 게이트웨이 프로토콜(interior gateway protocols, IGP)이라고 함
  * 가장 일반적인 intra-AS 라우팅 프로토콜
    * RIP : 라우팅 정보 프로토콜 (기말-교수님 출제성향)
      * RIP는 5개? RIPv2는 250개?
    * OSPF : Open Shortest Path First(본질적으로 OSPF와 동일한 IS-IS 프로토콜)
      * 알고리즘 이름을 프로토콜 이름으로 정함
    * IGRP : Internet Gateway Routing Protocol (Cisco가 2016년까지 수십년간 독점적으로 운영)
    * **특정된 회사의 Protocol을 물어보기 보다는 공통적이고 관계적인 부분을 물어볼 예정**

  ## OSPF (Open Shortest Path First)
  * "open" : 공개적으로 이용가능한
  * 링크 상태 알고리즘
    * 링크 상태 패킷 보급
    * 각 노드의 topology 맵
    * 다익스트라 알고리즘을 이용한 경로 계산
  ## 라우터가 AS 전체의 다른 모든 라우터에 OSPF 링크 상태
  * **전체** AS에 있는 다른 라우터에게 라우터의 홍수 링크 상태 전파
    * TCP 또는 UDP 대신 IP를 통해 직접 OSPF 메세지 전송
    * 연결 상태 : 연결된 각 링크
  * IS-IS 라우팅 프로토콜 : OSPF와 거의 동일

  ## OSPF의 진보된 기능
  * 보안 : 인증된 모든 OSPF 메세지 (악의적인 침입을 막기위해)
  * 동일한 비용의 **여러** 경로가 허용 (RIP에서 단 하나의 경로만 허용)
  * 각 링크에 대해 서로 다른 TOS에 대한 여러 비용 metric (예 : 최선의 ToS에 대해서는 위성 링크비용 낮음, 실시간 ToS에 대해서는 높음)
  * 통합된 단일 및 다중 캐스트 지원
    * 멀티캐스트 OSPF (MOSPF)는 OSPF와 동일한 topology 데이터베이스를 사용
  * 대규모 도메인의 **계층적** OSPF

  ## Hierarchical OSPF (기말)
  ![5-20.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-20.png)
  * 2 수준 계층 구조 : 로컬 영역, 백본
    * 지역내에서만 링크상태 광고
    * 각 노드에는 상세한 영역 topology가 존재
    * 다른지역의 그물에 대한 방향(최단 경로)만 알 수 있음
  * 영역 경계 라우터 : 자신의 영역에서 네트워크까지의 거리를 "요약"하고 다른 영역 경계 라우터에 전파(advertise, 광고)
  * 백본 라우터 : 백본으로 제한된 OSPF 라우팅을 실행
  * 경계 라우터 : 다른 AS에 연결

  ## 5-4. routing among the ISPs : BGP (기말)
  * Internet inter-AS routing : BGP
  * Border Gateway Protocol, BGP : 사실상의 도메인간 라우팅 프로토콜
    * 인터넷을 연결하는 접착제
  * BGP는 각 AS를 다음과 같은 방법으로 제공
    * eBGP : 인접한 AS로부터 서브넷 반응성 정보를 얻음
    * iBGP : 모든 AS내부 라우터에 도달 가능성(reachability) 정보를 전파
    * 도달 가능성 정보 및 정책을 기반으로 다른 네트워크에 대한 "좋은(good)" 라우터(경로)를 결정
  * 서브넷이 인터넷의 나머지 부분에 자신의 존재를 알리는 것을 허용 (나 여기있다)
  * OGP, BGP 풀네임이나 eBGP 또는 iBGP 연습문제 참고

  ## eBGP, iBGP 연결
  ![5-24.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-24.gif)
  * eBGP인지, iBGP인지

  ## BGP basics
  ![5-25.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-25.gif)
  * BGP 세션 : 두개의 BGP 라우터(피어)가 반영구적인 TCP연결을 통해 BGP 메세지를 교환
    * 다른 목적지 네트워크 프리픽스 대한 광고 경로 (BGP는 경로벡터 프로토콜임)
  * AS3 게이트웨이 라우터 3a가 경로 AS3, X를 AS2 게이트웨이 라우터 2c에 알릴 때
    * AS3는 AS2에게 데이터그램을 X로 전달할 것을 약속

  ## 경로 속성 및 BGP 경로
  * 광고된 접두사(advertised prefix)에는 BGP속성이 포함
    * prefix + attributes = route
  * 두개의 중요한 속성
    * AS-PATH : 접두사 광고가 통과된 ASES 목록
    * NEXT-HOP : 다음과 같은 특정 내부-AS라우터를 다음 홉AS로 나타냄
  * 정책 기반 라우팅
    * 게이트웨이 수신경로 광고는 가져오기 정책(import policy)을 사용하여 accept/decline를 초과하는 경로를 사용 (예: AS Y를 통과하지 않음)
    * AS 정책은 또한 다른 인접한 AS에 대한 경로를 광고할지 여부를 결정
    * 예를들어 서울에서 부산으로 최고성능을 기반(직진)으로 가고싶다고 하자, 그러나 정책(policy)가 허용되지 않으면 무조건 직진할 수가 없음. 즉, Policy > 성능

  ## BGP 경로 광고(advertisement)
  ![5-27.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-27.gif)

  * AS2 라우터 2c는 AS3 라우터 3a에서 경로 알림 AS3, X (eBGP를 통해)를받습니다.
  * AS2 정책에 따라 AS2 라우터 2c는 경로 AS3을 수용합니다. X는 iBGP를 통해 모든 AS2 라우터로 전파됩니다
  * AS2 정책에 따라 AS2 라우터 2a는 AS2, AS3, X 경로를 ASB 라우터 1c에 알립니다 (eBGP를 통해)

  ![5-28.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-28.gif)
  * 게이트웨이 라우터는 대상 경로에 대한 다중 경로를 학습할 수 있음
    * AS1 게이트웨이 라우터 1c는 경로 AS2, AS3, X를 2a에서 확인
    * AS1 게이트웨이 라우터 1c는 경로 AS3, X를 3a에서 습득
    * 정책에 따라 AS1 게이트웨이 라우터 1c는 경로 AS3, X를 선택하고 AS1 내의 경로를 iBGP를 통해 알림

  ## BGP Message
  * TCP연결을 통해 피어간에 교환되는 BGP 메세지
  * BGP 메세지
    * OPEN : 원격 BGP 피어와 TCP 연결을 열고 BGP 피어의 송신을 인증
    * UPDATE : 새 경로를 알림 (또는 오래된 것을 철회)
    * KEEP ALIVE : UPDATE가 없을 때 연결을 유지 (또는 ACKs OPEN 요청)
    * NOTIFICATION : 이전 메세지의 오류를 보고 (또는 연결을 닫는데 사용)

  ## BGP, OSPF 전달 테이블 항목
  * 라우터는 전달 테이블 항목을 접두어(prefix)로 어떻게 설정합니까?
      ![5-30.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-30.gif)
  * recall : 1a, 1b, 1c iBGP를 통해 dest X에 대해 알아보기
  * 1c : "X 경로가 1c를 통과 함"

  ![5-30-1.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-30-1.png)
  * 1d : OSPF 내부 도메인(intra-domain) 라우팅 : 1c로 이동, 발신 로컬 인터페이스 1로 전달

  ![5-31.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-31.png)
  * 1a : OSPF 내부 도메인 라우팅 : 1c에 도달하고 발신 로컬 인터페이스 2로 전달

## BGP route selection
  * 라우터는 목적지 AS에 대한 하나 이상의 라우트에 대해 학습하고 다음에 기초하여 라우트를 선택
    1. 지역 특징 가치 속성(local preference value attribute) : 정책 결정
    2. 최단 AS-PATH
    3. 가장 가까운 NEXT-HOP 라우터 : hot potato(뜨거운 감자, 최대한 빨리 판단할 수 있는) 라우팅
    4. 추가 기준

## BGP : 광고를 통한 정책 수립
  ![5-33.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-33.png)
  * ISP가 고객 네트워크에서만 트래픽을 라우팅 하기만을 원한다고 가정 (다른 ISP간의 트래픽 이동을 원치 않음)
  * A는 경로 Aw를 B와 C에 알림
  * B가 BAw를 C에 광고하지 않기로 결정한 경우
    * C, A, w중 어느것도 B의 고객이 아니기 때문에 B는 라우팅 CBAw에 대해 "수익"을 얻지 못함
    * C는 CBAw 경로에 대해 알지 못함
  * C는 CAw를 사용하지 않도록 CAw(B를 사용하지 않음)를 라우팅함

  * A, B, C는 공급자 네트워크
  * X, W, Y는 고객 (공급자 네트워크의)
  * X는 이중 홈(dual-home) : 2개의 네트워크에 연결됨
  * 시행 할 정책 : X는 X를 통해 B에서 C로 라우팅하고 싶지 않음
    * 그래서 X는 B에게 C경로를 광고하지 않을 것

  ## 왜 intra-AS와 inter-AS 라우팅은 다른가?
  * 정책
    * inter-AS : 관리자는 트래픽이 라우팅되는 방식, 네트워크를 통해 라우팅되는 방식을 제어하려고 함
    * intra-AS : 단일 관리자, 정책 결정 필요 없음
  * 규모
    * 계층적 라우팅으로 테이블 크기를 줄이고 업데이트 트래픽을 줄임
  * 성능
    * inter-AS : 성능에 집중할 수 있음
    * intra-AS : 정책이 성능보다 우세함 (policy > performance)

 ## 5-5. SDN 제어 평면
  * 인터넷 네트워크 계층 : 역사적으로 분산형, 라우터 단위방식으로 구현
    * monolithic 라우터에는 전용 라우터 OS(IP, RIP, IS-IS, OSPF, BGP)의 독점적인 구현이 포함되어 있다(예 : Cisco OS)
      * monolithic : 일체로 되어있는, 이음매가 없는, IC등 직접회로의 반도체 기판이 한 장일 때
    * 다양한 네트워크 계층 기능을 위한 다양한 "미들박스" : 방화벽, 로드 밸런서, NAT 박스
      * flexible 하게 네트워크 계층 기능들을 SDN으로 구현할 수 있음
  * 2005년 : 네트워크 제어 재설정에 대한 새로워진 관심

  ## [Recall : 라우터별 제어 계획](https://github.com/antaehyeon/computerNetworkConcept#라우터별-제어-계획per-router-control-plane)

  ## [Recall : 논리적 중앙집중 제어계획](https://github.com/antaehyeon/computerNetworkConcept#논리적으로-중앙-집중화-된-control-plane)

  ## 소프트웨어 정의 네트워킹 (SDN)
  * 왜 논리적으로 중앙 집중식 제어 계획입니까?
    * 쉬운 네트워크 관리 : 라우터의 잘못된 설정을 방지하고, 트래픽 흐름의 유연성 향상
    * 분산형 프로그래밍 : 더 어려움 : 각 라우터에 구현된 분산 알고리즘(프로토콜)의 결과로 테이블 계산
  * Control Plane의 공개 (비 독점) 구현
  * Management 하기 쉽고 (단, 각각의 라우터마다 configuration을 진행해야 하는 단점)

  ## 교통 공학 : 어려운 전통적인 라우팅
  ![5-42.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-42.png)

  * Q : 네트워크 운영자가 u-to-z 트래픽이 uvwz, x-to-z 트래픽이 xwyz를 통과하도록하려면 어떻게해야합니까?
  * A : 트래픽 라우팅 알고리즘이 경로를 적절히 계산할 수 있도록 링크 가중치를 정의해야합니다 (또는 새 라우팅 알고리즘 필요)!
  * 링크 중량은 "knobs" 를 제어할 수 있습니다.

  ![5-43.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-43.png)
  * Q. 네트워크 운영자가 uvwz 및 uxyz (로드 밸런싱)를 따라 u-to-z 트래픽을 분할하려는 경우 어떻게해야합니까?
  * A. 할 수 없습니다(또는 새로운 라우팅 알고리즘이 필요함)

  ![5-44.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-44.png)
  * Q : w가 파란색과 빨간색 트래픽을 달리 다르게하려면 어떻게해야합니까?
  * A : 할 수 없습니다 (목적지 기반 포워딩 및 LS, DV 라우팅 사용)

  ## 소프트웨어 정의 네트워킹 (SDN)
  ![5-45.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-45.gif)
    1. 일반화 된 "플로우 기반"포워딩 (예 : OpenFlow)
    2. 제어, 데이터 평면(data plane) 분리
    3. 제어 평면(control plane)기능 - 데이터 전송 스위치의 외부기능
    4. 프로그램 가능한 제어 어플리케이션

  * 중앙 집중화된 Remote Controller
  * Control plane 과 Data Plane 으로 나뉘는 부분
  * software 적으로 flexible 하게 프로그래밍해서 한꺼번에 처리하게 할 수 있음 (장점)

  ## SDN 관점 : 데이터 평면(data plane) 스위치
  ![5-46.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-46.png)
  * 데이터 평면 스위치
    * 하드웨어에서 일반화된 데이터 평면 포워딩(4.4절)을 구현하는 빠르고 단순한 상품 스위치
    * 컨트롤러에 의해 계산된 스위치 흐름표
    * 테이블 기반 스위치 제어를 위한 API (예: OpenFlow)
      * 제어할 수 있는것과 그렇지 않은것을 정의
    * 컨트롤러(예 : OpenFlow)와 통신하기 위한 프로토콜
  * 종속적으로 분리되어 있음
  * Forwarding table이 배포가되면, 그것을 소프트웨어로 처리하는 부분이 상이함
  * SDN Controller에는 각각의 방법이 다름 (예 : OpenFlow : 표준을 사용-API)

  ## SDN 관점 : SDN 컨트롤러
  ![5-47.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-47.png)
  * SDN 컨트롤러 (네트워크 OS)
    * 네트워크 상태 정보를 유지
    * Northbound API를 통해 "위"의 네트워크 제어 응용 프로그램과 상호작용
    * Southbound API를 통해 "아래"의 네트워크 스위치와 상호작용
    * 성능, 확장성, 내결함성, 견고성을 위한 분산시스템으로 구현
  * 네트워크 정보를 관리하고 위, 아래와 상호작용 하는것(north, south)
  * Southbound API : 소프트웨어적으로 여러개를 병합하기 때문에 성능적으로 효율이 증가

  ## SDN 관점 : 애플리케이션 컨트롤
  ![5-48.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-48.png)
  * 네트워크-제어 앱
    * 두뇌 제어 : 하위 수준 서비스를 사용하여 제어 기능 구현, SDN 컨트롤러가 제공하는 API
    * 번들되지 않음 : 타사에서 제공할 수 있음 : 라우팅 공급업체 또는 SDN 컨트롤러와 별개
  * 계층화 구조를 채택해서 flexible 하게 구현
    * 성능은 좋아지면서 가격은 저렴하게 (API 형식으로 사용하기 때문에)

  ## SDN 컨트롤러의 구성 요소
  ![5-49.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-49.png)
  * 네트워크 제어 앱에 대한 인터페이스 레이어 : 추상화 API
  * 네트워크 전체 상태 관리 계층 : 네트워크 링크, 스위치, 서비스 상태 : 분산 데이터베이스 - State Management
  * 통신 레이어 : SDN 컨트롤러와 제어 스위치 간 통신
  * 각각의 계층으로 나눠져서 수행

  ## OpenFlow 프로토콜
  ![5-50.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-50.png)
  * 컨트롤러 간 동작
  * **메세지** 교환에 사용되는 TCP
    * 선택적 암호화
  * OpenFlow 메세지의 3가지 클래스
    * 컨트롤러 - 스위치
    * 비동기 (컨트롤러로 전환)
    * 대칭 (기타)

  ## OpenFlow : 컨트롤러에서 제어하는 메시지(controller-to-switch messages)
  ![5-51.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-51.png)
  * 주요 컨트롤러 - 스위치 메시지
    * 기능 : 컨트롤러 쿼리 기능 전환, 응답전환
    * 구성(configure) : 컨트롤러 쿼리 및 스위치 구성 변수 설정
    * 수정-상태 : OpenFlow 테이블에서 흐름 항목 추가, 삭제, 수정
    * packet-out : 컨트롤러는 이 패킷을 특정 스위치 포트에서 보낼 수 있음

  ## OpenFlow : 컨트롤러 간 메시지(switch-to-controller messages)
  * 중요한 부분 : 컨트롤러 간 메시지
    * packet-in : 패킷(및 그 제어)을 컨트롤러로 전송하며 컨트롤러로 부터 패킷출력 메세지를 관찰
    * 흐름 제거 : 스위치에서 삭제된 flow table 항목
    * 포트 상태 : 컨트롤러에 포트 변경을 알림
  * 다행하게도, 네트워크 운영자는 OpenFlow메시지를 직접 생성/전송하여 스위치를 프로그래밍하지 않습니다. 대신 컨트롤러에서 더 높은 수준의 추상화를 사용함

  ## SDN : 컨트롤 / 데이터 플레인 상호 작용 예제
  ![5-53.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-53.png)
    1. S1, OpenFlow 포트 상태 메시지를 사용하여 컨트롤러에게 링크 실패 알림을 보냄
    2. SDN 컨트롤러가 OpenFlow 메세지를 수신하고 링크 상태 정보를 업데이트
    3. 다익스트라 라우팅 알고리즘 응용 프로그램은 이전 상태가 변경될 때 호출되도록 등록
    4. 다익스트라의 라우팅 알고리즘 액세스 네트워크 그래프 정보, 컨트롤러의 링크 상태 정보, 새로운 경로를 계산
    5. 링크 상태 라우팅 앱은 SDN 컨트롤러의 플로우 애플리케이션 구성요소와 상호작용하여 필요한 새로운 흐름 표(flow table)를 계산합니다.
    6. 컨트롤러는 OpenFlow를 사용하여 업데이트가 필요한 스위치에 새 테이블에 설치합니다.

  ## SDN: 선택된 도전과제
  * 제어 평면 강화 : 신뢰할 수 있고 성능이 확장 가능하며 안전한 분산시스템
    * 실패에 대한 견고성(robustness) : 제어 평면에 대한 신뢰할 수 있는 분산 시스템의 강력한 이론 활용
    * 의존성, 보안 : 첫날부터 구운(baked)?
  * 미션 특정 요구사항을 충족하는 네트워크, 프로토콜
    * 예 : 실시간, 신뢰할 수 있는, 울트라 보안
  * 인터넷 스케일링(?)

  ## 5-6. ICMP : 인터넷 제어 메시지 프로토콜

  ## ICMP: internet control message protocol
  ![5-57.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-57.png)

  * 호스트 및 라우터가 네트워크 수준의 정보를 전달하는데 사용
    * 오류보고 : 연결할 수 없는 호스트, 네트워크, 포트, 프로토콜
    * 에코 요청/응답 (핑에 의해 사용)
  * IP위의 네트워크 계층
    * IP 데이터그램에서 전달되는 ICMP 메세지
  * ICMP 메시지 : 유형, 코드+첫번 째 8바이트의 IP 데이터그램이 오류를 발생

  ## 추적(Traceroute) 및 ICMP
  ![5-58.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-58.gif)
  * source는 일련의 UDP 세그먼트를 대상으로 보냄
    * 첫번째 세트는 TTL = 1
    * 두번째 세트는 TTL = 2
    * 가능성이 없는 포트번호
  * n 번째 세트의 데이터그램이 n 번째 라우터에 도착하면
    * 라우터가 데이터그램을 삭제하고 원본 ICMP 메시지(유형 11, 코드 0)
    * ICMP 메시지는 라우터 및 IP주소가 포함
  * ICMP 메세지가 도착하면 소스 레코드가 RTT를 기록
  * 정지 기준
    * UDP 세그먼트가 최종 호스트에 도착
    * 대상이 ICMP "포트연결 불가" 메시지를 반환(유형3, 코드3)
    * 소스 스톱

  ## 5-7. 네트워크 관리 및 SNMP (기말)
  * SNMP가 시험에 나올 수 있음..?

  ## 네트워크 관리는 무엇인가?
  * **자율시스템** (일명 네트워크) : 1000초 마다 상호작용하는 하드웨어/소프트웨어 구성요소
    * 규모의 차이가 있지만 수천개, 수십만개(구글, 마소 등)가 각각의 management 대상이 됨

  * 모니터링, 제어가 필요한 다른 복잡한 시스템
    * 제트 비행기
    * 원자력 발전소
    * 다른 것들?
    * IoT 대상들도 management 범주에 포함되고, 감시, 제어, 관리 (jet airplane, nuclear, ower plant, others 등 ?) 의 부류도 모두 관리대상
  > "네트워크 관리는 네트워크, 소프트웨어 및 인적 요소의 구현, 테스트, 평가, 구성, 평가, 구성, 분석, 평가 및 제어를 위해 네트워크 및 소자 리소스의 구축, 평가, 제어, 평가, 제어를 합리적인 비용으로 수행합니다."

  > 네트워크 관점에서 보면 monitor, test, poll, configure, analyze 등을 합리적인 가격으로 real-time, operational performance, and Quaility of Service의 요구사항을 만족하는 것이다.

  > QoS : Quality of service, 서비스의 품질 (bandwidth)
  >   SLA : SI업체, Ni업체에게 정부가 요구하는 서비스 품질(어느 정도의 서비스를 요구하는)

  ## 네트워크 관리를 위한 인프라
  ![5-61.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-61.png)

  * 관리 장치에는 데이터가 MIB (Management Information Base)로 수집되는 관리 대상 개체가 포함됩니다.

  * Managed device = host, sensor 등 대상이 점점 늘어남
  * Data Parameter를 가지고 관리
  * 용어들에 대한 정의를 명확히 해야 표준을 정할 수 있음
  * 그래서 용어를 물어보는 것(기말)

  ## SNMP 프로토콜
  * MIB정보, 명령을 전달하는 두가지 방법
      ![5-62.gif](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-62.gif)

  * Ondemand 방식 = request / response

  ## SNMP 프로토콜 : 메시지 타입
  ![5-63.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-63.png)

  ## SNMP 프로토콜 : 메세지 형식
  ![5-64.png](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/5-64.png)

  * SNMP 가 무엇이다 정도만 알면됨, 외울필요 없음
  * Protocol Data Unit, PDU

  ## Chapter 05 요약
  * 네트워크 제어평면에 접근
    * 라우터 단위 제어 (전통적)
    * 논리적으로 중앙화된 제어(소프트웨어 정의된 네트워킹)
  * 전통적인 라우팅 알고리즘
    * 인터넷에서 구현 : OSPF, BGP
  * SDN 컨트롤러
    * 실제로 구현 : ODL, ONOS
  * 인터넷 제어 메시지 프로토콜
  * 네트워크 관리(management)

## 6단원. 링크 계층: 링크, 접속망, 랜(The Link Layer and LANs)
* 목표
  * 링크 계층 서비스의 기본 원리 이해
    * 오류 검출 및 정정
    * broadcast 채널 공유 : 다중 접속
    * 링크 계층 주소 지정
    * 로컬 영역 네트워크 : 이더넷, VLAN
  * 인스턴스화, 다양한 링크계층 기술 구현
    * 인스턴스화 : 추상적인 것을 구체적인 예를 통해서 표현

## 6-1. introduction, services

## 링크 레이어 : 소개
* 전문 용어(집합적인, terminology)
  * 호스트 및 라우터 : **노드**
  * 통신 경로를 따라 인접 노드들을 연결하는 통신 채널들 : **링크들**
    * 유선 링크
    * 무선 링크
    * LAN
  * 계층 2 패킷 : **프레임**, 데이터 그램 캡슐화
  > **데이터 링크 계층**은 한 노드에서 링크를 통해 **물리적으로 인접**한 노드로 데이터 그램을 전송할 책임이 있습니다.



## 링크 레이어 : 내용

* 서로 다른 링크를 통해 서로 다른 링크 프로토콜에 의해 전송된 데이터그램
  * 예를들어, 제 1 링크상의 이더넷, 중간 링크상의 프레임 릴레이, 마지막 링크상의 802.11
* 각 링크 프로토콜은 서로 다른 서비스를 제공
  * 예를 들어, 링크를 통해 rdt를 제공할 수 있고 제공하지 않을 수도 있음
    * rdt : Real Data Transport
* **예시 : 교통에 비유**
  * 프린스턴(Princeton)에서 로잔(Lausanne)까지의 여행
    * 리무진 : 프린스턴 ~ JFK
    * 비행기 : JFK ~ 제네바
    * 기차 : 제네바에서 로젠까지
    * 관광객 = **데이터그램**
    * 전송 세그먼트 = **통신 링크**
    * 운송 모드 = **링크 계층 프로토콜**
    * 여행사 = **라우팅 알고리즘**  (agent가 어떤 구간을 통해서 갈 수 있는지 예약)



## 링크 레이어 서비스

* **프레이밍(framing), 링크 액세스**
  * 데이터 그램을 프레임에 캡슐화하고, 헤더 및 예고(trailer)에 추가
  * 공유매체인 경우 채널에 접근
  * 출발지, 목적지를 식별하기 위해 프레임 헤더에 사용되는 "MAC" 주소
    * Media Access Control, MAC
    * IP주소와는 다른
* **인접한 노드 사이의 안정적인 전달**
  * 우리는 이미 이것을 어떻게 하는지 배웠음(Chapter 03)
  * 거의 사용되지 않은 비트 오류 링크 (광섬유, 일부 꼬임 쌍)
  * 무선 링크 : 높은 오류율(상대적으로 많은 에러가 발생)
    * Q. 링크 수준과 End-End 안정성이 모두 중요한 이유는 무엇입니까?
* **흐름 제어 (Flow Control)**
  * 인접한 송신노드와 수신노드 사이의 속도조절(pacing)
* **오류 검출 (Error Dection)**
  * 신호 감쇄, 노이즈로 인한 오류
  * 수신기는 오류 유무를 감지
    * 재전송 또는 프레임 드롭 신호 발신자 ? 
    * signals sender for retransmission or drops frame
* **오류 수정 (Error correction)**
  * 수신기는 재전송에 의지하지 않고 비트 오류를 식별하고 **수정**
* **반이중 (half-duplex) 및 전이중 (full-duplex)**
  * 반이중으로 링크의 양쪽 끝에있는 노드는 전송할 수 있지만, 동시에 전송할 수는 없음



##  링크 계층은 어디에 구현됩니까?

![![6-8](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-8.gif)]

- 각 호스트마다
- "어댑터"(**네트워크 인터페이스 카드**, NIC) 또는 칩(주로 메인보드에 같이 구현)에 구현된 링크 계층
  - 이더넷 카드, 802.11 카드; 이더넷 칩셋
  - 링크, 물리계층 구현
- 호스트의 시스템 버스에 연결
- 하드웨어, 소프트웨어, 펌웨어의 조합



## 통신 어댑터

![6-9](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-9.png)

- 보내는 쪽
  - 프레임에 데이터그램 캡슐화
  - 오류검사비트, rdt, 흐름제어 등을 추가
- 받는 쪽
  - 오류, rdt, 흐름제어 등을 찾음 (만약 발견하면 해당 데이터를 모두 버림)
  - 데이터그램 추출, 수신측 상위계층 통과



## 6-2. 오류 검출 및 정정

## 오류 검출

![6-11](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-11.png)

- EDC = 오류감지 및 수정비트 (중복성)
- D = 오류검사로 보호되는 데이터는 헤더 필드를 포함할 수 있음
- 100% 신뢰할 수 없는 오류감지!
  - 프로토콜이 약간의 오차를 발생시킬 수 있지만 드물다
  - EDC가 커지면 검출 및 보정이 향상



## Parity 검사

- single bit parity : 단일 비트 오류 감지
- two-dimensional bit parity : 2차원 비트 패리티 (column, row parity)



## 인터넷 checksum (review)

- 목표 : 전송 패킷에서 "오류" (예: 플립된 비트)를 감지 (예: 전송계층에서만 사용)
- 보내는 사람
  - 세그먼트 내용을 16비트 정수로 처리
  - 체크섬 : 세그먼트의 내용 더하기 (1의 보수 합)
  - 보낸 사람이 체크섬 값을 UDP 체크섬 필드에 추가
- 받는 사람
  - 수신 세그먼트의 체크섬 계산
  - 계산된 체크섬이 체크섬 필드값과 같은지 확인
    - 예 : 오류가 발견되지 않았지만, 그럼에도 불구하고 오류일 수 있습니까?
    - 아니오 : 오류 감지



## 순환 중복 검사

- Cyclic redundancy check, CRC



## 순환 중복 검사 예시

- 6-15



## 6-3. 다중 접근 프로토콜

## 다중 액세스 링크, 프로토콜

- 강의하는 곳처럼 여러 수업이 한 강의실에서 진행되는 것 또는 한 컴퓨터를 여러 사람이 같이 사용하는 것
  - 이러한 부분에서 충돌이 날 수 있으므로 충돌회피기법이 존재
  - 초창기 - shared Wire
    - 하나의 동축케이블을 이용해서 공유
    - 속도도 느리고 실시간에 적합하지 못했지만
    - 스위치 덕분에 살아남, 가격도 저렴
- 두가지 유형의 "링크"
  - point-to-point
    - 전화 접속 액세스용 PPP
    - 이더넷 스위치, 호스트 간 point-to-point
  - **broadcast (공유된 유선 또는 매체)**
    - 구식 이더넷
    - upstream HFC
    - 802.11 무선 LAN
- 단일 공유 broadcast 채널
- 노드에 의한 2개 이상의 동시전송 : 간섭
  - 노드가 2개 이상의 신호를 동시에 수신하면 **충돌(collision)**
- **다중 접속 프로토콜**
  - 노드가 채널을 공유하는 방식을 결정하는 분산 알고리즘
  - 즉, 노드가 언제 전송할 수 있는지 결정
  - 채널 공유에 대한 커뮤니케이션은 채널 자체를 이용
    - 조정을 위한 대역 외 채널은 존재하지 않음



## 이상적인 다중 접속 프로토콜

- given : R bps 속도의 broadcast 채널
- 필요한 것 (desiderata)
  1. 하나의 노드가 전송하기를 원할 때, 그것은 속도(rate) R로 전송할 수 있다
  2. M개의 노드가 전송하기를 원할 때, 각각의 평균 비율로 전송할 수 있다 **(R/M)**
  3. 완전히 분산된
     - 전송 조정을 위한 특별한 노드가 존재하지 않음
     - 클록 슬롯의 단순한 동기화 없음
  4. 단순한



## MAC 프로토콜 : 분류법(taxonomy)

- 3가지 broad 클래스들
  - 채널 분할(파티셔닝, partitioning)
    - 채널을 더 작은 '조각' (타임슬롯, 주파수, 코드) 으로 나눔
    - 배타적(독점적) 사용을 위해 조각을 노드에 할당
  - 랜덤 액세스
    - 분할되지 않은 채널, 충돌 허용
    - 충돌로부터 회복
  - 번갈아가며
    - 노드가 회전하지만 더 많은 전송이 필요한 노드가 더 오래 걸릴 수 있음



## 채널 분할 MAC 프로토콜 : TDMA

![6-21](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-21.png)

- TDMA : 시분할 다중 접속 (Time Division Multiple Access)
  - '원형'에서의 채널접근
  - 각 역(station)은 각 라운드에서 고정길이슬롯(길이=패킷전송시간)을 갖는다
  - 사용되지 않은 슬롯은 유휴 상태
  - 예 : 6-스테이션 LAN, 1,3,4 패킷 전송, 슬롯 2,5,6 유휴



## 채널 분할 MAC 프로토콜 : FDMA

![6-22](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-22.png)

- FDMA : 주파수 분할 다중 접속 (Frequency Division Multiple Access)
  - 주파수 대역으로 분할된 채널 스펙트럼
  - 각 국은 고정 주파수 대역을 할당받음
  - 주파수 대역에서 사용되지 않은 전송시간은 유휴 상태가 됨
  - 예 : 6-스테이션 LAN, 1,3,4 패킷전송, 주파수대역 2,5,6 유휴



## 랜덤 접근 프로토콜

- 사전에 coordination(조정) 하는것은 없고, 아무때나 보내고 싶을 때 보냄
- 노드가 보낼 패킷이 있을 때
  - 풀 채널 데이터 속도 R로 송신
  - 노드 사이의 선천적인(priori ?) 조정이 이루어지지 않음
- 2개 이상의 전송노드 = 충돌(collision)
- **랜덤 액세스 MAC 프로토콜**은 다음을 지정합니다
  - 충돌을 감지하는 방법
  - 충돌로부터 복구하는 방법(예를 들어, 지연된 재전송을 통해)
- 랜덤 액세스 MAC 프로토콜의 예
  - 슬롯 형 ALOHA
  - ALOHA
  - CSMA, CSMA/CD, CSMA/CA



## 슬롯이 있는 ALOHA

- 가정
  - 모든 프레임이 같은 크기
  - 동일한 크기의 슬롯으로 분할된 시간 (1 프레임 전송시간)
  - 노드는 슬롯 시작부분만 전송하기 시작
  - 노드 동기화
  - 2개 이상의 노드가 슬롯에서 전송하면 모든 노드가 충돌을 감지
- 기능(operation)
  - 노드가 새로운 프레임을 획득할 때, 다음 슬롯에서 전송
    - 충돌이 없다면 : 노드는 다음 슬롯에서 새로운 프레임을 전송할 수 있음
    - 충돌이 있다면 : 각 후속 슬롯에서 prob-up을 사용하여 **노드 재전송** 프레임을 반환 (성공할 때 까지)

![6-25](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-25.png)

- 장점
  - 단일 활동 노드는 채널의 최대속도를 통해 연속적으로 보낼 수 있음
  - 분산된 노드 : 노드의 슬롯만 동기화
  - 간단함
- 단점
  - 충돌, 슬롯을 소모
  - 유휴 슬롯
  - 노드는 패킷을 전송할 시간보다 적게 충돌을 감지할 수 있음
  - 클럭(clock) 동기화
- 충돌(Collision) 및 empty일 경우 해당 슬롯을 전부 비워버리기 때문에 Channel 효율성 측면에서 좋지 않음



## Slotted ALOHA : 효율성

> 효율 : 성공적인 슬롯의 장기적인 실행 (많은 노드, 모두 많은 프레임을 보낼 수 있음)

- 가정 : N개의 노드는 많은 프레임을 보내고, 각각 성공할 확률은 P
- 주어진 노드가 슬롯에서 성공했다는 prob = p(1-p)^(N-1)
- 모든 노드가 성공 =  Np(1-p)^(N-1)
- 최대 효율 : 최대화하는 p*를 구함 Np(1-p)^(N-1)
- 많은 노드에서, N이 무한대로 갈 때 Np*(1-p^star)^(N-1) 의 한계를 취하면, **최대효율 1/e = .37**

> 기껏해야 : 유용 전송에 사용되는 채널 시간의 약 37%



## 순수(슬롯 없음) ALOHA

![6-27](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-27.png)

- Unslotted ALOHA : 단순, 동기화 없음
- 프레임이 처음 드랍될 때
  - 즉시 전송
- 충돌 확률이 증가
- t0에서 전송된 프레임은 [t0-1, t0+1]에서 전송된 다른 프레임과 충돌



## CSMA (Carrier Sense Multiple Access)

- CSMA : 전송 전에 듣기
- 채널 감지 유휴 : 전체 프레임 전송
  - 만약 채널이 사용중임을 감지하면 전송을 지연시킨다
  - 인간 분석(analogy) : 다른 것들을 방해하지 말것



## CSMA 충돌(collision)

![6-30](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-30.png)

- 충돌은 여전히 발생할 수 있음** : 전파 지연은 두 노드가 서로의 전송물들을 수없이 의미
- **충돌** : 전체 패킷 및 전송 시간 낭비
  - 거리 및 전파 지연(propagation delay)이 충돌 확률을 결정하는 역할을 함

## CSMA/CD (충돌 감지)

![6-32](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-32.png)

- CSMA/CD : 캐리어 감지, CSMA와 같은 지연
  - 단시간 내에 충돌이 감지됨
  - 충돌 전송이 중단되어 채널 낭비를 줄임
- 충돌 감지
  - 유선 LAN에서 쉽게 : 신호강도측정, 전송된 수신신호 비교
  - 무선  LAN에서 어려움 : 수신 된 신호 강도가 로컬 전송 강도에 의해 압도됨
- 인간 분석(analogy) : 공손한 대화 예술가




## 이더넷 CSMA/CD 알고리즘

1. NIC는 네트워크 계층에서 데이터그램을 받아 프레임을 생성
2. NIC가 채널 유휴를 감지하면, 프레임 전송을 시작하고 NIC가 사용중인 채널을 감지하면 채널이 유휴상태가 될때까지 기다린다음 전송
3. NIC가 다른 전송을 감지하지 않고 전체 프레임을 전송할 경우 NIC가 프레임으로 이루어짐
4. NIC가 전송신호를 전송하는 동안 다른 전송을 감지하는 경우, 중단하고 신호를 전송
5. 중단 후, NIC는 **이진수(지수)백업**을 시작
   - 중단 후 NIC는 K (0,1,2, … , 2^m-1) 에서 무작위로 선택하고 NIC가 K*512 bit 동안 대기 후 2단계로 리턴
   - 더 많은 충돌이 발생한다면 더 긴 백업 간격을 가짐

- 이더넷에서 백업을 하는 부분이 알고리즘으로 구현되어 있음



## CSMA/CD 장점(기말)

- T-prop = LAN의 2 노드 간 최대 지연시간
-  t-trans = 최대 크기의 프레임 전송시간
- 효율성은 1로
  - t-prop가 0이 될때
  - t-trans가 무한대로 이동함에 따라
- **ALOHA보다 우수한 성능을 제공, 간단하고 저렴하며 분산되어있음**



## 교대(Taking turns) MAC 프로토콜

- 채널 파티셔닝(partitioning) MAC 프로토콜
  - 고부하에서 채널을 효율적이고 공평하게 공유
  - 낮은 부하에서 비효율적 : 채널 액세스 지연, 1개의 활성노드만 할당된 1/N 대역폭
- 랜덤 액세스 MAC 프로토콜
  - 낮은 부하에서 효율적 : 단일 노드가 채널을 최대한 활용
  - 높은 로드 : 충돌 오버 헤드
    - 많은 충돌이 일어나므로 Backup을 진행하는 횟수가 증가하여 실제로 보내는 데이터가 적음
- 교대(taking turns) 프로토콜
  - 두 세계의 최고를 찾으십시오!

![6-36](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-36.gif)

- 폴링(palling) - 순서대로 보내주는 것
  - 마스터 노드는 슬레이브 노드가 차례대로 전송하도록 '초대(invite)'함
  - 일반적으로 '멍청한(dumb)' 슬레이브는 장치와 함께 사용됨
  - 우려사항(concerns)
    - 폴링 오버헤드
    - 지연
    - 단일 장애 지점(마스터)

![6-37](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-37.gif)

- 토큰 전달 - 순서를 가지고 token으로 passing 하는 방법 (Token이 돌면서 passing 하거나 data를 전송하거나)
  - 제어 토큰은 한 노드에서 다음 노드로 순차전달을 진행
  - 토큰 메시지
  - 우려 사항
    - 토큰 오버헤드
    - 지연
    - 단일 장애 지점(토큰)



## 케이블 접근 네트워크

![6-38](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-38.gif)

- **다중** 40Mbps 다운 스트림(broadcast) 채널
  - 단일 CMTS(Cable Modem Termination System) 가 채널로 전송
- **여러개**의 30Mbps 업스트림 채널
  - **다중 액세스** : 모든 사용자가 특정 업스트림 채널 시간 슬롯(다른 채널 할당)

![6-39](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-39.png)

- **DOCSIS** : 케이블 서비스 인터페이스 명세
- 업스트림, 다운스트림 주파수 채널을 통한 FDM
- TDM 업스트림 : 일부 슬롯은 할당되고 일부 슬롯은 경합이 있음
  - 다운스트림 MAP 프레임 : 업스트림 슬롯 할당
  - 선택된 슬롯에서 업스트림 슬롯(및 데이터) 전송 랜덤 액세스 (바이너리 백오프) 요청



## MAC 프로토콜 요약

- 시간, 주파수 또는 코드에 의한 **채널 파티셔닝**
  - 시간 분할, 주파수 분할
- 무작위 액세스 (동적)
  - ALOHA, S-ALOHA, CSMA, CSMA/CD
  - 캐리어 감지 : 일부 기술(유선), 다른 기술(무선)
  - CSMA/CD 는 이더넷을 사용
  - CSMA/CA 는 802.11 사용
- 교대로
  - 중앙 사이트에서 폴링, 토큰 전달
  - 블루투스, FDDI(Fiber Distributed Data Interface) , 토큰 링



## 6.4 LANs - 주소지정, ARP



## MAC 주소 그리고 ARP

- 32비트 IP 주소
  - 인터페이스를 위한 네트워크 레이어 주소
  - 계층 3 (네트워크 계층) 전달에 사용
- MAC (또는 LAN 또는 물리적 또는 이더넷) 주소
  - 기능 : **하나의 인터페이스에서 다른 물리적으로 연결된 인터페이스로 프레임을 가져오기위해 '로컬'로 사용됨**
    **(IP 주소 지정 의미에서 동일한 네트워크)**
  - NIC ROM에서 48비트 MAC주소(대부분의 LAN용)가 구워짐(burned)
  - 때때로 소프트웨어 설정이 가능
- 1A-2F-BB-76-09-AD
  - 16진법 (기수16) 표기법, 각각의 숫자는 4비트를 나타냄



## LAN 주소 그리고 ARP

![6-43](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/6-43.png)

- LAN 상의 각 어댑터에는 고유한 LAN주소가 있음



## LAN 주소 (more)

- IEEE(Institute of Electrical and Electronics Engineers)에서 관리하는 MAC주소 할당
- 제조업체가 MAC 주소 공간의 일부를 구입 (고유성을 보장하기 위해)
- 유추(analogy)
  - MAC 주소 : 사회 보장 번호 (Social Security Number) 와 같음 (주민등록번호와 같음)
  - IP 주소 : 우편 주소 (서브넷 마스크에 의해서 변경 될 수 있음)
- MAC 플랫 주소 - 이식성 (portability)
  - LAN카드를 한 LAN에서 다른 LAN으로 이동할 수 있음
- 휴대용 IP 계층 주소
  - 주소는 노드가 연결된  IP 서브넷에 따름







