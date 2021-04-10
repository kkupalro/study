## **1. 리눅스에 대한 이해**

### **리눅스란**
- **리눅스**는 리누스 토르발스가 커뮤니티 주체로 개발한 컴퓨터 운영체제, 혹은 커널을 뜻함
- **리눅스**는 자유소프트웨어와 오픈소스 개발이 가장 유명한 표본
- **리눅스**는 다중 사용자, 다중 작업(멀티태스킹), 다중 스레드를 지원하는 네트워크 운영체제

### **Linux 특징**
- **장점)** 무료, 오픈 소스, 멀티태스킹, 누구나 수정하고 개발 가능
- **단점)** 커널 및 라이브러리 버전이 변화가 빠름, (개인환경)사용자 UI 중심보다는 (기업환경)인프라 또는 어플리케이션 환경에 최적화에 초점

## **2. 오픈소스에 대한 이해**

### **사물인터넷(IoT) : 모든 사물은 연결되어야 한다.**
- 구글 글라스, 갤럭시 기어, iwatch
- KT olleh GIGA IoT, LGU+ IoT@home 등
- M2M, 비콘, NFC기술을 활용한 생활밀착형 서비스
- 2015 : 150억개, 2020 : 310억개 연결 예상

### **빅데이터 : 데이터의 홍수 시대**
- 매년 50% 이상의 데이터 증가율
- 데이터 생성, 수집, 분석
- 3V (Volume, Velocity, Variety)

### **클라우드 컴퓨팅**
- Public, Private, Hybrid 클라우드 컴퓨팅
- 다양한 클라우드 컴퓨터 기술

### **하드웨어도 오픈소스 OSHW**
- 오픈컴퓨트 프로젝트(opencompute.org) : 
Facebook 주도의 하드웨어 아키텍쳐 오픈
- 라즈베리 파이 : 교육용 보드
- 아두이노 : 마이크로 컨트롤러 내장 제어용 기판

### **왜 오픈 소스인가?**
- 개방성에 따른 업계 ‘사실상’
-	표준화 및 모듈화
-	기능성, 성능, 안정성
- 시장환경 및 비용 절감
-	클라우드 인프라 소프트웨어
-	커뮤니티의 피드백과 로드맵이 더 중요
-	TCO/ROI 경제성
- 기술 경쟁력 확보에 따른 종속성 탈피
-	개발자/테스터/고객이 언제나 소통 가능
-	신속한 버그 발견 및 패치
- 투명성 및 접근 용이성
-	제품 기능 및 스펙의 공개
-	소스의 공개

### **최근 오픈소스 IT업계 핫이슈**
- 벤더사 중심에서 서비스 마켓중심으로
- 애플과 구글의 오픈소스 협업
- 오픈소스 인공지능 연합군 구축하는 글로벌IT기업

## **3. 인프라에 대한 이해**

### **시대 흐름에 따른 인프라 환경 변화**
- 1960 : MainFrame
-	MainFrame Vendor
- 1990 : Client/Server
-	2 Tier
-	Unix (Vendor)
-	Scale Up
- 2000 : Web
-	3 Tier
-	Linux
-	Scale Out
- 2010 : Cloud
-	IoT / Big Data
-	Mobile
-	Elastic Scaling

### **가트너 선정 2020년 10대 기술 트렌드**
- 초자동화(Hyperautomation)
- 다중경험(Multiexperience)
- 전문성의 민주화(Democratization of Expertise)
- 인간증강(Human Augmentation)
- 투명성 및 추적성(Transparency and Traceability)
- 자율권을 가진 엣지(The Empowered Edge)
- 분산형 클라우드(Distributed Cloud)
- 자율 사물(Autonomous Things)
- 실용적 블록체인(Practical Blockchain)
- 인공지능과 보안(AI Security)

### **IaaS PaaS SaaS**
![image](https://user-images.githubusercontent.com/34331235/114262617-f5966200-9a1b-11eb-940e-77fdb065afce.png)<br>

### **클라우드의 혼란**
- 예상되는 클라우드 IaaS비용 증가

### **숨은 실력자 리눅스**
- 시스템 제어 / 자동화 단말기
- 무인 자동차
- PMP테블릿 / 모바일 기기
- 지능형 로봇 / 홈 네트워크
- 첨단 의료기기 / 보안시스템
- IoT
- 네비게이션
- facebook / Instagram / twitter

## **3. 파일 시스템 관리**

### **리눅스 명령어**

#### 명령어
```
nmcli con add type team con-name team0 ifname team0 config '{"runner":{"name":"activebackup"}}'
```

#### 확인
```
nmcli con show
```

#### team0에 아이피 할당
```
nmcli con mod team0 ipv4.addresses 
192.168.136.238/24
```

#### 명령어1
```
nmcli con mod team0 ipv4.method manual
```

#### 명령어2
```
cd /etc/sysconfig/network-scripts
```

#### 37 38 연결
```
nmcli con add type team-slave ifname ens37 master team0 con-name team0-38
```

#### 38 37 연결
```
nmcli con add type team-slave ifname ens38 master team0 con-name team0-37
```

#### team0에 연결
```
nmcli con up team0
```

#### 디스크 추가한 것 업데이트
```
echo ‘- - -‘ > /sys/class/scsi_host/host0/scan
```

#### 장치 파일 확인
```
fdisk -l
```

#### 디스크 파티션 작업 명령어 유틸리티 사용
```
fdisk /dev/sdb
```
#### 파티션 확인
```
fdisk -lu /dev/sdb
```
- n // 새로운 파티션 생성
- +5G // 사이즈 할당
- p // 출력
- w // 저장

### **장치 타입**
- SCSI /dev/sda


## **4. 네트워크 서버(FTP) 구성**

### **리눅스 명령어(설치)**
```
yum install vsftpd
yum install ntp
yum install ftp
systemctl start ntpd
systemctl status ntpd
systemctl start vsftpd // 시작
ftp localhost
anonymous // 익명 아이디 비밀번호 엔터
quit // 나가기
/* 방화벽 열기 */
firewall-cmd —permanent –add-port=21/tcp
firewall-cmd —permanent –add-service=ftp
firewall-cmd —reload
ftp server1 (station1)
yum Install httpd // 아파치 웹서버 설치
systemctl start httpd // 시작
systemctl status httpd // 확인
cd /var/www/html/
echo Hello > index.html
firewall-cmd --permanent --add-service=http
firewall-cmd —reload
```

### **마운트 하기**
```
fdisk /dev/sdd
fdisk -lu /dev/sdd
yum install lvm2
pvcreate /dev/sdd1
vgcreate vg02 /dev/sdd1
lvcreate -l 100%FREE -n lvol02 vg02
mkfs.xfs /dev/vg02/lvol02
mkdir -p /iscsi_disk
vi /etc/fstab
mount -a
df -h
```
