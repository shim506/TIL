# 모두의 네트워크

## 1장. 네트워크 첫 걸음
### 패킷
- 네트워크를 통해 전송되는 테이터의 가장 작은 기본 단위
- 사진을 전송하는 과정
  1. 사진을 패킷 단위로 나눈다
  2. 각 패킷들에 번호를 붙여 전송한다.
  3. 전송된 패킷을 순서에 맞게 재구성하여 사진을 완성한다.
- 패킷을 단위로 데이터를 나누어 전송하는 이유
  - 큰 데이터를 통째로 보내면 데역폭을 너무 많이 차지하게 되어 다른 통신 흐름을 방해하게 됨

### 대역폭(BPS)
- 네트워크의 최대 전송 속도
- Bit Per Second
- 단위 시간당 전송량을 의미

### LAN / WAN
- LAN은 지리적으로 제한된 곳에서 컴퓨너와 프린터를 연결할 수 있는 네트워크
- WAN은 지리적으로 넓은 범위에 구축된 네트워크
- WAN은 ISP(인터넷 서비스 제공자) 를 통해 LAN 들을 조합한 네트워크이다.
- LAN 은 WAN 에 비해 빠르고 오류가 적다.

## 2장. 네트워크의 기본 규칙

### 프로토콜
- 데이터 통신을 위해 모두가 지켜야할 통신 규약을 지정했다.
- OSI 모델
  - 7개의 계층 존재
  - 응용, 표현 , 세션, 전송, 네트워크, 데이터링크, 물리 계층으로 구분된다.
- TCP/ IP 모델
  - OSI 모델의 간소화를 통해 4계층으로만 구분
  - 응용(응용 + 표현 + 세션), 전송, 인테넷(네트워크), 네트워크 접속(데이터링크 + 물리)

### 캡슐화
- 헤더를 데이터의 앞부분에 추가해나가는 과정
- 데이터의 송신 기준 데이터 레이어가 깊어질 수록 각 계층에 맞는 헤더가 추가됨
- 헤더에는 데이터를 전달받을 상대에 대한 정보도 포함
- 마지막 레이어인 데이터 링크 계층에서는 해더와 함께 트레일러를 추가함
  - 트레일러란 데이터를 전달할 때 데이터의 마지막에 추가하는 정보를 말함
- 데이터 수신 측에서는 반대로 한꺼풀씩 해더를 떼어 내고 이를 역캡슐화라고함


## 3장. 물리 계층 : 데이터를 전기 신호로 변환하기
- 물리 계층에서 0,1 데이터는 랜카드에의해 전기 신호로 변환되어짐
- 전기 신호에는 아날로그, 디지털 신호가 존재함
  - 아날로그 신호 : 미분 가능한 그래프 형태
  - 디지털 신호 : 계단식 그래프

### 전송 매체 : 케이블
- 무선 : 라디오파, 마이크로파 , 적외선
- 유선 : 트위스트 페어 케이블, 광케이블
  - 트위스터 페어케이블 = UTP 케이블 + STP 케이블 = 랜 케이블
  - STP 케이블 : 케이블을 실드로 보호하고 있어서 노이즈에 영향을 적게 받음
  - UTP 케이블 : 케이블을 실드로 보호하지 않아서 노이즈에 영향을 많이 받음, 싸서 일반적으로 많이 쓰임
  - 랜케이블은 커넥터 구성에 따라 다이렉트 케이블과 크로스 케이블로 나뉨
    - 다이렉트 케이블 : 시작 커넥터의 번호와 종단 커넥터의 번호가 일치함 (컴퓨터와 스위치 연결시 사용)
    - 크로스 케이블 : 시작 커넥터의 번호와 종단 커넥터 번호가 꼬아져 있음 (컴퓨터와 컴퓨터 연결시 사용)
      - 컴퓨터 끼리 연결시 수신과 송신에 대해 충돌이 나지 않기 위해 설계됨
### 리피터 와 허브
- 리피터 : 전기 신호의 정상 파형을 유지하게 하기 위해서 중간에 파형을 증폭 시켜주는 역할, 근래에는 거의 쓰이지 않음
- 허브 :  연결된 여러대의 컴퓨터에서의 전기신호를 증폭해주는 역할을 함


## 의문
- 패킷 내부 데이터는 최대 몇 bit 혹은 byte 가 들어갈까?


