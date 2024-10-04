
# 네트워크 기본 개념
## 네트워크에서 서버와 클라이언트는 각각 어떤 역할을 하나요?
> 서버
- 클라이언트의 요청을 처리하고 응답하는 역할
- 데이터베이스, 파일서버, 웹 서버 등 형태로 존재 
> 클라이언트
- 서버에 데이터를 요청하거나 정보는 제공받는 역할
- HTTP, FTP 등 네트워크 프로토콜을 통해 서버에 요청을 전송 

## HTTP와 HTTPS의 차이점은 무엇인가요?
> HTTP ( Hyper Text Transfer Protocol )
- 웹 브라우저(클라이언트)와 웹 서버가 데이터를 주고받기 위한 프로토콜
- OSI 애플리케이션 레벨의 프로토콜
- 암호화 되지 않은 평문 데이터 전송
  
> HTTPS ( Hyper Text Transfer Protocol Secure )
- HTTP에 SSL/TLS 암호화 프로토콜이 추가된 프로토콜
- 클라이언트와 서버 간의 데이터가 암호화되어 전송되므로 중간에 데이터가 변경되는 것을 방지 
- SSL/TLS 인증서를 사용하여 서버를 보증. 해당 인증서는 CA(Certificate Authority)에서 발급 

## TCP와 UDP의 차이점은 무엇인가요?
> TCP (Transmission Control Protocol)
- 연결 지향적 프로토콜로 신뢰성 있는 데이터 전송 보장
- 데이터 전송 전에 클라이언트와 서버간에 3-way handshaking, 4-way handshaking를 통해 연결 설정 후 데이터 주고받고 연결을 해제함 
- 네트워크 상태에 따라 전송 속도를 조절하여 네트워크 혼잡 방지
- 데이터 전송 중 클라이언트와 서버간의 연결 유지. 전송 완료되면 연결 해제
- 데이터 전송 후 상대로부터 응답(ACK)를 받아 패킷이 정상적으로 도착했는지 확인
- HTTP/HTTPS , SMTP, FTP 등 신뢰성이 중요한 서비스에 사용
  
> UDP (User Datagram Protocol)
- 비연결형 프로토콜로 빠른 데이터 전송을 보잠 
- 연결을 설정하고 해제하는 과정이 없고, 데이터의 신뢰성을 보장하지않음
- 연결 설정 과정이 없으므로 전송속도가 빠름
- TCP에 비해 프로토콜 구조가 단순하며 오버헤드가 적음
- 실시간 스트리밍, 온라인 게임 등 실시간 서비스에서 많이 사용

- https://dev-coco.tistory.com/144

> 차이점
- TCP는 연결형 프로토콜로 데이터를 전송하기 전에 연결을 설정하며, 신뢰성 있는 데이터 전송을 보장함
- UDP는 비연결형 프로토콜로 데이터를 전송하기 전에 연결을 설정하지 않으며, 데이터 전송이 빠르지만 신뢰성이 보장되지 않음 
  
## IP 주소란 무엇이며, 어떻게 분류되나요?
> IP 주소(Internet Protocol Address)란?
- 네트워크 상에서 각 장치가 서로 통신할 수 있도록 고유하게 할당된 숫자 주소
> IP 분류
1. 공인 IP (Public IP) / 사설 IP (Private IP)
-  공인 IP (Public IP)
      + 인터넷 서비스 제공자(ISP)로부터 할당받은 전 세계적으로 고유한 IP주소
      + 인터넷에 직접 연결된 장치가 사용하는 주소.
      + 웹사이트, 서버, 네트워크 장비 등 외부 네트워크와의 통신에 사용
-  사설 IP (Private IP)
      + 내부 네트워크에서만 사용되는 IP주소
      + 회사 내부에서 사용되며, 외부 인터넷과는 NAT(Network address Translation)를 통해 공인 IP를 통해 연결
      + 사설 IP 범위
      + 10.0.0.0 - 10.255.255.255
      + 172.16.0.0 - 172.31.255.255
      + 192.168.0.0 - 192.168.255.255

