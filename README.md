# Sejong Computer Network
##세종대학교 김영복 교수님 컴퓨터 네트워크 기말 정리본 입니다 (PPT 기반, 모르는 내용은 책으로 보충)

### 4단원. 네트워크 계층 (The Network Layer: Data Plane)

목표
: 네트워크 계층이 호스트 사이의 통신 서비스를 어떻게 통과하는지

#### 4-1. 네트워크 계층 개요

- 데이터 플랜에 초점을 맞춘 네트워크 계층서비스의 원리 이해
  * network layer 서비스 모델
  * 포워딩 대 라우팅
  * 라우터 작동방법
  * 일반 포워딩
- 인스턴스화, 인터넷에서 구현  

#### 네트워크 레이어
- 전송 구간에서 수신 호스트로의 전송 구간
- 송신측에서 세그먼트를 데이터그램으로 캡슐화
- 수신측에서 세그먼트를 전송계층에 전달
- **모든** 호스트, 라우터의 네트워크 계층 프로토콜
- 라우터는 통과하는 모든 IP 데이터 그램의 **헤더 필드를 검사**



1. Data Plane
2. Control Plane
![네트워크 계층](https://github.com/antaehyeon/computerNetworkConcept/blob/master/image/network%20layer.png)




### 5단원. 네트워크 계층: 제어 평면 (The Network Layer: Control Plane)

### 6단원. 링크 계층: 링크, 접속망, 랜(The Link Layer and LANs)
