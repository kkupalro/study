## **1. 네트워크의 4가지 속성**

### **01 분임 토의**
- **네트워크는 무엇인가? (What is an network?)**
- 어떠한 목적을 이루기 위해, 두개 이상의 엣지가 연결된 것
- Net(그물) + Work(목적)
- 연결 대상
- 쉽게 연결
- 연결 인접성
- 연결 성공
<br>![image](https://user-images.githubusercontent.com/34331235/114262856-422e6d00-9a1d-11eb-8b71-b3fc49998150.png)<
- **페이지랭크(PageRank)**는 월드 와이드 웹과 같은 하이퍼링크 구조를 가지는 문서에 상대적 중요도에 따라 가중치를 부여하는 방법이다. 이 알고리즘은 서로간에 인용과 참조로 연결된 임의의 묶음에 적용할 수 있다.

###
- 너와 나만
- 친구를 만남
- 친구에 친구 만남
- 연결 성공
- Facebook은 2006년부터 “다양한 방식으로 API를 오픈”했다.
- API(Application Programming Interface, 응용 프로그램 프로그래밍 인터페이스)는 응용 프로그램에서 사용할 수 있도록, 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻한다. 주로 파일 제어, 창 제어, 화상 처리, 문자 제어 등을 위한 인터페이스를 제공한다.

###
- 전세계 및 한국 인터넷 사용자 현황(2011.11 조사 결과)
- 전세계 19억 6천 6백 51만 명, 한국 약 3천 7백 13만 명(전체 인구 중 78%, 만 3세 이상 이용)

###
- 시간과 공간
- 정보 전달 변화
- 가상 세계
- 네트워크 가상화
- 네트워크는 유기적으로 진화하는 시스템임과 동시에 원거리를 ‘연결’하고 시공간의 개념을 확장시키는 원동력으로 성장해왔다.

### **02 네트워크의 시작점**
- **우리가 알고 있는 네트워크 (The network we know?)**
- “LAN Card”
- 전기 신호로부터 데이터를 수신하고 변환
- MAC Address를 이용한 데이터의 수신여부 판별
- 케이블의 타입
- 토폴로지
- 네트워크의 확장

#### **What’s a protocol?**
- 프로토콜의 종류
-	Open Protocols (TCP/IP)
-	Vendor-Specific Protocols (IPX/SPX)
-	Vendor-Specific Protocols (NetBEUI))
- 네트워크에서의 방송
-	Unicast : 정확한 목적지를 가지고 통신
-	Broadcast : 목적지를 가지지 않고 통신
-	Multicast : 그룹을 지정하고 그 그룹에게만 정보를 전달

#### **“OSI 7 Layer”**
국제표준기구(ISO)에서 표준화된 네트워크 구조를 제시한 기본 모델로써 통신망을 통한 상호접속에 필요한 제반 통신절차를 정의 한것
-	Application : 프로그램, User Interface
-	Presentation : 데이터 암호화
-	Session : 사용자의 세션 유지
-	Transport : Reliable or Unreliable delivery
-	Network : Logical Address
-	Data Link : 비트를 Frame으로 만듬
-	Physical : 장비들 간에 bit 전송

#### **“데이터 캡슐화”**
-	Application 
-	Presentation
-	Session
-	Transport : Segment
-	Network : Packet
-	Data Link : Frame
-	Physical : Bits

## **2. 클라우드 서비스의 이해**

### **01 클라우드 개념**
- **클라우드 정의** : 인터넷을 통해 서버, 스토리지, SW 등 ICT자원을 필요시 서비스 형태로 이용하며 사용한 만큼 비용 지불
- TTA : 가상화와 분산처리 기술을 기반으로 인터넷을 통해 대규모 IT자원을 임대하고, 사용한 만큼의 요금을 지불하는 컴퓨팅 환경을 의미
- 가트너 : 인터넷 기술을 활용해 고객에게 수준 높은 확장성을 가진 자원들을 서비스로 제공하는 컴퓨팅의 한 형태
- IBM : 웹 기반 응용 소프트웨어를 활용해 대용량 DB를 인터넷 가상공간에서 분산 처리하고, 이 데이터를 다양한 단말기에서 불러오거나 가공할 수 있는 환경