2. IPv4 / IPv6
- IPv4 (Internet Protocol version 4)
  + 32비트 숫자, 4개의 8비트를 점으로 구분 (192.168.0.1)
  + 0 ~ 255 사이의 숫자를 가지며 최대 약 43억개의 고유 주소 제공가능
  + 5가지 클래스로 분류
      + A class : 대규모 네트워크 환경(대기업)에서 사용, 첫번째 옥텟값의 10진수 범위 (0~127), 0.0.0.0 ~ 127.255.255.255
      + B class : 중간규모 네트워크 환경(중소기업, 대학교 등)에서 사용, 첫번째 옥텟값의 10진수 범위 (128~191), 128.0.0.0 ~ 191.255.255.255
      + C class : 소규모 네트워크 환경(소규모 회사, 개인)에서 사용, 첫번째 옥텟값의 10진수 범위 (192~223), 192.0.0.0 ~ 223.255.255.255  
      + D class , E class : 멀티캐스팅용, 연구/개발용으로 일반적으로 잘 사용되지 않음
- IPv6 (Internet Protocol version 6)
    + IPv4 주소가 부족해서 나오게됨
    + 128비트 숫자, 16진수 형식으로 8그룹으로 ":" 으로 구분 (2001:0db8:85a3:0000:0000:8a2e:0370:7334)

3. 고정 IP (Static IP) / 동적 IP (Dynamic IP)
- 고정 IP (Static IP)
    + 변하지 않는 고유의 IP 주소
    + 서버, 프린터 등 같은 IP 주소를 유지해야하는 장치에 사용
    + 설정된 후에 변경되지 않으며, 장치가 인터넷에 접속할 때마다 동일한 IP 주소 할당 
- 동적 IP (Dynamic IP)
    + DHCP(Dynamic Host Configuration Protocol)를 통해 네트워크에 연결될때마다 동적으로 할당되는 IP 주소
    + 개인 사용자, 일반 네트워크 장치에 사용

> DHCP(Dynamic Host Configuration Protocol)
- 네트워크 상에서 IP 주소와 네트워크 설정( 서브넷 마스크, 기본 게이트웨이, DNS 서버 )을 자동으로 할당해주는 프로토콜

## OSI 7계층 모델을 설명해주세요.
- 네트워크 통신을 계층별로 분류해놓은 모델

1. 물리 계층 (Physical Layer)
- 데이터를 전기 신호로 변환하여 물리적 형태로 변환하여 전달
- 케이블, 전선, 전파 등을 통해 비트 스트림이 전송되는 통로 제공
- 데이터 단위 : 비트 
2. 데이터링크 계층 (Data Link Layer)
- 물리 계층에서 발생할 수 있는 오류를 감지하고 수정하며, MAC 주소를 사용해 같은 네트워크 내에서 장치 간 데이터 전송 관리
- 데이터 단위 : 프레임 
3. 네트워크 계층 (Network Layer)
- 데이터를 IP 주소를 사용하여 다른 네트워크 간의 라우팅을 관리.
- 라우터가 작동하며, 데이터를 목적지까지 전달할 경로 설정 
- 패킷을 목적지 네트워크로 라우팅하고, 각 패킷이 목적지에 도달할 수 있도록 경로 설정
- 데이터 단위 : 패킷 
4. 전송 계층 (Transport Layer)
- 종단 간 통신을 제공하고, 데이터의 신뢰성 있는 전송 보장 ( TCP, UDP ) 
- 데이터 단위 : 세그먼트
5. 세션 계층 (Session Layer)
- 응용 프로그램 간의 통신 세션을 설정, 유지, 종료하는 역할
- 데이터 단위 : 데이터
6. 표현 계층 (Presentation Layer)
- 데이터를 표현하고 변환하는 역할. 
- 전송하는 데이터의 인코딩, 디코딩, 암호화, 코드 변화
- 데이터 단위 : 데이터 
7. 애플리케이션 계층 (Application Layer)
- 사용자와 직접적으로 상호작용하는 프로그램 서비스 제공 담당
- HTTP, FTP, SMTP
- 데이터 단위 : 메시지, 데이터 


## TCP/IP 모델을 OSI 모델과 비교하여 설명해주세요.
> 네트워크 접근 계층 (Network Access Layer)
-  인터넷을 구성하는 각각 다른 물리적 네트워크의 연결과 관련된 기능 수행
-  OSI 7계층의 물리계층 + 데이터 링크 계층
> 인터넷 계층 (Internet Layer)
- 데이터를 패킷으로 분할하고 목적지까지 전송 경로 설정 ( IP )
- OSI 7계층의 네트워크 계층
> 전송 계층 (Transport Layer)
- 송신측과 수신측 사이에서 데이터를 전송하는 기능 수행
- OSI 7계층의 전송 계층
> 응용 계층 
- 사용자와 직접적으로 상호작용하는 프로그램 서비스 제공 담당
- OSI 7계층의 응용 계층 + 표현 계층 + 세션 계층

