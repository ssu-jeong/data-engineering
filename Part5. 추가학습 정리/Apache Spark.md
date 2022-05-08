## Apache Spark

---

빅 데이터 워크로드에 주로 사용되는 오픈소스 분산처리 시스템. Apache Spark는 빠른 성능을 위해 인 메모리 캐싱과 최적화된 실행을 사용하며, 일반 배치 처리, 스트리밍 분석, 기계학습, 그래프 데이터베이스 및 임시 쿼리를 지원한다.

하둠 YARN상의 Apache Spark는 Amazon EMR에서 기본적으로 지원하므로, AWS Management Console, AWS CLI 또는 Amazon EMR API를 통해 관리형 Apache Spark 클러스터를 빠르고 간편하게 생성할 수 있다. 그 밖에도 Amazon EMR 파일 시스템(EMRFS)을 ㅅ용한 빠른 Amazon S3연결, Amazon EC2 스팟 시장과의 통합, 클러스터에서의 인스턴스를 손쉽게 추가 또는 제거하는 크기 조정 명령 등을 비롯한 추가적인 Amazon EMR 기능을 활용할 수 있다. 또한 Apache Spark를 통해 데이터를 탐색할 수 있도록 Apache Zeppelin을 사용하여 대화형 협업 노트북을 생성할 수 있다. 

### 기능 및 장점

---

**빠른성능**
방향성 비순환 그래프(DAG) 실행 엔진을 사용함으로써 데이터 변환에 대한 효율적인 쿼리 계획을 생성할 수 있다. 또한 입력, 출력 및 중간 데이터를 인 메모리에 RDD(Resilient Distributed Dataset)로 저장하므로, I/O 비용 없이 반복 또는 대화형 워크로드를 빠르게 처리하고 성능을 높일 수 있다. 

**애플리케이션 신속 개발**
기본적으로 Java, Scala 및 Python을 지원하므로, 애플리케이션을 구축할 수 있도록 다양한 언어를 제공한다. Spark SQL 모듈을 사용하여 SQL 또는 HiveQL 쿼리를 Apache Spark에 제출할 수 있다. 애플리케이션을 실행하는 것 외에도, Apache Spark API를 Python과 대화식으로 사용하거나 클러스터의 Apache Spark 셀에서 Scala를 직접 사용할 수 있고 Zepplin을 사용하여 데이터 탐색과 시각화를 위한 대화형 협업 노트북을 생성할 수도 있다.

**다양한 워크플로 생성**
Apache Spark에는 기계 학습(MLlib), 스트림 처리(Spark Streaming) 및 그래프 처리(GraphX)용 애플리케이션을 구축하는 데 도움이 되는 몇 가지 라이브러리가 포함되어있다. 이러한 라이브러리는 Apache Spark 에코시스템과 긴밀하게 통합되고, 다양한 사용 사례를 해결하는 데 바로 활용 가능.

**Amazon EMR 기능 집합과 통합**
Amazon EMR Step API로 Apache Spark 작업을 제출하고, EMRFS와 함께 Apache Spark를 사용하여 Amazon S3에 있는 데이터에 직접 액세스하며, Amazon EC2 스팟 용량을 사용하여 비용을 절감하고, 워크로드에 맞춰 장기 실행 또는 휘발성 클러스터를 시작할 수 있다. Amazon EMR은 하둡 YARN에서 Apache Spark를 설치 및 관리하고, 사용자는 클러스터에 다른 하둡 에코시스템 애플리케이션을 추가할 수도 있다.