#### **클라우드 서비스 특징**
- 주문형 셀프 서비스 : 필요할 때 온라인으로 즉시 사용
- 광대역 네트워크 접근 : 네트워크를 통한 서비스 자원 접근
- 빠른 탄력성 : 다중 임대 모델을 통한 자원 할당
- 자원의 공동관리 : 비즈니스 상황에 따른 자원의 탄력적 사용
- 측정 가능한 서비스 : 서비스를 사용한 만큼 비용 지불

#### **클라우드 서비스 제공 모델**
- EnterPrise IT : on-premise 방식
- IaaS : AWS EC2
- Paas
- Serverless
- SaaS : Google Spreadsheet

#### **클라우드 운용 모델**
- Hybrid
- Private
- Public

### **02 클라우드 서비스를 위한 기술**
- **클라우드 구성 지원 기술 요소**
- 가상화 기술
- 분산 컴퓨팅 기술
- 오픈 인터페이스
- 프로비저닝 : 시스템 자원을 할당, 배치, 배포해 두었다가 시스템을 즉시 사용할 수 있는 상태로 미리 준비해 두는 것

#### **가상화 개념**
- 물리적으로 다른 시스템을 논리적으로 통합하거나 하나의 시스템을 논리적으로 분할해 자원을 할당하는 것

#### **가상화 기능**
- 공유
- 단일화 
- 에뮬레이션 : 원래 없는것을 처음부터 있는것처럼 보이게 하는것
- 절연

#### **네트워크 가상화**
- SDS(Software Defined Network) : 네트워크 장치(Control Plane)의 제어와 전송부(Data Plane)를 분리하는 개념
- NFV(Network Function Vitualization) : 방화벽이나 로드밸런서와 같은 네트워크 장비를 가상화하는 개념

### **03 클라우드 서비스의 동향**

#### **기업별 시장점유율**
- AWS : 34.4%
- MS : 14.4%
- IBM : 7.2%
- Google : 6.6%
- Alibaba : 4.1 %
- 기타 : 33.3%

### **04 퍼블릭 클라우드 서비스 소개 (AWS)**

#### **Compute Servie**
-	IaaS : Amazon Elastic Compute Cloude (EC2)
-	PaaS : AWS Elastic Beanstalk
-	Containers : Amazon Elastic Container Service
-	Serverless Functions : AWS Lambda
-	
#### **Database Services**
-	RDBMS : Amazon Relational Database Service
-	NoSQL (Key-Value) : Amazon DynamoDB
-	NoSQL (Indexed) : Amazon SimpleDB
-	
#### **Storage Service**
-	Object Storage : Amazon Simple Storage Service
-	Block Storage : Amazon Elastic Block Store
-	Cold Storage : Amazon Glacier
-	File Storage : Amazon Elastic File System
-	
#### **Networking Services**
-	Vitrual Network : Amazon Virtual Private Cloud (VPC)
-	Elastic Load Balancer : Elastic Load Balancer
-	Peering : Direct Connect
-	DNS : Amazon Route 53

### **05 AWS 소개**

#### **AWS 클라우드 컴퓨팅**
- AWS는 네트워크로 연결된 하드웨어들을 소유하고 유지 관리합니다
- 고객은 필요한 항목을 프로비저닝하여 사용합니다.
- 애플리케이션
- 플랫폼 서비스
- 기초 서비스
- 글로벌 인프라

#### **AWS 인터페이스**
- AWS Management Console
- AWS CLI
- AWS SDK
- AWS API

### **06 글로벌 인프라 소개**

#### **용어**
- Region = AZ 묶음 (서비스 관리하는 인프라)
- AZ = Data Center 묶음 (가용 영역)
- CloudFront (CDN 비슷)
- Shield : DDOS 공격 방어
- WAF