> 차이점
- OSI 7계층은 이론적인 참조 모델이며, TCP/IP는 실제로 구현된 프로토콜 스택

## DNS의 역할은 무엇이며, 작동 방식은 어떻게 되나요?
> DNS(Domain Name System) 란?
- 도메인 이름을 IP 주소로 변환해주는 시스템
- 사용자가 도메인 주소를 통해 웹사이트에 쉽게 접근할 수 있도록 함
> 작동 방식
1. 사용자가 브라우저에 도메인 입력 ( www.google.com )
2. 사용자의 캐시(운영체제 또는 브라우저에 저장된 임시 DNS 정보)에 도메인에 대한 IP 주소가 저장되어 있는지 확인 -> 캐시에 정보가 있으면 바로 IP 주소 반환하여 요청된 웹사이트에 연결
3. 캐시에 정보가 없으면, 사용자의 컴퓨터는 DNS Resolver에 도메인 이름에 대한 IP 주소 요청
4. DNS Resolver는 루트 DNS 서버에 최상위 도메인 (TLD, Top-level Domain) 정보를 요청
5. 루트 DNS 서버는 DNS Resolver에게 .com의 TLD 서버의 주소를 반환
6. DNS Resolver는 TLD 서버에게 정보를 요청하면, TLD 서버는 google.com에 대한 권한있는 네임서버의 주소를 반환
7. DNS Resolver는 최종적으로 권한있는네임서버에 정보를 요청하면, 해당 서버는 www.google.com 도메인에 대한 IP주소를 DNS Resolver에게 반환
8. DNS Resolver는 해당 IP 주소를 사용자에게 반환하며, 캐시에 일정시간동안 저장
9. 사용자의 브라우저는 해당 IP 주소를 사용해 웹 서버에 접속하고, 사용자가 요청한 웹 페이지 가져옴

> DNS 서버 종류
- DNS resolve (DNS Recursive Server): 요청 받은 도메인에 매칭되는 IP 주소를 찾기 위해 DNS 쿼리를 수행. DNS 캐시 저장하는 곳
- 루트 DNS 서버 (Root Name Server): 순환 DNS 서버에서 처음으로 DNS 쿼리 요청을 보내는 서버. 해당 도메인의 확장자(.com, .net, .org 등)에 따른 TLD 네임 서버의 주소를 DNS Resolver에 응답.
- 최상위 도메인 DNS 서버 (TLD Name Server): 최상위 도메인(.com, .net, .org 등)에 대한 DNS 정보를 관리. 루트 DNS 서버와 권한 네임 서버의 중간 단계.
- 권한 네임 서버 (Authoritative Name Server): 도메인의 IP 주소를 응답해주는 최종 단계 DNS 서버.

  
## ARP(주소 결정 프로토콜, Address Resolution Protocol)란 무엇이며, 어떻게 작동하나요?
> ARP(주소 결정 프로토콜, Address Resolution Protocol)란?
- 네트워크에서 IP 주소를 통해 통신할때 해당 IP 주소에 대응하는 MAC 주소를 찾아주는 프로토콜
- 요청과 응답으로 구성된 프로토콜로 라우팅 되지 않는 단일 네트워크에서만 동작 (L2-L3사이에 있는 프로토콜)
- 단일 네트워크 : 같은 IP 주소 범위 내에 있는 장치들이 속한 네트워크 
> 동작원리
1. 송신자는 목적지 IP 주소를 지정해 패킷을 송신
2. 네트워크 계층의 IP 프로토콜이 ARP 프로토콜에게 ARP Request 메시지를 생성하도록 요청
3. 메시지는 데이터링크 계층으로 전달되고, 이더넷 프레임으로 캡슐화됨
4. 같은 네트워크에 있는 모든 장치(모든 호스트와 라우터)는 프레임을 수신 후 자신의 ARP 프로토콜에게 전달
5. 목적지 IP 주소가 일치하는 시스템은 자신의 물리주소를 포함하고 있는 ARP Reply 메시지 보냄
6. 송신자는 요청한 목적지 IP 주소에 대응하는 물리주소 획득

- https://coding-factory.tistory.com/720

