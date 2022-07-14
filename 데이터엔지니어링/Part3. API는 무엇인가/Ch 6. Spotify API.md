### Spotify App 생성 및 토큰 발급
---

#### Client Credentials Flow

![Untitled](https://user-images.githubusercontent.com/86764734/178995148-e837e9f1-165b-4f82-8823-e2c49ff01863.png)

![Untitled2](https://user-images.githubusercontent.com/86764734/178995268-6790db7a-0944-4c4f-9882-62f28f0f8677.png)

- expires_in: 3600 → 1시간 동안 유효한 access_token

#### APP만들기

- dashboard에 접속하여 로그인하고 새로운 앱만들기
- 이 앱을 통해  우리가 spotify api와 어떻게 작동하는지를 관장하는

![Untitled3](https://user-images.githubusercontent.com/86764734/178995811-6f749da9-9562-466b-88ce-27727c6f334e.png)

- authrization 하기 위해 client id와 secret key를 인코딩해서 spotify account service에 제공을 하면 한시간 동안 유요한 access key를 넘겨준다
- 이 access key를 이용해 spotify api에서 데이터를 제공받는다.

### Python 기본

---

```py
#패키지 import
import  sys # 파이선 시스템에 관련된


#파이선스크립트가 직접 실행되었을때 어떤 일을 해야하는지 main함수 안에 작성
def main():

    print('fastcampus')


#만약에 이름이 main일때 main func을 런. 즉, 실행하라
if __name__=='__main__':
    main()
#만약 그렇지 않고 sys처럼 spotify_api.py가 import가 됐을 경우에는 아래내용 프린트
else:
    print('this script is being imported')

##spotify_api.py 파일이 직접 실행이 안되고 어떤 모듈, 어떤 패키지화 되서 import가 되었을 때 

##quit()
```
![Untitled0](https://user-images.githubusercontent.com/86764734/178996940-9ef857e4-4a0b-4f6b-8f73-35f3a0adab0d.png)

### Python Requests 패키지
---
**API를 사용하기 위해서 Python이 제공하는 하나의 패키지**

![Untitled4](https://user-images.githubusercontent.com/86764734/178997354-fd75b301-33e1-44cf-a94b-628ad0f1098f.png)

- requests(패키지이름).**request**(requests가 제공하는 함수 부분)(method, url(endpoint), kwargs(parameters)

![Untitled5](https://user-images.githubusercontent.com/86764734/178998449-df8e7dbc-3c06-4d82-acd6-281166b5b7a5.png)

**requests 설치**
- [requests doc](https://requests.readthedocs.io/en/latest/api/)
```shell
[~/documents/fastcampus] git(main) ❱❱❱ pip3 install requests
```

- 만약 실행이 되지 않는다면 
```shell

[~/Documents/fastcampus] git(main) ❱❱❱ pip3 install --upgrade pip

[~/documents/fastcampus] git(main) ❱❱❱ sudo pip3 install requests
Password:
```

### API를 통해 데이터 요청 
---

- 우리는 **Client Credentials Flow**
- POST방식으로 요청할 것이며 HEADER PARAMETER안에는 Authorization이 들어와야한다.
    - Basic64: 어떤 스트링(client id, secert key)에 대해서 이 부분을 인코딩하는 방식

![Untitled6](https://user-images.githubusercontent.com/86764734/179001278-e698b6ae-46b4-4496-9a85-477a44f581ae.png)

```py
import sys
import requests #다운로드 후 
import base64 #파이썬이 기본적으로 가지고있는 패키 
import json
import logging # 에러나 로그를 관리하는 패키지

client_id = " "
client_secret = " "


def main():
    headers = get_headers(client_id, client_secret)
    #print(headers) >> {'Authorization': 'Bearer BQD6NcEwzwp2hY7OWEWq8Fq9krFsfAerd7OBmATVlC3Pry59oWtm3qzUUmO4eUOn_MU7B0xicrim3YGXTx6sciom5XY39TfZhYhVUU3Nt0CLqdXlaBw'}

	## spotify search API
    params = {
        "q": "BTS",
        "type": "artist"
    }

    r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)

    #print(r.status_code) >> 200
    #print(r.text)
   
def get_headers():
    #url - api endpoit
    endpoint = "https://accounts.spotify.com/api/token"
    
    #인코딩 .encode('utf-8')).decode('ascii')-> 파이썬3이상 사용할 때 추가적으로
    encoded = base64.b64encode("{}:{}".format(client_id, client_secret).encode('utf-8')).decode('ascii')

    headers = {
        "Authorization": "Basic {}".format(encoded) # 인코딩한 부분을 넣어준다
    }

    payload = {
        "grant_type": "client_credentials" # requests body parameter
    }

	# requests패키지를 통해서 method는 POST/ data=body parameter
    r = requests.post(endpoint, data=payload, headers=headers)

	#print(r.status_code) >> 200
    #print(r.text) >> {"access_token":"BQD-nIx3etjgBLL353-xhCEeSJiyvX-wUFllhwAcKUKZVF6GDemhs8lWVkkT_221Zg5vQuAXqD8xMHBNjXoWjhHZTyElwEyzWEEvN1hUIMRAqD1Eh6A","token_type":"Bearer","expires_in":3600}
	#print(type(r.text)) >> <class 'str'>
	#sys.exit(0) #0이면 에러없이 나온다.

    access_token = json.loads(r.text)['access_token']

		#print(type(aces_token)) >> <class 'dict'>

    headers = {
        "Authorization": "Bearer {}".format(access_token)
    }

    return headers


if __name__=='__main__':
    main()
```

- sys.exit()를 통해 코드가 정상적으로 작동하는지 확인
    - print(r.text) >> Authorization Guides에 나와있는 것 처럼 확인 가능

![Untitled7](https://user-images.githubusercontent.com/86764734/179001784-4ddfc00b-9211-4a85-b24e-6650985779e2.png)

- main 함수 실행 결과값

![Untitled8](https://user-images.githubusercontent.com/86764734/179001966-32ad521a-4b84-4a36-be9c-db856c6cf956.png)

### Status Code

---

**API로 요청했을 때 돌아오는 응답코드**

> 데이터 엔지니어링 관점에서 우리는 api를 지속적으로 사용하게 될 것. 어떤 경우에는 우리가 api를 통해서 요청을 할 때 실수를 할 때도 있겠지만, 서버의 문제로도 사용할 수 없을 수 있다. 이럴 때 이 상태코드를 통해 어떤 식으로 다양한 에러들을 핸들링 할 수 있는지 고민해야함
> - 대부분 상태코드는 documents제공. 그렇기 때문에 api를 요청했을 때 이런 에러 코드를 볼 수 있다는 것을 인지하고  python 스크립팅을 할 때 경우의 수들을 다 생각을 하고 진행해야 한다!  

![Untitled9](https://user-images.githubusercontent.com/86764734/179002947-79326cbf-7315-4b05-a0c4-d45085728791.png)

### 에러 핸들링
---
>에러 핸들링 같은 경우에는 필요에 따라서 엔지니어링을 통해서 어떤 식으로 관장할지에 대해서 생각을 해보고,
이런 식으로 자동화를 할건지 아니면 에러코드만 띄워놓고 알림을 해서 엔지니어가 고칠때까지 기다릴 것인지 이런부분을 고려한 다음에 이렇게 하나하나 적용을 해야함

```py
import sys
import requests #다운로드 후
import base64 #파이썬이 기본적으로 가지고있는 패키
import json
import logging # 에러나 로그를 관리하는 패키지

client_id = "f386fb9e14f842ef8abb6c72e34bf9bd"
client_secret = "2c02f03808e246908026b24b3f92c7a5"

def main():

    headers = get_headers(client_id, client_secret)
    #print(headers)

    ## spotify search API
    params = {
        "q": "BTS",
        "type": "artist"
    }

    r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)

    # 스크립트를 멈추고 나서 엔지니어가 왜 멈췄는지를 확인을 하고 다시 작업을 진행하는
    try:
        r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)

    except:
        #어떤 에러가 떳는지 표시
        logging.error(r.text)
        sys.exit(1)

    r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)



    if r.status_code != 200:
        logging.error(r.text)

        if r.status_code == 429:
            #헤더안의 Retry-After라는 부분이 있는데 그걸 json.loads로 불러와 retry_after라는 변수에 저장하겠다(몇 초일 것)
            retry_after = json.loads(r.headers)['Retry-After']
            #그 초 동안은 스크립트가 멈춰있겠다.
            time.sleep(int(retry_after))

            #그리고 나서 우리가 원했던 api요청을 다시 하겠다.
            r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)

            ## access_token expired
        elif r.status_code == 401:
            #다시 access_token을 요청해서 headers부분 새로고침
            headers = get_headers(client_id, client_secret)
            #새로운 헤더를 가지고 다시한번 api요청
            r = requests.get("https://api.spotify.com/v1/search", params=params, headers=headers)

        else:
            #그렇지 않은 에러의 경우 위에서 오류표시를 해줬기 때문에 종료하는 것으로 관리할 수 있다. 
            sys.exit(1)




def get_headers(client_id, client_secret):
    #url - api endpoit
    endpoint = "https://accounts.spotify.com/api/token"
    #인코딩 .encode('utf-8')).decode('ascii')-> 파이썬3이상 사용할때 추가적으로
    encoded = base64.b64encode("{}:{}".format(client_id, client_secret).encode('utf-8')).decode('ascii')

    headers = {
        "Authorization": "Basic {}".format(encoded)
    }

    payload = {
        "grant_type": "client_credentials"
    }

    r = requests.post(endpoint, data=payload, headers=headers)


    #str인 r값을 우리가 사용할 수 있게 변환을 해줘야 한다
    #json패키지의 loads라는 함수를 사용해서
    access_token = json.loads(r.text)['access_token']

    #print(type(access_token)) # dict로 변경된 것 확인

    headers = {
        "Authorization": "Bearer {}".format(access_token)
    }

    return headers


if __name__=='__main__':
    main()
```

- client_id 부분 오타냈을 때

<img width="648" alt="Untitled10" src="https://user-images.githubusercontent.com/86764734/179004808-5dc6ba3b-270f-49cf-bc6b-614dfc45bdfa.png">




