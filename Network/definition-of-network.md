# Network 정의

## Network란?
: 컴퓨터 들이 통신 기술 이용하여 그물망 처럼 연결된 통신 이용 형태를 의미

## Network 종류
#### 1. PAN (Personal Area Network)
- 가장 작은 규모의 네트워크
- IEEE 802.15
- ex) Bluetooth

#### 2. LAN (Local Area Network)
- 근거리 네트워크
- IEEE 802.11
- 이더넷(Ethernet) 프로토콜 사용

#### 3. MAN (Metropolitan Area Network)
- 대도시 영역 네트워크
- 표준 : **DQDB(Distributed Queue Dual Bus)** 토폴로지 기법 규정 (IEEE 802.6)
- fixed WIMAX

#### 4. WAN (Wide Area Network)
- 광대역 네트워크 = 원거리 통신망 ↔ 근거리통신망
- 전용선과 교환회선 방식으로 두 종류로 구분함

## DQDB란?
- Distributed Queue Dual Bus의 약어로, IEEE에서 제안된 기술
- E1(2.048[Mbps])에서 STM-1(155.520[Mbps])까지의 전송속도
- 회선교환 및 패킷교환 서비스 모두 제공
-이중 버스 토폴로지를 사용하며, 각 버스는 단방향이다.
- 버스의 머리(Head) 부분 에는 53바이트의 슬롯을 주기적으로 생성하는 슬롯 생성기(Slot Generator) 존재.
(각 노드는 데이터 링크 계층내의 MAC계층 데이터를 48바이트씩 받아 5바이트의 헤더를 붙인 후 53바이트를 만들어 가용한 슬롯에 실어 전송한다.)
