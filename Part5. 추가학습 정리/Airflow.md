## Airflow

---

Airflow는 복잡한 워크플로우를 프로그래밍 방식으로 작성해서, 스케줄링하고 모니터링할 수 있는 플랫폼.

데이터 파이프라인을 이루고 있는 ETL 스트립트들을 스케줄링 할 때 crontab, cloudwatch 등을 사용하는 곳이 많은데, 스크립트들이 많아지고 서로에 대한 의존성이 생기게 되면 컨트롤하기 어렵고, 기존 작업이 실패했을 때 다시 스크립트를 실행하려면 로그를 확인하고 실행해야 하는 등의 문제점이 생긴다. Airflow에는 서로에 대한 의존성을 표현할 수 있고, 스크립트가 실패했을 때 알람을 보내 확인하고 쉽게 수정 후 재시도할 수 있고, 이전 날짜 작업이 실패했을 때 그 날짜만 다시 실행하는 등 위의 문제점을 많이 해결한다.

### Apache Airflow란?

---

Airflow란 airbnb에서 만든 workflow management tool. workflow는 일련의 작업의 흐름이라고 말할 수 있다. 예를 들어 ETL 같은 경우는 데이터를 Extractaction -> Transformation -> Loading 하는 작업의 흐름이 있는데, 이런 workflow를 관리하는 툴이 Airflow. 여기러 관리라는 것은 워크플로우(workflow)를 작성, 스케줄링, 모니터링 하는 작업을 말한다. 

Airflow는 특징이 되는 컴포넌트들이 있으며 각 component들 간의 아키텍쳐는 아래와 같다.

<img width="652" alt="스크린샷 2022-05-06 오후 8 10 54" src="https://user-images.githubusercontent.com/86764734/167120893-614883cd-1d99-40b4-a54e-adae7d60dbd4.png">

Airflow는 크게 3가지의 구성요소로 이루어져 있다.

- Webserver

    Airflow의 로그를 보여주거나 스케줄러에 의해 생성된 DAG 목록, Task 상태등을 시각화해서 보여준다. 즉, UI를 통해 사용자에게 시각적으로 정보를 제공해주는 요소라 볼 수 있음


- Scheduler

    Airflow로 할당된 work들을 스케줄링 해주는 component. Scheduled된 workflow들의 triggering과 실행하기 위해서 executor에게 task를 제공해주는 역할을 수행

- Executor

    실행죽인 task를 handling하는 component. default 설치시에는 scheduler에 있는 모든 것들을 다 실행시키지만, production 수준에서의 executor는 worker에게 task를 push한다.


- Workers

    Airflow worker는 실제 task를 실행하는 주체자

- Airflow Dtabase

    Airflow에 있는 DAG, Task 등의 metadata를 저장하고 관리

또한, 아래와 같은 개념을 이용해 workflow를 작성한다.

- DAG(Diredted Acyclic Graph)

    비순환 그래프로써 순환하는 싸이클이 없는 그래프. 즉, 노드와 노드가 단방향으로 연결되어 있어 그 노드로 향하게 되면 돌아오지 않는다는 특성을 가지고 있다. Airflow에서는 이러한 DAG를 이용해 workflow를 구성하여 어떤 순서로 task를 실행시킬 것인지 dependency를 어떻게 표현할 것인지 등을 설정.

    <img width="644" alt="스크린샷 2022-05-06 오후 8 20 37" src="https://user-images.githubusercontent.com/86764734/167122077-9ab2ac7f-e870-4277-9c9a-098be1d3171a.png">





### Reference

---

- [Airflow 시작하기](https://data-engineer-tech.tistory.com/30)

- [Airflow란?](https://lsjsj92.tistory.com/631)
