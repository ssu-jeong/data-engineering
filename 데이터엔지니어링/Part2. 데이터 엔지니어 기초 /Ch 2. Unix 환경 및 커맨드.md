## Unix 환경 및 커맨드

---

### 1. Text Editor
파이썬 언어를 통해 스크립트 하게 될 때 작성하기위해 사용하는 에디터 

- emacs

- vi

- dim

- atom

### 2. Unix, Shell Commands

|Navigating Files and Directions|Files and Directories|Pipes and Fillters|
|-|-|-|
|cd path</br>ls path</br>pwd</br>..</br>.|cp old new</br>mkdir path</br>rm path</br>*</br>cp -r / rm -r(폴더는 -r)|cat(전체 프린트)</br>head(처음10줄 프린트)</br>tail(마지막10줄 프린트)</br>command>file</br>command>>file|
 
### 3. Shell Scripting 기본

<img width="598" alt="스크린샷 2022-06-16 오후 11 08 03" src="https://user-images.githubusercontent.com/86764734/174090072-62619472-0912-48dc-b094-b48758c49517.png">

<img width="592" alt="스크린샷 2022-06-16 오후 11 08 16" src="https://user-images.githubusercontent.com/86764734/174090124-b6eecbc1-1cc9-46bc-b224-2aa96c7ef670.png">

첫번째 sys를 통해서 example.py 뒤에 오는 것을 print 해달라는 말인데 뒤에 아무것도 없어서 생긴 오류

<img width="592" alt="스크린샷 2022-06-16 오후 11 19 09" src="https://user-images.githubusercontent.com/86764734/174090741-a42040a7-a31b-4a97-a57e-a9fc646152a0.png">

어떤 경우에 우리가 파이썬을 통해서 example.py에 1을 붙여가지고 먼저 run하고 싶고 그리고 나서 2를 실행하고 싶다고 할 때,

매번 들어와서 위 이미지처럼 작성하는 것이 아닌 Shell script를 이용할 수 있다!

<img width="590" alt="스크린샷 2022-06-16 오후 11 38 44" src="https://user-images.githubusercontent.com/86764734/174094915-3c07ce51-e63d-44d7-bdfb-50797ad96fbf.png">

먼저 새로운 파일 run.sh(shell script는 .sh) 하나 만든다 

<img width="1176" alt="스크린샷 2022-06-17 오전 12 04 51" src="https://user-images.githubusercontent.com/86764734/174100698-215d1204-6047-48a0-affd-2b097b3446d5.png">

```
#!/bin/bash 
> bash라는 shell을 통해서 작동하는 스크립트

chmod +x run.sh
> 권한 부여
```

<img width="1152" alt="스크린샷 2022-06-17 오전 12 12 43" src="https://user-images.githubusercontent.com/86764734/174102345-ddf674ac-95f7-47a6-add4-ba99603b193e.png">

```
output이 example.txt로 갔기 때문에 프린트 되지 않음.

목록을 보면 example.txt가 생성된 것 확인

cat example.txt를 실행했을 때 
> 첫번째 output을 지우고 두번째 output 저장
```

<img width="1149" alt="스크린샷 2022-06-17 오전 12 16 25" src="https://user-images.githubusercontent.com/86764734/174103251-ed255057-c994-423a-acbb-aef43f5a7ece.png">

```
python3 example.py >> example.txt
> 기존 output에 append
```

**왜 shell script 사용할까?**

우리가 다양한 커맨드를 순차적으로 실행해야 하는데 (예: aws의 다양한 서비스 사용, python 실행, 패키지 다운) 이런 부분들을 deploy.sh라는 파일안에 관리를 한다. 

<img width="1131" alt="스크린샷 2022-06-17 오전 12 22 06" src="https://user-images.githubusercontent.com/86764734/174104872-0879884d-91d3-4135-8a46-da824b06bcc6.png">

```
rm *.zip -> .zip으로 해당하는 모든 파일을 삭제

zip lisztfever.zip -r * -> 어떤 해당 폴더의 모든 파일에 대해서 lisztfever.zip으로 압축

aws s3 rm s3://areha/lisztferver/lisztfever.zip -> aws안에 s3라는 스토리지 안의 파일 삭제

aws s3 cp ./lisztfever.zip s3://areha/lisztferver/lisztfever.zip -> 그리고 다시 해당 파일을 복사

aws lambda update-function-code --function-name lisztfever --s3-bucket areha --s3-key lisztfever/lisztfever.zip -> aws 안에 있는 lambda function을 update
```