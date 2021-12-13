URI와 웹 브라우저 요청 흐름에 대해
URI
URI는 로케이터(locator) 이름(name) 또는 둘 다 추가로 분류될 수 있다.

I L N

로케이터는 뭐고 이름은 뭐지?

자 I 는 큰 개념 식별한다라는 의미 이고 

L이 로케이터이고 리소스의 위치

N은 리소스의 이름

URI 단어 뜻 

Uniform 리소스 식별하는 통일된 방식
REsource 자원 URI로 식별할 수 있는 모든 것(제한 없음)

예를 들어서 실시간 교통정보 

Identifier  다른 항목과 구분하는데 필요한 정보  ----- 식별할 수 있다는 뜻 이다 뭐... 사람식별할때 주민번호로 식별합니다라고 하면 주민번호가 identifier가 되는 것이다.

URL Locator -
URN Name

URL 리소스가 있는 위치를 지정

URN  리소스에 이름을 부여

위치는 변할수 있지만 이름은 변하지 않는다

urn:isbn:8960777331 어떤 책의 isbn URN

URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음

앞으로 URI를 URL과 같은 의미로 이야기 하겠음

URI 분석

https://www.google.com/search?q=hello&hl=ko

URI 문법

scheme://[userinfo@]host[:port][/path][?query][#fragment]

주로 프로토콜 사용
프로토콜 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
http https ftp 등등
http는 80포트 https는 443포트를 주로 사용 포트는 생략 가능
https는 http에 보안 추가(HTTP secure)

userInfo는 URL 사용자 정보를 포함해서 인증
거의 사용하지 않음

호스트명
도메인명 또는 IP주소를 직접 사용가능

포트
접속 포트
일반적으로 생략, 생략시 http는 80, https는 443

리소스 경로(path)  계층적 구조
예)
/home/file1.jpg
/members
/members/100, /item/iphone12

key=value 형태
?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB
query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태

scheme://[userinfo@]host[:port][/path][?query][#fragment]
https://docs.spring.io/spring-boot/docs/current/reference/html/gettingstarted.html#getting-started-introducing-spring-boot
fragment
html 내부 북마크 등에 사용
서버에 전송하는 정보 아님

웹 브라우저요청 흐름
 DNS 조회 IP와 포트정보 찾아냄
 HTTP 요청 메시지 생성
 ![image](https://user-images.githubusercontent.com/53653597/145562655-2c6b60f6-b0c9-4ed7-a2b5-960706c850f7.png)

 Get : 데이터를 뭔가 달라는 거겠죠?
path부터 쿼리정보가 들어감 
뒤에 HTTP 버전정보 들어감
HOSt 정보가 들어감
