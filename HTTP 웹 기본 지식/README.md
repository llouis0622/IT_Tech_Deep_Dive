# 모든 개발자를 위한 HTTP 웹 기본 지식

## 1. 인터넷 네트워크

### 1. 인터넷 통신
- 클라이언트, 서버 연결
  - 물리적인 선 연결
  - 인터넷 망 연결

### 2. IP(인터넷 프로토콜)
- IP 주소 부여 -> 클라이언트, 서버 둘 다
- 지정한 IP 주소에 데이터 전달
- 패킷(Packet)이라는 통신 단위로 데이터 전달
- IP 패킷 정보 : 출발지 IP, 목적지 IP, 기타 등
- 클라이언트 패킷 전달 <-> 서버 패킷 전달
- IP 프로토콜의 한계
  - 비연결성 : 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
  - 비신뢰성 : 중간에 패킷이 사라짐 or 패킷이 순서대로 안 옴
  - 프로그램 구분 : 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상일 때

### 3. TCP, UDP
- 인터넷 프로토콜 스택 4계층 
  - 애플리케이션 계층 - HTTP, FTP
  - 전송 계층 - TCP, UDP
  - 인터넷 계층 - IP
  - 네트워크 인터페이스 계층
- TCP 패킷 정보 : 출발지 PORT, 목적지 PORT, 전송 제어, 순서, 검증 정보 등
- TCP 특징
  - 전송 제어 프로토콜(Transmission Control Protocol)
  - 연결 지향 - TCP 3way Handshake(가상 연결)
  - 데이터 전달 보증
  - 순서 보장
  - 신뢰할 수 있는 프로토콜
  - 현재는 대부분 TCP 사용
- TCP 3way Handshake : SYN -> SYN + ACK -> ACK -> 데이터 전송
- UDP 특징
  - 사용자 데이터그램 프로토콜(User Datagram Protocol)
  - 하얀 도화지에 비유(기능 거의 없음)
  - 연결 지향 X - TCP 3way Handshake X
  - 데이터 전달 보증 X
  - 순서 보장 X
  - 데이터 전달 및 순서가 보장되지 않음 but 단순하고 빠름
  - IP와 거의 동일 : PORT 체크섬 정도만 추가
  - 애플리케이션에서 추가 작업 필요

### 4. PORT
- 같은 IP 내에서 프로세스 구분 가능
- 0 ~ 65535 : 할당 가능
- 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
  - FTP : 20, 21
  - TELNET : 23
  - HTTP : 80
  - HTTPS : 443

### 5. DNS
- IP
  - 기억하기 어려움
  - 변경 가능성 존재
- DNS(Domain Name System) : 전화번호부, 도메인 명을 IP 주소로 변환

## 2. URI와 웹 브라우저 요청 흐름

### 1. URI
- Uniform Resource Identifier
  - Uniform : 리소스 식별하는 통일된 방식
  - Resource : 자원, URI로 식별할 수 있는 모든 것
  - Identifier : 다른 항목과 구분하는 데 필요한 정보
- URL, URN
  - URL(Uniform Resource Locator) : 리소스가 있는 위치 지정
  - URN(Uniform Resource Name) : 리소스에 이름 부여
  - 위치는 변할 수 있지만, 이름은 변하지 않음
  - URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
- 로케이터(Locator), 이름(Name) 또는 둘 다 추가로 분류될 수 있음
- URL 전체 문법
  - `scheme://[userinfo@]host[:port][/path][?query][#fragment]`
  - scheme
    - 주로 프로토콜 사용
    - 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
    - http -> 80 포트, https -> 443 포트 주로 사용
    - https -> http + 보안
  - userinfo
    - URL에 사용자 정보 포함해서 인증
    - 거의 사용하지 않음
  - host
    - 호스트명
    - 도메인명 또는 IP 주소를 직접 사용가능
  - PORT
    - 포트, 접속 포트
    - 일반적으로 생략
  - path
    - 리소스 경로, 계층적 구조
  - query
    - key=value 형태
    - `?`로 시작, `&`로 추가 가능
    - query parameter, query string 등으로 불림
    - 웹 서버에 제공하는 파라미터, 문자 형태
  - fragment
    - html 내부 북마크 등에 사용
    - 서버에 전송하는 정보 X

