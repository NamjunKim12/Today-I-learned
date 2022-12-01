# 대칭키(Symmetric-Key)

## 📌대칭키란 ? 

- 양방향 암호화 방식의 일종으로, 암호화와 복호화에 사용되는 키가 동일한 암호화 방식(우리가 문을 열쇠하나로 여닫는 것과 동일하다.)
- 키 크기가 상대적으로 작고, 암호 알고리즘 내부 구조가 단순하여, 시스템 개발 환경에 용이하고, 비대칭키에 비해 암호화와 복호화의 속도가 빠르다. 따라서 크기가 큰 Data를 전송할때 사용된다.
- 교환 당사자 간 동일한 키를 공유해야하기 때문에 키 관리의 어려움이 있고, 키가 유출되면 암호화된 정보를 해독할 수 있기 때문에 보안에 취약하다.
- 디지털 서명 기법에 적용이 곤라고, 안정성을 분석하기 어려우며 중재자가 필요하다.


## 대칭키의 암호화 방식

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Fdd4UHB%2FbtraVqhyda9%2FKoiw2rKp2yVdJWiLBthiDk%2Fimg.png)


# 📌공개키(Public-Key)

## 공개키란 ?


- 양방향 암호화 방식의 일종으로, 암호화와 복호화에 사용되는 키가 다른 암호화 방식
- 공개키는 네트워크에 공유하고, 개인키는 본인이 보관하는 방식이다.
- 각 키의 관리와 분배가 용이하다. 개인키는 본인만 보관하므로, 키가 유출되는 위험이 없다. 공개키는 네트워크에 공유되므로, 키가 유출되더라도 개인키가 유출되지 않는 한, 암호화된 정보를 해독할 수 없다.
- 속도가 느리고, 키 크기가 상대적으로 크다. 따라서 크기가 작은 Data를 전송할때 사용된다.

## 공개키의 암호화 방식


![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FPQpX1%2FbtraSZq1AR9%2FRCKdYGJtoi8i9FkH0pkeek%2Fimg.png)

1. A가 웹상에 공개된 'B의 공개키'를 이용하여 암호화를 하여 B에게 전송한다.
2. B는 자신의 비밀키로 복호화한 평문을 확인, A의 공개키로 응답을 암호화하여 A에게 보낸다.
3. A는 자신의 비밀키로 암호화된 응답문을 복호화한다.

## 공개키와 대칭키 암호화 방식 비교

![image](https://t1.daumcdn.net/cfile/blog/27276A4B5503A14B2B?original)