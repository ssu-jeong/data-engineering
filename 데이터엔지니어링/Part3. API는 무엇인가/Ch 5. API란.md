### REST API의 정의와 예제들
---

>#### Application Programming Interface

두개의 시스템이 서로 상호작용하기 위한 인터페이스

- 데이터를 주고 받는 인터페이스
- API라 하면 보통 REST API를 지칭 
    - 예) 계산기
        우리가 숫자를 입력하면 이볅한 값이 컴퓨터안에 어떠한 시스템으로 전송하고
        전송받은 값을 시스템이 계산 하여 결과값을 다시 보여준다.

>#### Web API란 웹을 통해 외부 서비스들로부터 정보를 불러오는 API

로컬안에서만 데이터를 주고받는 것이 아니라 각 서버(서비스)에 데이터를 요청하고 받는 것

- Application
    - 예) 내 컴퓨터에서 브라우저를 켜서 웹주소를 주게된다.
    - HTTP라는 프로토콜(경로)를 통해서 브라우저에 입력한 값이 어느 서버에 전달
- REST API
    - 그러면 이 서버는 전달된 내용을 인지하고 다시 리턴 값으로 나에게 전달
    - 요청된 HTML을 받고 하나의 웹사이트를 보게되는 것

이런 식으로 데이터도 주고 받을 수 있다. 

#### Authorization

---

>#### Authentication VS Authorization

- Authentication: Identity(정체)가 맞다는 증명
- Authorization: API를 통한 어떠한 액션을 허용(Header에 있다)

API가 Authentication을 하여도 어떠한 액션에 대해서는 Authorization을 허용하지 않을 수 있음

>#### API의 필수는 첫째도 시큐리티, 둘째도 시큐리티

**어떠한 시큐리티(보안) 방안이 없을 경우**:

- DELETE 리퀴스트를 통해서 다른 이용자의 정보를 지울 수도 있음
- 제 3자에세 데이터 유출로 이어질 수 있음
- 누가 API를 사용하는지, 어떤 정보를 가져가는지 트래킹 할 수가 없음

> #### API Key란 무엇인가?

**API Key란 보통 Request URL 혹은 Request 헤더에 포함되는 긴 스트링**
api에 접근권한이 있는지 확인하기위해 key값을 사용 - requst Url에 포함

만약 key값을 넣어주지 않으면 해당 화면이 확인된다. 

>#### Basic Auth

**Basic Auth의 경우 username:password와 같은 Credential을 Base64로 인코딩한 값을 Request Header안에 포함**

<img width="1071" alt="스크린샷 2022-07-12 오후 9 24 07" src="https://user-images.githubusercontent.com/86764734/178488906-d07f66d5-11c7-4baf-82e8-67d9929939b7.png">

> #### OAuth 2.0

- Server: the Spotify server
- Client: your application
- Resource: the end user data and controls

<img width="911" alt="스크린샷 2022-07-12 오후 9 26 42" src="https://user-images.githubusercontent.com/86764734/178489492-a98eb1f2-39b1-4831-b377-eae96b5656a4.png">

OAuth 2.0의 플로우 예
어떠한 앱을 페이스북으로 로그인하려할 때, 이름, 메일, 성별등을 제공하는데 동의하는지 메세지창을 볼 수 있는데 이게 end유저가 보는 화면
이렇게 동의를 하게되면 동의했다는 정보를 해당 앱이 페이스북에 전달하고 사용자가 동의했다는 정보를 확인하고 해당 정보를 앱에게 전달

### Spotify Web API 개요

---

- spotify에서 나의 앱으로 어떤 정보를 받아오겠다

<img width="1268" alt="스크린샷 2022-07-12 오후 9 37 21" src="https://user-images.githubusercontent.com/86764734/178491420-aed4ff40-1b0b-4790-8fac-ccd042ebfbf5.png">

- ENDPOINS REFERENCE(Spotify가 제공하는 하나의 API라고 볼 수 있음)
- 왼쪽의 목록들이 하나의 리소스(Albums라는 리소스, Artists라는 리소스)

- artist에 대한 정보가 Josn형태로 보여진다
<img width="1256" alt="스크린샷 2022-07-12 오후 11 01 44" src="https://user-images.githubusercontent.com/86764734/178508490-e0ef5d43-6300-4435-9f06-ba52b5537c82.png">

### Endpoints & Methods

---

> #### 'Resource'는 API를 통해 리턴된 정보 
> #### - 하나의 Resource안에 여러개의 Endpoints가 존재

<img width="943" alt="스크린샷 2022-07-12 오후 11 18 01" src="https://user-images.githubusercontent.com/86764734/178511964-cdcedf5d-b706-4498-9749-2e67580c64b2.png">

<img width="551" alt="스크린샷 2022-07-12 오후 11 21 11" src="https://user-images.githubusercontent.com/86764734/178513476-9a864fb6-b53d-48ac-bb3c-4fade8fbe873.png">

> #### Endpoint: Resource를 엑세스하는 경로/방법
> #### Method: Resource 접근에 허용된 행위 (GET, POST, PUT, DELETE 등)

- 이 Endpoint를 통해서 어디에 접근하여 어떤 Method를 행할 것인가

<img width="764" alt="스크린샷 2022-07-12 오후 11 26 42" src="https://user-images.githubusercontent.com/86764734/178513989-35ce8e7d-5af8-4a53-b511-8be6ee02012d.png">

> #### Methods 정의

- GET: 해당 리소스를 조회하고 정보를 가져온다
- HEAD: GET방식과 동일하나 응답코드와 HEAD만 가져온다(안에 데이터는 빼고 -> 작동확인용)
- POST: 요청된 리소스를 생성한다
- PUT: 요청된 리소스를 업데이트한다
- DELETE: 요청된 리소스를 삭제한다

<img width="939" alt="스크린샷 2022-07-12 오후 11 47 38" src="https://user-images.githubusercontent.com/86764734/178518616-da88a96e-5995-4c35-ae95-260177ffc115.png">

GET이라는 방법을 통해서 해당 api한테 요청
- {id}: 해당 artist id로 변환을 해줘라(path parameter)

### Parameters

---

> #### Parameters는 Endpoint를 통해 리퀘스트 할 때 같이 전달하는 옵션들

해당 엔트포인트에 어떤 메소드를 통해서 리퀘스트 했을 때 같이 전달하는 옵션들

> #### 4가지 Parameter 타입들

- Request Body는 주로 post할 때 더 많이 사용

<img width="1016" alt="스크린샷 2022-07-12 오후 11 53 48" src="https://user-images.githubusercontent.com/86764734/178519919-265280ab-2b80-4e99-89c7-c5c7ee8500c7.png">


<img width="1152" alt="스크린샷 2022-07-12 오후 11 56 56" src="https://user-images.githubusercontent.com/86764734/178520627-a6e8d45f-c1e3-4269-94f5-575fccee3b36.png">

해당 Header에는 Authorization을 넣어줘야하고, Path Parameter에는 id값을 넣어줘야한다