# Kinesis

---

## Amazon Kinesis?

실시간으로 비디오 및 데이터 스트림을 쉽게 수집, 처리 및 분석하기 위한 AWS(Amazon Web Service)에서 제공하는 클라우드 서비스

### Kinesis에서 제공하는 기능

- Data Stream
    
    데이터 스트림으로 스트리밍 데이터 수집
    
- Data Firehose
    
    데이터 전송 스트림으로 스트리밍 데이터를 처리 및 전송
    
- Data Analytics
    
    데이터 분석 어플리케이션을 사용하여 스트리밍 데이터 분석

[*stream이란?](https://medium.com/@su_bak/technology-data-stream-streaming%EC%9D%B4%EB%9E%80-3762b6d48720)

---

### Kinesis Data Stream?

![1_7wgJdbetiQAJFLOq4kpXxg](https://user-images.githubusercontent.com/86764734/165319651-f5a5de57-c62d-4644-a327-ff57adf39c60.png)

Kinesis Data Stream이란 대량의 데이터를 실시간으로 수집, 처리하는 서비스. 내부적으로 샤드로 구성되어 있으며 이를 동적으로 증가/감소할 수 있고 샤트 수에 따른 보장된 전송시간을 제공하기 때문에 이점이 많음.

주로 연속적으로 생간되는 대랑의 데이터 소스(1MB이하)를 처리해야하는 파이프라인에 사용하기 좋다.

이와 비슷한 서비스로 Kafka, Rabbitmq등이 있고 이와 구별되는 Kinesis Data Stream의 특징은 아래와 같다.

- AWS 클라우드 서비스로 제공되어 서버관리가 필요없다.
- AWS 보안을 사용하기 때문에 보안성이 좋다.
- 이미 AWS 클라우드 서비스를 사용하고 있다면 도입이 간편.

---

### Kinesis Data Stream에서 사용되는 개념

**데이터 레코드**
저장되는 데이터의 단위. 데이터 레코드는 시퀀스 번호, 파티션 키 및 데이터가 있고 데이터는 최대 1MB.

**보존 기간**
데이터 레코드를 스트림에 추가한 후 데이터 레코드에 액세스할 수 있는 시간의 길이. 스트림 보존 기간은 기본적으로 생성 후 24시간으로 설정. 이 기간은 추가적으로 더 늘릴 수 있으나 그에 할당하는 추가 요금이 적용. (일반적으로 기본 24시간으로 사용된다.)

**Producer**
생산자는 Amazon Kinesis Data Stream으로 데이터를 입력하는 주체, 그림에서 a와 같이 웹서버, 디바이스 등이 있다.

**Consumer**
소비자는 Amazon Kinesis Data Stream으로부터 데이터를 가져와 사용하는 주체, 기본적으로 그림 b와 같이 Kinesis Data Firehouse를 바로 연결하여 처리.

**Shard**
샤드는 스트림에서 고유하게 식별되는 데이터 레코드 시퀀스. 스트림은 하나 이상의 샤드로 구성되며 각 샤드는 고정된 용량 단위를 제공한다. 

각 샤드는 읽기에 대해 초당 최대 5개의 트랜잭션, 최대 총 데이터 읽기 속도 (초당 2MB), 초당 최대 1,000개의 레코드를 지원할 수 있다. 최대 총 데이터 쓰기 속도는 초당 1MB (파티션 키 포함). 

스트림의 데이터 용량은 스트림에 지정하는 샤드 수의 함수. 스트림의 총 용량은 해당 샤드의 용량의 합계. 이러한 샤드를 구축 후에도 언제든지 변경 가능하여 데이터속도, 용량에 대한 대비가 가능.

**파티션 키**
A파티션 키는 스트림 내에서 샤드별로 데이터를 그룹화하는 데 사용. Kinesis Data Streams 스트림에 속한 데이터 레코드를 여러 샤드로 나눈다. 각 데이터 레코드와 연결된 파티션 키를 사용하여 해당 데이터 레코드가 속한 샤드를 확인. 

파티션 키는 각 키에 대한 최대 길이 제한이 256자인 유니코드 문자열. 파티션 키를 128비트 정수 값에 매핑하고 샤드의 해시 키 범위를 사용하여 연결된 데이터 레코드를 샤드에 매핑하기 위해 MD5 해시 함수 사용. 애플리케이션이 데이터를 스트림에 넣을 때는 파티션 키를 지정해야 한다.

**시퀀스 번호**
Kinesis Data Stream에서 내부적으로 할당하는 시퀀스 번호 .

---

### Kinesis Data Firehose?

실시간 스트리밍 데이터를 제공하기 위한 완전 관리형 서비스. 
생산자(데이터 입력)-Kinesis Data Firehose-소비자
같이 Kinesis Data Stream과 동일한 입출력 개념으로 사용되며 전송과정에서 데이터 변환이 가능, AWS의 S3,RDS 등을 소비자로 사용하기에 간쳔하게 구성되어 있다.

![1_LxcE-A0eLCWgiI2R1BKNOA](https://user-images.githubusercontent.com/86764734/165654138-98496981-ea19-447a-a8cb-4eaf8e2d2fd0.png)

### Kinesis Data Firehose 에서 사용되는 개념

**기록**
데이터 생산자가 Kinesis Data Firehose 전송 스트림으로 보내는 관심 데이터. (레코드의 최대 크기는 1MB)

**데이터 생산자**
생산자는 레코드를 Kinesis Data Firehose 전송 스트림으로 보낸다. 예를 들어 로그 데이터를 전송 스트림으로 보내는 웹서버는 데이터 생산자.
또한 게존 Kinesis Data Stream에서 데이터를 자동으로 읽고 대상으로 로드하도록 Kinesis Data Firehose 전송 스트림을 구성할 수 있다. 

**버퍼 크기 및 버퍼 간격**
Kinesis Data Firehose는 수신 스트리밍 데이터를 특정 크기로 또는 특정 기간 동안 버퍼링하여 대상으로 전달. 
(버퍼크기는 MB 단위이고 버퍼간격은 초 단위.)

---

### Kinesis Data Stream 사용법
Kinesis Data Stream을 사용하기 위한 (인스턴스?)생성은 어렵지 않지만 이후 Consumer를 설정하기 위한, 즉 실시간 스트림 전송이 되는 데이터를 처리/전송/소비하기 위한 설정은 다양한 방식이 있다. 

