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

Kinesis Data Stream이란 대량의 데이터를 실시간으로 수집, 처리하는 서비스. 내부적으로 샤트로 구성되어 있으며 이를 동적으로 증가/감소할 수 있고 샤트 수에 따른 보장된 전송시간을 제공하기 때문에 이점이 많음.

주로 연속적으로 생간되는 대랑의 데이터 소스(1MB이하)를 처리해야하는 파이프라인에 사용하기 좋다.

이와 비슷한 서비스로 Kafka, Rabbitmq등이 있고 이와 구별되는 Kinesis Data Stream의 특징은 아래와 같다.

- AWS 클라우드 서비스로 제공되어 서버관리가 필요없다.
- AWS 보안을 사용하기 때문에 보안성이 좋다.
- 이미 AWS 클라우드 서비스를 사용하고 있다면 도입이 간편.