## NAT(Network Address Translation)란 무엇인가요?
> NAT(Network Address Translation)란
- 라우터 등의 장비를 사용하여 다수의 private IP를 하나의 public IP로 변환하는 기술
- 주소변환 정보에 대해 IP 주소와 port 번호로 구성된 NAT Forwarding Table을 보관하고 있음

## 네트워크에서 CORS(Cross-Origin Resource Sharing)는 무엇인가요?
> CORS(Cross-Origin Resource Sharing)란?
- 웹 브라우저가 다른 출처의 리소스에 대한 접근을 허용하는 정책
- SOP 정책을 위반해도 CORS 정책에 따르면 다른출처의 리소스를 허용
  
> SOP(Same Origin Policy)
- 동일한 origin에서만 리소스를 공유할 수 있다는 정책
- Origin : Protocol + Host + Port 를 합친 URL ( https://www.google.com:3000 )

> CORS 동작
- 클라이언트에서 HTTP 요청 헤더에 Origin 정보를 담아서 전달
- 서버는 응답헤더에 Access-Control-Allow-Origin를 담아서 클라이언트에 전달
- 클라이언트에서 Origin과 서버가 보내준 Access-Control-Allow-Origin 비교
- 이때 유효하지 않다면 CORS 에러 발생

- https://inpa.tistory.com/entry/WEB-%F0%9F%93%9A-CORS-%F0%9F%92%AF-%EC%A0%95%EB%A6%AC-%ED%95%B4%EA%B2%B0-%EB%B0%A9%EB%B2%95-%F0%9F%91%8F

## 기타 정리 사항
> URI / URL 
- URI (Uniform Resource Identifier, 자원의 식별자)
  + 자원이 어디에 있는지 자원 자체를 식별하는 방법
  + URL 보다 더 포괄적인 개념
  + URN(urn:doi:10.1000/182) , 메일 주소(mailto:someone@example.com), FTP 등 
- URL (Uniform Resource Locator, 위치)
  + 네트워크 상에 자원이 어디 있는지 위치를 알려주기 위한 규약
  + ex) "https://www.google.com:443/search?q=test&hl=ko"
      + shceme : "https" 프로토콜 사용
      + host : "www.google.com" 도메인명, IP 주소
      + port : "443"  접속 포트, 일반적으로 생략 가능
      + path : "search" 리소스 경로
      + query : "q=test&hl=ko" 웹서버에 제공하는 파라미터

> URL 웹 브라우저 요청 흐름
1. URL 입력 / DNS 조회
   - 사용자가 브라우저에 URL 입력 -> 브라우저는 URL을 분석
   - URL에 포함된 도메인을 IP 주소로 변환하기 위해 DNS 서버에서 도메인의 IP 주소 조회
   - 로컬 캐시 조회 -> DNS Resolver에 요청 -> 루트 네임서버 조회 -> TLD 네임 서버 조회 -> 권한 있는 데임 서버 조회
2. TCP 연결 설정
    - IP 주소 확인 후 TCP 연결 설정
    - TCP 3-way handshake 과정을 통해 클라이언트-서버 연결 설정 ( 클라이언트가 서버에 연결 요청 -> 서버가 요청 수락 후 응답 보냄 -> 클라이언트가 서버의 응답 확인 후 연결 설정 )
3. HTTPS 요청 전송
    - tcp 연결이 완료되면 브라우저는 HTTP/HTTPS 프로토콜을 통해 서버에 요청 전송
4. 서버는 클라이언트 요청을 분석하고 필요한 데이터 반환
5. 클라이언트는 브라우저가 응답을 수신 후 받은 데이터들을 파싱하여 렌더링 


# 데이터 통신 및 프로토콜
## TCP 3-way 핸드셰이크 과정은 무엇인가요?
## 4-way 종료 과정(TCP 연결 종료)은 어떻게 이루어지나요?
## 데이터 전송 중 손실이 발생할 때 TCP는 어떻게 처리하나요?
## TCP에서 슬라이딩 윈도우 프로토콜의 역할은 무엇인가요?
## HTTP 상태 코드 200, 301, 404, 500의 차이점을 설명해주세요.
## HTTP/1.1과 HTTP/2의 주요 차이점은 무엇인가요?
## REST API와 SOAP의 차이점은 무엇인가요?
## 웹소켓(WebSocket)이란 무엇이며, HTTP와의 차이점은 무엇인가요?
## MQTT 프로토콜은 무엇이며, 어떤 상황에서 사용되나요?
## FTP와 SFTP의 차이점을 설명해주세요.
