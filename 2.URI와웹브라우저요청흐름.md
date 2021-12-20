
# URI(Uniform Resource Identifier)

![image](https://user-images.githubusercontent.com/53653597/145810937-67d18442-039c-40ba-80e0-680fdf3eb3b0.png)


URI는 인터넷의 우편물 주소 같은 것으로, 정보 리소스를 고유하게 식별하고 위치를 지정할 수 있다.

그리고 이 URI에는 두 가지 형태가 있는데 이것이, URL, URN이라는 것이다.

URL 리소스가 있는 위치를 지정

URN 리소스에 이름을 부여

위치는 변할수 있지만 이름은 변하지 않는다

urn:isbn:8960777331 어떤 책의 isbn URN

URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음

앞으로 URI를 URL과 같은 의미로 이야기를 풀어가볼 생각이다.

Uniform: 리소스 식별하는 통일된 방식

• Resource: 자원, URI로 식별할 수 있는 모든 것(제한 없음)

• Identifier: 다른 항목과 구분하는데 필요한 정보

URI(URL) 분석

https://www.google.com/search?q=hello&hl=ko

URI(URL) 문법

scheme://[userinfo@]host[:port][/path][?query][#fragment]

• 프로토콜(https)

• 호스트명(www.google.com)

• 포트 번호(443)

• 패스(/search)

• 쿼리 파라미터(q=hello&hl=ko)

## **scheme:**//[userinfo@]host[:port][/path][?query][#fragment]

- 주로 프로토콜 사용
- 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙

    예) http, https, ftp 등등

- http는 80 포트, https는 443 포트를 주로 사용, 포트는 생략 가능
- https는 http에 보안 추가 (HTTP Secure)

## scheme://[**userinfo@**]host[:port][/path][?query][#fragment]

- userInfo는 URL 사용자 정보를 포함해서 인증

- 거의 사용하지 않음

## scheme://[userinfo@]**host**[:port][/path][?query][#fragment]

- 호스트명

- 도메인명 또는 IP주소를 직접 사용가능

   예) www.google.com

   예) 192.168.0.12

## scheme://[userinfo@]host[**:port**][/path][?query][#fragment]
- 포트(PORT)
- 접속 포트
- 일반적으로 생략, 생략시 http는 80, https는 443

## scheme://[userinfo@]host[:port][**/path**][?query][#fragment]
- 리소스 경로(path)  계층적 구조
  
  예)

    /home/file1.jpg

    /members
    
    /members/100, /item/iphone12

## scheme://[userinfo@]host[:port][/path][**?query**][#fragment]

- ?로 시작, &로 추가 가능, key=value 형태 

    예) ?keyA=valueA&keyB=valueB

- query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태


## scheme://[userinfo@]host[:port][/path][?query][**#fragment**]

https://docs.spring.io/spring-boot/docs/current/reference/html/gettingstarted.
html#getting-started-introducing-spring-boot

- fragment
- html 내부 북마크 등에 사용, 서버에 전송하는 정보 아님

# 웹 브라우저요청 흐름

자~ get방식의 요청 URL이 있다.
프로토콜이 https이고 
 
호스트는 www.google.com이며 
 
생략이 가능하지만 443이라는 포트까지 친절히 달려있으며
 
path는 /search

get에서 queryString인 ?q=hello&hl=ko까지! 알아볼수 있게 되었다.

 ![image](https://user-images.githubusercontent.com/53653597/145815314-ede088df-92de-4380-8bb9-3a6b9cbdf9ff.png)

 그럼 요청 메세지가 어떻게 되어있는지 살펴보자

![image](https://user-images.githubusercontent.com/53653597/145562655-2c6b60f6-b0c9-4ed7-a2b5-960706c850f7.png)


GET : 데이터를 달라는 요청이며

path부터 쿼리정보가 들어감 

뒤에 HTTP 버전정보 들어감

HOST 정보가 들어감




![image](https://user-images.githubusercontent.com/53653597/145816598-57f0a3ed-95a4-4a30-ad77-5cc105b6645c.png)

![image](https://user-images.githubusercontent.com/53653597/145816905-cb18c644-d9a6-4db9-b5e4-4ab8dbf9142c.png)

![image](https://user-images.githubusercontent.com/53653597/145816994-fa59ecab-e850-44ac-a7fd-ed0610db1c42.png)

응답 패킷을 살펴보자

어떤 HTTP버전을 받아서 그리고 컨텐츠의 타입을 선별해서 보여주고 html의 타입인 body값을 가진다 명시해준다.


![image](https://user-images.githubusercontent.com/53653597/145817058-9af47c48-a17f-4bee-9c0e-87cdb5a1b266.png)

![image](https://user-images.githubusercontent.com/53653597/145817186-29167ea0-9fb3-4fc0-bb8d-b54b94d3d02c.png)

![image](https://user-images.githubusercontent.com/53653597/145817269-69fbe6d5-745e-4bd6-9390-85d9fdbce0d4.png)