### 2. 웹 브라우저 요청 흐름
- DNS 조회 -> HTTP 요청 메시지 생성

## 3. HTTP 기본

### 1. 모든 것이 HTTP
- HyperText Transfer Protocol
  - HTML, TEXT
  - Image, 음성, 영상, 파일
  - JSON, XML(API)
  - 거의 모든 형태의 데이터 전송 가능
  - 서버간에 데이터를 주고 받을 때에도 대부분 HTTP 사용
- HTTP 역사
  - 1991년 : HTTP/0.9, GET 메서드만 지원, HTTP 헤더 X
  - 1996년 : HTTP/1.0, 메서드, 헤더 추가
  - 1997년 : HTTP/1.1, 가장 많이 사용, 우리에게 가장 중요한 버전
  - 2015년 : HTTP/2, 성능 개선
  - HTTP/3 진행중 : TCP 대신에 UDP 사용, 성능 개선
- 기반 프로토콜
  - TCP : HTTP/1.1, HTTP/2
  - UDP : HTTP/3
- HTTP 특징
  - 클라이언트 서버 구조 
  - 무상태 프로토콜, 비연결성
  - HTTP 메시지
  - 단순함, 확장 가능

### 2. 클라이언트 서버 구조
- Request Response 구조
- 클라이언트는 서버에 요청을 보내고 응답 대기
- 서버가 요청에 대한 결과를 만들어서 응답

### 3. Stateful, Stateless
- 서버가 클라이언트의 상태 보존 X
- 서버 확장성 높음 but 클라이언트가 추가 데이터 전송
- Stateful : 상태 유지, 항상 같은 서버가 유지되어야 함
- Stateless : 무상태 -> 응답 서버 쉽게 변경 가능, 아무 서버나 호출 가능
  - 모든 것을 무상태로 설계할 수 있는 경우도 있고 없는 경우도 존재
  - 상태 유지는 최소한만 사용

### 4. 비연결성(Connectionless)
- HTTP는 기본이 연결을 유지하지 않는 모델
- 일반적으로 초 단위의 이하의 빠른 속도로 응답
- 서버 자원을 매우 효율적으로 사용 가능
- TCP/IP 연결을 새로 맺어야 함 -> 3way Handshake 시간 추가
- 웹 브라우저로 사이트 요청 -> HTML 뿐만 아니라 JS, CSS, 추가 이미지 등 수 많은 자원이 함께 다운로드
- HTTP 지속 연결로 문제 해결
- HTTP/2, HTTP/3에서 더 많은 최적화

### 5. HTTP 메시지
- HTTP 메시지 구조 : 시작 라인, 헤더, 공백 라인(CRLF), Message Body
- 시작 라인
  - 요청 메시지
  - start-line : request-line/status-line
  - request-line : method SP request-target SP HTTP-version CRLF
  - HTTP 메서드(GET 조회)
  - 요청 대상
  - HTTP version
  - GET : 리소스 조회
  - POST : 요청 내역 처리
  - absolute-path[?query] : 절대경로
- HTTP 상태 코드
  - 200 : 성공
  - 400 : 클라이언트 요청 오류
  - 500 : 서버 내부 오류
  - 이유 문구 : 사람이 이해할 수 있는 짧은 상태 코드 설명 글
- HTTP 헤더
  - header-field = field-name:OWS(띄어쓰기 허용) field-value OWS
  - HTTP 전송에 필요한 모든 부가정보
  - 표준 헤더가 너무 많음
  - 필요시 임의의 헤더 추가 가능
- HTTP 메시지 바디
  - 실제 전송할 데이터
  - HTML 문서, 이미지, 영상, JSON 등등 Byte로 표현할 수 있는 모든 데이터 전송 가능

