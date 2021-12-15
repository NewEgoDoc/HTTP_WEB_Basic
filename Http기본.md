
 ### HTTP란 **H**yperText **T**ransfer **P**rotocol로서 모든 것을 이 프로토콜을 통해서 전송하고 받고있다.
        
        HTML, TEXT
        IMAGE, 음성, 영상, 파일
        JSON, XML (API)
        거의 모든 형태의 데이터 전송 가능
        서버간에 데이터를 주고 받을 때도 대부분 HTTP 사용

### HTTP 역사
- HTTP/0.9 1991년: GET 메서드만 지원, HTTP 헤더X
- HTTP/1.0 1996년: 메서드, 헤더 추가
- `HTTP/1.1 1997년: 가장 많이 사용, 우리에게 가장 중요한 버전`
    - RFC2068 (1997) -> RFC2616 (1999) -> RFC7230~7235 (2014)
- HTTP/2 2015년: 성능 개선
- HTTP/3 진행중: TCP 대신에 UDP 사용, 성능 개선

0.9라는 것은 처음엔 그렇게 안불렸겠지만 초창기에 발전을 하다가 1.1 이 되어 가장 중요하고 가장 많이 사용하는 버전이 되었다.
1.1에 대부분의 기능 스펙이 들어있고 2와 3는 성능 개선에 초점이 맞추어져 있다.

간추려 보자면 

- TCP: HTTP/1.1, HTTP/2
- UDP: HTTP/3
- 현재 HTTP/1.1 주로 사용
    - HTTP/2, HTTP/3 도 점점 증가

http3는 UDP프로토콜 위에 그냥 application 레벨에서 새로 설계해서 나온게  바로 3이다.

현재에는 2,3이 급속도로 퍼지고 있다.

# HTTP 특징
- 클라이언트 서버 구조
- 무상태 프로토콜(스테이스리스), 비연결성
- HTTP 메시지
- 단순함, 확장 가능



## 1. 클라이언트와 서버구조
    - Request Response 구조
    - 클라이언트는 서버에 요청을 보내고, 응답을 대기
    - 서버가 요청에 대한 결과를 만들어서 응답

