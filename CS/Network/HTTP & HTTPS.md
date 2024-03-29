# HTTP

## 📌HTTP 란?

- HyperText Transfer Protocol의 약자로서, 문서를 전송하기 위한 통신규약(Protocol)을 뜻한다. 
- `서버`와 `클라이언트`의 사이에서 어떻게 메시지를 교환할지를 정해놓은 규칙이다.
- 요청`(Request)`와 응답`(Response)`으로 이루어져 있다.
- 브라우저에서 인터넷 주소 맨 앞에 들어가는 **http://** 가 바로 이 프로토콜을 사용해서 정보를 교환하겠다는 것이다.

## 📌HTTP의 특징

- HTTP는 요청과 응답으로 이루어져 있다. 클라이언트가 요청을 하면 서버가 응답을 하는 구조이다. 
- 상태가 없는 프로토콜로서, 개별의 통신은 독립적으로 이루어진다.
- 즉 서버가 클라이언트의 상태를 유지하지 않기 때문에 요청을 보낼 때마다 모든 데이터들을 매번 보내야한다.
- 로그인과 같이 상태를 유지해야만 하는 경우는 쿠키와 서버 세션 등을 사용해서 상태를 유지한다.
- 우리가 네이버에 접속을 했다고 가정하면, 클라이언트는 GET 명령을 네이버의 서버에 전송하고,
- GET요청을 받은 서버는 응답 코드와 메시지를 전송한다. 클라이언트는 이를 받아서 화면에 렌더링한다.

## 📌 HTTP 메시지
- 서버 - 클라이언트 간 통신시 텍스트, 이미지 및 파일, JSON 등 모든 것을 **HTTP 메시지**를 통해 전송한다.
- 시작줄, 헤더(HTTP 헤더), 본문(HTTP 메시지 바디)으로 구성된다.

### 1️⃣시작줄(start-line)

#### Request 시

```bash
request-line = method SP request-target SP HTTP-version CRLF(엔터)
```
- 요청시 해당하는 시작줄은 **request-line**이다.
- method는 서버가 수행해야할 동작을 지정한다. (GET, POST 등);
- request-target은 요청이 전송되는 목표 주소를 가리킨다.
- HTTP-version은 HTTP의 버전을 명시한다.

#### Response 시

```bash
status-line = HTTP-version SP status-code SP reason-phrase CRLF
```
- 응답시 해당하는 시작줄은 **status-line**이다.
- status-code는 요청이 성공했는지 실패했는지를 나타낸다.
- reason-phrase는 status-code를 설명하는 문구이다.

### 2️⃣헤더(HTTP Header)

<img width="403" alt="image" src="https://user-images.githubusercontent.com/69416561/201112539-e9e8d5a1-80f9-4db0-80b2-66aabdbe3ba1.png">

- 헤더는 요청과 응답에 대한 부가적인 정보를 담고 있으며, 크롬 개발자 도구에서 확인할 수 있다.
- 헤더는 여러개가 올 수 있으며, key-value 형태로 이루어져 있다.

### 3️⃣본문(HTTP message body)
- HTTP가 전송하는 데이터를 담고 있다.
- byte 단위로 표현할 수 있는 모든 데이터를 담을 수 있다.

## 📌HTTP의 요청 메시지 목록

- HTTP 요청 메시지는 크게 8가지로 구분할 수 있다.
- GET : 클라이언트가 서버에게 URL에 해당하는 정보를 요청할 때 사용한다.
- HEAD : GET과 비슷하지만, 응답으로 헤더만 받는다.
- POST : 클라이언트가 서버에서 처리할 수 있는 자료를 보낸다. 예를 들어, 회원가입, 로그인, 글쓰기 등이 있다.
- PATCH : 클라이언트가 서버에게 지정한 URL에 해당하는 정보를 수정할 때 사용한다.
- PUT : 클라이언트가 서버에게 지정한 URL에 지정한 정보를 저장할 때 사용한다.
- DELETE : 클라이언트가 서버에게 지정한 URL에 해당하는 정보를 삭제할 때 사용한다.
- CONNECT : 클라이언트가 서버에게 프록시를 통해 통신할 때 사용한다.
- OPTIONS : 클라이언트가 서버에게 지원하는 메서드를 요청할 때 사용한다.

## 📌HTTP의 응답 코드 목록

-  HTTP 응답 코드는 크게 5가지로 구분할 수 있다. 해당 항목에서는 자주 사용하는 응답 코드만 기재한다.
#### 1️⃣ 100 번대 코드 : 요청을 받았고, 작업을 진행 중 이라는 의미이다. HTTP/1.1에서는 100번대 코드가 더이상 사용되지 않는다.
    - 101 Switching Protocols : 클라이언트가 서버에게 프로토콜을 전환하라고 요청했을 때 사용한다. 예를 들어, 클라이언트가 웹소켓을 사용하고 싶을 때 사용한다.
  
#### 2️⃣200 번대 코드 : 작업을 성공적으로 받았고, 이해했으며, 받아들여졌다는 의미이다. 200, 204, 206을 제외하고는 볼일이 거의 없다.

