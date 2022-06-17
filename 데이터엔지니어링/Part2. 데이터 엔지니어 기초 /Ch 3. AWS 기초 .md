## AWS 기초

---

### 1. AWS CLI (Command Line Interface) 세팅

AWS Console에 접속하지 않고 unix 환경에서 어떤식으로 aws에 송신할 수 있는지 구축

- install awscli

<img width="1247" alt="스크린샷 2022-06-17 오전 1 26 21" src="https://user-images.githubusercontent.com/86764734/174119662-9597cbeb-9230-433a-bb79-1d049b4c594e.png">

<img width="604" alt="스크린샷 2022-06-17 오전 1 27 09" src="https://user-images.githubusercontent.com/86764734/174119790-cf71b2ad-853c-4a04-930f-e150c146d8d1.png">

- IAM(Identity and Access Management)

    내가 누구이고 어떤 access를 가지고 있는지 관리

    <img width="598" alt="스크린샷 2022-06-17 오전 1 36 12" src="https://user-images.githubusercontent.com/86764734/174121475-0d18ff58-cdb2-4b38-9a25-97dd003fbbb4.png">

    <img width="1194" alt="스크린샷 2022-06-17 오전 1 38 56" src="https://user-images.githubusercontent.com/86764734/174121983-7299f333-2352-42c4-95ab-1ade1275b53d.png">

    모든 단계를 마무리하고 나면 액세스 키 ID/비밀 액세스 키 확인할 수 있다.

    <img width="1183" alt="스크린샷 2022-06-17 오전 1 41 56" src="https://user-images.githubusercontent.com/86764734/174122844-0758c58e-2e8c-4cb8-a5c4-9d93a2cdc4d1.png">
    

- Configuring

<img width="721" alt="스크린샷 2022-06-17 오전 2 43 51" src="https://user-images.githubusercontent.com/86764734/174134067-6debfa54-15dc-4324-9221-f11510d27076.png">

여기서 오류발생..

<img width="1194" alt="스크린샷 2022-06-17 오전 2 49 13" src="https://user-images.githubusercontent.com/86764734/174134554-e1b5f677-52f2-4dc8-b9f7-0246480dd1c8.png">

WARNING 멘트그대로 코드 실행

<img width="1192" alt="스크린샷 2022-06-17 오전 2 49 44" src="https://user-images.githubusercontent.com/86764734/174134590-bcc772b2-690a-40ea-ba44-f8c061b4ff04.png">

또 다른 WARNING...
<img width="1189" alt="스크린샷 2022-06-17 오전 2 50 03" src="https://user-images.githubusercontent.com/86764734/174134628-11eca28b-0f3c-4665-ac08-dec218edf07e.png">

PATH 설정에도 되지 않아서 brew로 재설치
<img width="1187" alt="스크린샷 2022-06-17 오전 2 50 19" src="https://user-images.githubusercontent.com/86764734/174134677-3bbb6fee-c4cc-4c62-a3e1-bcefeced7abe.png">

성공..!
<img width="1193" alt="스크린샷 2022-06-17 오전 2 50 40" src="https://user-images.githubusercontent.com/86764734/174135011-9735e317-03fd-4b06-bac4-bb360453173e.png">

이렇게 하면 터미널 안에서 aws의 다양한 커맨드들을 통해서 접근가능한 환경을 구축할 수 있다. 

### Reference

---

- [AWS CLI 설치방법](https://devlos.tistory.com/37)

- [AWS Configure 오류](https://stackoverflow.com/questions/61026031/pip-installation-for-python3-problem-consider-adding-this-directory-to-path)