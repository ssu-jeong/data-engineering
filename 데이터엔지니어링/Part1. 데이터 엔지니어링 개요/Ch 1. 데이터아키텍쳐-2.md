# 데이터 엔지니어링 개요


## Ch 1. 데이터 아키텍쳐

### 4. 데이터 파이프라인이란

---

1. **데이터 파이프라인**

    데이터 파이프라인이란 데이터를 한 장소에서 다른 장소로 옮기는 것을 의미

    - API -> Database

    - Database -> Database

    - Database -> BI Tool

2. **데이터 파이프라인이 필요한 경우**

    - 다양한 데이터 소스들로부터 많은 데이터를 생성하고 저장하는 서비스

    - **데이터사일로**: 마케팅, 어카운팅, 세일즈, 오퍼레이션 등 각 영역(부서)의 데이터가 서로 고립되어 있는 경우

    - 실시간 혹은 높은 수준의 데이터 분석이 필요한 비지니스 모델

    - 클라우드 환경으로 데이터 저장

3. **데이터 파이프라인 예시**

    <img width="971" alt="S3_data_pipe_line_exaple" src="https://user-images.githubusercontent.com/86764734/173845878-8a3e7178-b754-48af-b6dc-2edc2899afa5.png">   

    - 여러가지를 고려해서 아키텍쳐를 구성


    <img width="760" alt="스크린샷 2022-06-15 오후 10 56 34" src="https://user-images.githubusercontent.com/86764734/173845293-bdf920d8-af8d-49aa-a9d0-110995abba1d.png">

    - spotify API를 통해서 MySQL 데이터베이스로 데이터를 가져오는 것 또한 하나의 데이터파이프라인

4. **데이터 파이프라인 구축시 고려사항**

    - **Scalability**: 데이터가 기하급수적으로 늘어났을 때도 작동하는가

    - **Stability**: 안정성이 있는가 (에러, 데이터 플로우 등 다양한 모니터링 관리)

    - **Security**: 데이터 이동간 보안에 대한 리스크는 무엇인가


### 5. 자동화의 이해

---

1. **데이터 프로세싱 자동화란?**

    필요한 데이터를 **추출, 수집, 정제**하는 프로세싱을 최소한의 사람 인풋으로 머신이 운영하는 것을 의미

    예) Spotify 데이터를 하루에 한번 API를 통해서 클라우드 데이터베이스로 가져온다고 했을 때 매번 사람이 데이터 파이프라인을 작동하는 것이 아니라 크론탭 등 머신 스케쥴링을 통해 자동화

2. **자동화를 위해 고려할 사항**

    - 데이터 프로세싱 스텝들

    - 에러 핸들링 및 모니터링

    - 트리거 / 스케쥴링

3. **데이터 프로세싱 스텝들**

    <img width="859" alt="스크린샷 2022-06-15 오후 11 19 24" src="https://user-images.githubusercontent.com/86764734/173850343-46f2282d-94db-4d8a-a9c0-ed64de94c0eb.png">

    - Data Validater: 데이터가 좋은 데이터인지 아닌지 확인하는 과정

    - EMR ETL Cluster Starter: 데이터 정제, 추출 프로세스

4. **에러 핸들링 및 모니터링**

    Python Logging Package

    ```py
    import logging
    logging.basicConfig(filename='example.log', level=logging.DEBUG)
    logging.debug('This message should go to the log file')
    logging.info('So should this')
    logging.warning('And this, too')
    ```

    Cloud Logging Systems

    - AWS Cloudwatch
    - AWS Data Pipeline Errors
    
5. **트리거 / 스케쥴링**

    어떠한 작업이 끝났을 때 그다음 작업이 어떻게 트리거 될 것인지, 어떻게 지속적으로 작업이 일어나게 스케쥴링

    <img width="950" alt="스크린샷 2022-06-15 오후 11 34 57" src="https://user-images.githubusercontent.com/86764734/173853921-3c93afbc-d6ff-478e-ab14-e860e8361909.png">


### 6. 엔드 투 엔드 아키텍쳐 예시들

---

1. **빅데이터 처리를 위한 데이터 레이크**



    <img width="1060" alt="스크린샷 2022-06-15 오후 11 37 48" src="https://user-images.githubusercontent.com/86764734/173854557-940fff88-a5e9-47a1-85ae-00c98e1c3a2f.png">

2. **넷플릭스 데이터 시스템 예시**

    <img width="1072" alt="스크린샷 2022-06-15 오후 11 40 57" src="https://user-images.githubusercontent.com/86764734/173855301-b1f099ae-6d3b-474b-b3d8-355199bb8057.png">

    - kafka: 실시간 데이터를 수집하는데 최적화된 오픈소스

    - S3: 데이터 베이스/ 백업용으로 사용

3. **우버 데이터 아키텍쳐**

    <img width="1017" alt="스크린샷 2022-06-15 오후 11 43 34" src="https://user-images.githubusercontent.com/86764734/173855883-b9f238fe-328e-4be1-b75c-7381448bba79.png">

    - Hudi: data parquet

    - 분석하는 환경에서 최적화 될 수 있도록 다양한 변형을 시도하여 저장


### 7. Spotify 프로젝트 아키텍쳐

---

1. **Ad hoc VS. Automated**

    - Ad hoc 분석 환경 구축은 서비스를 지속적으로 빠르게 변화시키키 위해 필수적 요소

    - 이니셜 데이터 삽입, 데이터 Backfill 등을 위해 Ad hoc 데이터 프로세싱 시스템 구축 필요

    - Automated: 이벤트, 스케쥴 등 트리거를 통해 자동화 시스템 구축

2. **아티스트 관련 데이터 수집 프로세스**

    <img width="1203" alt="스크린샷 2022-06-16 오전 12 13 36" src="https://user-images.githubusercontent.com/86764734/173863159-4558e74b-8381-4cd6-91b7-91432152d135.png">


3. **데이터 분석 환경 구축**

    <img width="1021" alt="스크린샷 2022-06-16 오전 12 17 36" src="https://user-images.githubusercontent.com/86764734/173863915-7fdcf043-07ff-40e6-9cad-5878f114461f.png">

4. **서비스 관련 데이터 프로세스**

    <img width="1106" alt="스크린샷 2022-06-16 오전 12 20 04" src="https://user-images.githubusercontent.com/86764734/173864437-036b3bd4-d195-41b3-b724-70c817b9b81b.png">

    - S3에 있는 데이터를 Spark가 컴퓨팅 시작

        - 노래 분석을 통해 유사도 계산

    - 계산된 데이터가 NoSQL에 저장 

        - 추후에 어떤 서비스로 이용할지 모르기 때문에 스키마가 없는 NoSQL 데이터베이스를 사용