#### 3️⃣300 번대 코드 : 이 요청을 완료하기 위해서는 리다이렉션이 이루어져야 한다는 의미이다. 

#### 4️⃣400 번대 코드 : 이 요청은 올바르지 않다는 의미이다. **클라이언트가 잘못된 요청을 했을 때 사용**한다.
    - 400 Bad Request : 클라이언트가 잘못된 요청을 했을 때 사용한다.
    - 401 Unauthorized : 클라이언트가 인증되지 않았을 때 사용한다.
    - 403 Forbidden : 클라이언트가 요청을 거부당했을 때 사용한다.
    - 404 Not Found : 클라이언트가 요청한 자원을 찾을 수 없을 때 사용한다.
    - 408 Request Timeout : 요청 중 서버가 일정 시간동안 응답을 하지 않았을 때 사용한다.

#### 5️⃣500 번대 코드 : **서버에 오류가 발생했을 때 사용**한다.
    - 500 Internal Server Error : 서버에 오류가 발생했을 때 사용한다.
    - 502 Bad Gateway : 서버가 게이트웨이나 프록시 역할을 하고 있을 때, 게이트웨이나 프록시가 잘못된 응답을 받았을 때 사용한다.
    - 503 Service Unavailable : 서버가 일시적으로 오류가 발생했을 때 사용한다.
    - 504 Gateway Timeout : 게이트웨이가 연결된 서버로부터 응답을 받을 수 없었을 떄 사용한다. 

### 6️⃣비표준 응답코드
    - 420 Enhance Your Calm : 트위터에서 사용하는 비표준 응답코드로, 클라이언트가 너무 많은 요청을 보내고 있을 때 사용한다.
    - 520 Unknown Error : 클라우드플레어에서 사용하는 비표준 응답코드로, 서버가 오류를 반환했을 때 사용한다.
    - 521 Web Server Is Down : 클라우드플레어에서 사용하는 비표준 응답코드로, 서버가 다운되었을 때 사용한다.

# 📌HTTPS

## HTTPS란?
- HTTPS는 HTTP에 SSL(보안 소켓 계층)이라는 암호화 프로토콜을 추가한 것이다.
- 공개키 암호화 방식을 사용하여 텍스트를 암호화한다.
- SSL 인증서는 사용자가 사이트에 제공하는 정보를 암호화 하는데, 이렇게 전송된 데이터는 중간에서 누가 훔쳐낸다고 하더라도 데이터가 암호화 되어 있어 해독할 수 없다.
- 우리나라의 경우, 인터넷 결제나 인터넷 뱅킹 등의 개인정보 입력이 필요한 사이트에서는 법접으로, 반드시 HTTPS를 사용해야한다.
- HTTP를 HTTPS로 전환하면 SEO 측면에서도 이점이 있다.
- 모든 사이트에서 텍스트를 암호화시켜 전송하면 과부하가 걸려 속도가 느려질 수 있다.
- HTTPS를 지원한다고 해서 무조건 안전한 것은 아니다. 
- 신뢰할 수 있는 CA 기업이 아니라 자체적으로 인증서를 발급할 수도 있고, 신뢰할 수 없는 CA 기업을 통해서 인증서를 발급받을 수도 있기 때문이다.

## HTTPS 통신 흐름
1. 애플리케이션 서버(A)를 만드는 기업은 HTTPS를 적용하기 위해 공개키와 개인키를 만든다.

2. 신뢰할 수 있는 CA 기업을 선택하고, 그 기업에게 내 공개키 관리를 부탁하며 계약을 한다.

- CA란? : Certificate Authority로, 공개키를 저장해주는 신뢰성이 검증된 민간기업

3. 계약 완료된 CA 기업은 해당 기업의 이름, A서버 공개키, 공개키 암호화 방법을 담은 인증서를 만들고, 해당 인증서를 CA 기업의 개인키로 암호화해서 A서버에게 제공한다.

4. A서버는 암호화된 인증서를 갖게 되었다. 이제 A서버는 A서버의 공개키로 암호화된 HTTPS 요청이 아닌 요청이 오면, 이 암호화된 인증서를 클라이언트에게 건내준다.

5. 클라이언트가 main.html 파일을 달라고 A서버에 요청했다고 가정하자. HTTPS 요청이 아니기 때문에 CA기업이 A서버의 정보를 CA 기업의 개인키로 암호화한 인증서를 받게 된다.

6. CA 기업의 공개키는 브라우저가 이미 알고있다. (세계적으로 신뢰할 수 있는 기업으로 등록되어 있기 때문에, 브라우저가 인증서를 탐색하여 해독이 가능한 것)

7. 브라우저는 해독한 뒤 A서버의 공개키를 얻게 되었다. 이제 A서버와 통신할 대는 얻은 A서버의 공개키로 암호화해서 요청을 날리게 된다.

## 유용한 레퍼런스
[ZeroCho-HTTP](https://www.zerocho.com/category/HTTP)
