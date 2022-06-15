# 데이터 엔지니어링 개요

---

## 데이터 아키텍쳐

### 1. 데이터 엔지니어링의 필요성

- 문제를 해결하기 위한 가설 검증 단계

    |문제 >|데이터 분석 >|가설 수립 >|실험 및 테스팅>|최적화|
    |---|--------|-------|----------|----|
    |구축되어야하는 시스템|- 분석할 데이터 </br> - 데이터 분석 조직||- 통계적 실험 설계 </br> - 클린한 테스팅 환경|데이터 기반 자동화 시스템|
 
    모든 비지니스가 동일한 데이터 분석 환경을 갖출 수가 없고 성장 단계에 따라 선택 집중해야 하는 분석 환경이 다르다.

- 페이스북과 같은 유저 경험이 중요한 비지니스의 경우 처음부터 데이터 시스템 구축이 성공의 열쇠

    - **필요한 데이터 예시**

        유저정보:
        - ID
        - Last Login

        컨텐츠 정보:
        - content Id
        - Content Type
        - Categories

        유저액션:
        - Impression/Clik
        - Position in Feed
        - Comment, Like, etc

- 이커머스는 마케팅, CRM, 물류 데이터 분석을 통해 전략 수립

    - **필요한 데이터 예시**

        - 마케팅 채널별 비용 데이터
        - CRM 데이터
        - 각종 물류 데이터

- 처음부터 모든 인력을 갖추고 분석 환경을 갖출 수 없다. 

    <img width="674" alt="스크린샷 2022-06-15 오전 12 04 11" src="https://user-images.githubusercontent.com/86764734/173825992-c9e3c37f-c8ac-4e3b-94db-4684b3d6bac8.png">

    - 성장 단계 별로 필요한 분석 환경을 갖추는 것이 키

        - custom 환경

        - 자동화

        - Data Integration

---

### 2. 데이터 아키텍쳐 시 고려사항

</br>

1. **비지니스 모델 상 가장 중요한 데이터는 무엇?**

    <img width="679" alt="스크린샷 2022-06-15 오후 9 20 09" src="https://user-images.githubusercontent.com/86764734/173826015-4c1471ea-f66d-4433-b811-879555427958.png">

    우리가 어떤 데이터에 집중하고 어떤 가치를 만들 것인가?

    - 데이터비용

        - 소요시간
        - 엔지니어 리소스
        - 과금

    - 비니지스 임팩트

</br>

2. **데이터 거버넌스 (Data Governance)**

    항상 데이터 아키텍쳐를 진행할 때 고려해야할 부분 

    **원칙 (Principle)** 

    데이터를 어떻게 유지관리하며 가져올 것인가

    - 데이터를 유지 관리하기 위한 가이드

    - 보안, 품질, 변경관리

    **조직 (Organaization)**

    데이터를 누가 어떻게 관리할 것인가

    - 데이터를 관리할 조직의 역할과 책임

    - 데이터 관리자, 데이터 아키텍트

    **프로세스(Process)**

    어떤 식으로 관리하고 모니터링 할 것인가

    - 데이터 관리를 위한 시스템

    - 작업 절차, 모니터 및 측정

</br>

3. **유연하고 변화 가능한 환경 구축**

    - 특정 기술 및 솔루션에 얽매여 있지 않고 **새로운 테크를 빠르게 적용할 수 있는** 아키텍쳐를 만드는 것

    - 생성되는 데이터의 형식이 변화할 수 있는 것처럼 그에 맞는 **툴과 솔루션도 빠르게 변화할 수 있는 시스템을 구축**

</br>

4. **Real Time(실시간) 데이터 핸들링이 가능한 시스템**

    밀리세컨 단위의 스트리밍 데이터가 됐건 하루에 한번 업데이트 되는 데이터든 **모든 스피트의 데이터를 핸들링**

    - Real Time Streaming Data Processing

    - Cronjob

    - Serverless Trggered Data Processing

</br>

5. **시큐리티**

    내부와 외부 모든 곳에서부터 발생할 수 있는 **위험요소**들을 파악하여 어떻게 데이터를 안전하게 관리할 수 있는지 **아키텍쳐**안에 포함

</br>

6. **셀프 서비스 환경 구축**

    데이터 엔지니어 한명만 엑세스가 가능한 데이터 시스템은 **확장성**이 없는 데이터 분석 환경

    - BI Tools

    - Query System for Analysis

    - Front-end data application

### 3. 데이터 시스템의 옵션들

1. **API의 시대**

    마케팅, CRM, ERP 등 다양한 플랫폼 및 소프트웨어들은 여러 데이터들을 데이터베이스 혹은 데이터시스템에 구축하고, API(하나의 송신 방법)를 통해 데이터를 주고 받을 수 있는 환경을 구축하여 추후에 애플리케이션을 만들 수 있도록 생태계를 생성

    <img width="725" alt="스크린샷 2022-06-15 오후 10 11 08" src="https://user-images.githubusercontent.com/86764734/173835165-46c35348-ab87-44ae-ae58-7bfff3ca9eca.png">

    api를 통해 바로 그쪽 데이터베이스에 있는 데이터를 가지고 서비스를 할 수도 있고 그 api를 통해 데이터를 받아 우리 데이터 베이스에 저장을 하고 분석환경을 구축할 수도 있다.  

<br/>

2. **Relational Databases**

    - 데이터의 관계도를 기반으로 한 디지털 데이터베이스로 데이터의 저장을 목적으로 생겨남

    - SQL이라고 하는 스탠다드 방식을 통해 자료를 열람하고 유지

    - 현재 대부분의 서비스들이 가장 많이 쓰고 있는 데이터 시스템

3. **NoSQL Databases**
    
    기존의 데이터베이스들의 형식, 구조적인 한계점을 극복하고 비용적인 문제를 해결할 수 있다.

    - Not Only SQL

    - Unstructured, Schema Less Data

    - Scale horizontally (예: 메신저)

    - Highly scalcble / Less expensive to maintain

4. **Hadoop / Spark / Presto 등 빅데이터 처리**

    Distributed Storage System / MapReduce를 통한 병렬 처리

    **Spark:**

    - Hadoop의 진화된 버전으로 빅데이터 분석 환경에서 Real Time 데이터를 프로세싱하기에 더 최적화

    - Java, Python, Scala를 통한 API를 제공하여 애플리케이션 생성

    - SQL Query 환경을 서포트하여 분석가들에게 더 각광

5. **서버리스 프레임워크**

    - Triggerd by http requests, database events, queuing services

    - Pay as you use (항상 서버를 띄워 놓고 있지 않기 때문에)

    - Form of functions (함수/알고리즘)

    - 3rd Party 앱들 및 다양한 API를 통해 데이터를 수집, 정제하는데 유용