![image](https://user-images.githubusercontent.com/53653597/146177493-44eed9ff-075d-49db-8220-b87046b172b7.png)


http는 클라이언트가 http 메세지를 통해서 서버에 요청을 보내게 되고 클라이언트는 서버의 응답이 올때까지 그냥 기다리게 됨.

서버가 요청을 해서 기다린 응답이 오면 그 응답결과를 열어서 클라이언트가 동작을 하게 됨.

자 이렇게 설명하면 되게 단순한 것 같다

하지만, 메세지를 보내고 서버가 응답을 한다

이렇게 분리를 하는게 중요하다

클라이언트와 서버를 `분리`하면서 서버는 비지니스 로직이나 데이터에 클라이언트 UI 사용성에 집중하면서 각각 독립적으로 진화를 할수가 있다.

복잡한 비지니스 로직이나 데이터 처리는 그냥 서버가 처리하게 되는 것이다.

반면에 클라이언트에 해당하는 UI 는 안드로이드 인터넷 ios 마다에 집중하면서 각각 발전해나갈수 있다.

서버의 아키텍처를 어떻게 할지 서버의 대용량 트래픽으로 더 고도화하고 진화 할지를 백엔드에서는 그것만 고민하면 되는 것이다.

php를 쓰다가 자바로 바꾼다던가 다른 언어로 바꾸더라도 

서버는 그것에 대해서 상관할 필요가 없는 것이다.

이렇게 두 그룹으로 나누어 생각하면 양쪽이 **` 독립적으로 진화 할 수 있다.`**

---

## 2. 무상태프로토콜

![image](https://user-images.githubusercontent.com/53653597/146179386-4b5afda7-5a8d-40f9-9229-e9a1aeb6ba85.png)

위의 예제와 같이고객에 대해서 데이터를 계속 쌓으면서 가기때문에 점원이 다른일을 하다가와도 점원이 바뀌어도 마지막 결제까지 순탄하게 갈 수 있다.


HTTP의 중요한 특징중에 하나는 '무상태 프로토콜'을 지향한다는 것이다.
영어로는 stateless 즉,
서버가 클라이언트의 상태를 보존하지 않는다



### **Stateful, Stateless 차이**
**정리**
- 상태 유지: 중간에 다른 점원으로 바뀌면 안된다.

    (중간에 다른 점원으로 바뀔 때 상태 정보를 다른 점원에게 미리 알려줘야 한다.)

- 무상태: 중간에 다른 점원으로 바뀌어도 된다.
- 갑자기 고객이 증가해도 점원을 대거 투입할 수 있다.
- 갑자기 클라이언트 요청이 증가해도 서버를 대거 투입할 수 있다.
- 무상태는 응답 서버를 쉽게 바꿀 수 있다. -> **`무한한 서버 증설 가능`**

![image](https://user-images.githubusercontent.com/53653597/146181704-52d014af-1ee1-4c30-9885-0d8d3e718019.png)

상태유지는 중간에 한서버가 다운되면? 클라이언트는 처음부터 다시해야하지만 무상태 설계는 서버 다운에 대해 신경을 쓰지않기때문에
필요시 스케일아웃(수평확장) = 서버증설이 가능하다.

하지만 모든걸 무상태로 설계하기는 사실상 어렵다

### **Stateless**
**실무 한계**

- 무상태
    - 예) 로그인이 필요 없는 단순한 서비스 소개 화면
- 상태 유지
    - 예) 로그인
- 로그인한 사용자의 경우 로그인 했다는 상태를 서버에 유지
- 일반적으로 브라우저 쿠키와 서버 세션등을 사용해서 상태 유지
- 상태 유지는 최소한만 사용(그렇기 때문이 **`상태유지는 최소한으로 stateless는 최대한으로`**)

Stateless 설계의 **`단점`**도 알아두자! 항상 상태를 유지와 다르게 모든 데이터를 품고있어 **`엄청난 데이터를 주고 받게 될 수도`** 있다


## 3. 비 연결성(connectionless)

![image](https://user-images.githubusercontent.com/53653597/146183001-9756e52f-2e07-4337-bbf4-213f2fc0dc13.png)

### **비 연결성**
- HTTP는 기본이 연결을 `유지하지 않는 모델`
- 일반적으로 `초 단위의 이하의 빠른 속도`로 응답
- 1시간 동안 수천명이 서비스를 사용해도 실제 서버에서 동시에 처리하는 요청은 수십개 이하로 매우 작음
    - 예) 웹 브라우저에서 계속 연속해서 검색 버튼을 누르지는 않는다.
- 서버 자원을 매우 효율적으로 사용할 수 있음

**한계와 극복**
- TCP/IP 연결을 새로 맺어야 함 - `3 way handshake 시간 추가`
- 웹 브라우저로 사이트를 요청하면 HTML 뿐만 아니라 자바스크립트, css, 추가 이미지 등등 수 많은 자원이 함께 다운로드
- 지금은 `HTTP 지속 연결(Persistent Connections)로 문제 해결`
- HTTP/2, HTTP/3에서 더 많은 최적화

![image](https://user-images.githubusercontent.com/53653597/146183873-f0644230-ea33-4827-a055-b2cbf60a4796.png)

# HTTP 메시지

기본적인 HTTP 메시지 구조는 아래와 같다

![image](https://user-images.githubusercontent.com/53653597/146186017-e0e116f8-b6ed-43f3-b2a5-21dfbbf6ea47.png)

모든 메세지는 해당 구조와 같이 

    start-line
    header
    empty line(CRLF) - 반드시 있어야한다
    message body

4가지 부분으로 구성되어있다.

## 요청 메시지

![image](https://user-images.githubusercontent.com/53653597/146186374-de0e8397-71dc-4db8-be83-352c707f979f.png)

- start-line = request-line / status-line

    request-line = method SP(공백) request-target SP HTTP-version CRLF(엔터)

1. HTTP 메서드 (GET: 조회)
2. 요청 대상 (/search?q=hello&hl=ko)
3. HTTP Version

### 1. HTTP 메서드
- 종류: GET, POST, PUT, DELETE...
- 서버가 수행해야 할 동작 지정
    - GET: 리소스 조회
    - POST: 요청 내역 처리

### 2. 요청 대상
- absolute-path[?query] (절대경로[?쿼리])
- 절대경로= "/" 로 시작하는 경로
- 참고: *, http://...?x=y 와 같이 다른 유형의 경로지정 방법도 있다.

 ### 3. HTTP 버전 
- HTTP Version 
 
    ex)HTTP/1.1, HTTP/2, HTTP/3

## 응답 메시지

![image](https://user-images.githubusercontent.com/53653597/146187377-cfd54d4a-a40b-46d0-af8a-7bc769c027d8.png)

- start-line = request-line / **status-line**
- **status-line** = HTTP-version SP status-code SP reason-phrase CRLF
---
### HTTP 버전
- HTTP 상태 코드: 요청 성공, 실패를 나타냄
    - 200: 성공
    - 400: 클라이언트 요청 오류
    - 500: 서버 내부 오류
- 이유 문구: 사람이 이해할 수 있는 짧은 상태 코드 설명 글

### HTTP 헤더
- header-field = field-name ":" OWS field-value OWS
- HTTP 전송에 필요한 모든 부가정보
    - 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트(브라우저) 정보,
          서버 애플리케이션 정보, 캐시 관리 정보...
- 표준 헤더가 너무 많음
- https://en.wikipedia.org/wiki/List_of_HTTP_header_fields
- 필요시 임의의 헤더 추가 가능
- helloworld: hihi <- 이럴경우 약속된 응답자만이 받아 사용할수 있겠죠?

### HTTP 메시지 바디
- 실제 전송할 데이터
- HTML 문서, 이미지, 영상, JSON 등등 byte로 표현할 수 있는 모든 데이터 전송 가능

```javascript
마지막으로...

단순함 확장 가능
- HTTP는 단순하다. 스펙도 읽어볼만...
- HTTP 메시지도 매우 단순
- 크게 성공하는 표준 기술은 **단순하지만 확장 가능한 기술**
```