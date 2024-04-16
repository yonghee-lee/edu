
## Kafka란?

**Apache Kafka**는 LinkedIn에서 개발되어 현재는 Apache Software Foundation에서 관리하는 오픈 소스 스트림 처리 플랫폼입니다. Kafka는 대규모 메시지 처리를 위한 분산 스트리밍 플랫폼으로, 실시간 데이터 파이프라인과 스트리밍 애플리케이션을 구축하기 위해 널리 사용됩니다.

#### 핵심 특징

- **고성능**: Kafka는 높은 처리량과 낮은 지연 시간을 갖춘 메시징 시스템으로 설계되었습니다. 대용량의 데이터 스트림을 효과적으로 처리할 수 있습니다.
    
- **확장 가능성**: Kafka는 수평적으로 확장 가능한 아키텍처를 가지고 있습니다. 클러스터에 브로커를 추가하여 처리 용량을 쉽게 확장할 수 있습니다.
    
- **내구성과 신뢰성**: Kafka는 메시지를 디스크에 저장하며, 복제를 통해 데이터의 손실 없이 고가용성을 보장합니다.
    
- **실시간 처리**: Kafka는 실시간 데이터 피드를 처리하고, 즉각적인 분석이 가능한 스트리밍 데이터를 제공합니다.
    

### 카프카의 기본 구성 요소

Apache Kafka의 구조를 이해하는 데 있어 중요한 몇 가지 기본 구성 요소들이 있습니다. 이들은 Kafka가 데이터를 효율적으로 처리하고 관리하는 데 필수적인 역할을 합니다.




#### 1. 토픽(Topic)

- Kafka의 데이터 저장 및 전송 단위입니다.
- 토픽은 메시지 또는 이벤트의 특정 카테고리 또는 피드를 나타냅니다.
- 프로듀서는 특정 토픽에 메시지를 발행하고, 컨슈머는 특정 토픽으로부터 메시지를 구독합니다.

#### 2. 파티션(Partition)

- 토픽은 여러 파티션으로 나뉠 수 있으며, 각 파티션은 메시지의 순서를 유지합니다.
- 파티션을 통해 데이터가 여러 브로커에 분산되어 저장될 수 있으며, 이를 통해 Kafka의 확장성과 병렬 처리 능력이 강화됩니다.
- 각 파티션은 브로커의 디스크에 순차적으로 저장되는 메시지 로그로 구성됩니다.

#### 3. 브로커(Broker)

- Kafka 서버의 인스턴스를 브로커라고 합니다.
- 하나의 Kafka 클러스터는 여러 브로커로 구성되며, 각 브로커는 토픽의 파티션 일부를 저장합니다.
- 브로커들은 클러스터 전반에 걸쳐 메시지의 로드 밸런싱과 복제를 관리합니다.

#### 4. 프로듀서(Producer)

- 메시지를 생성하고 Kafka 토픽의 파티션에 게시하는 역할을 합니다.
- 프로듀서는 메시지를 보낼 특정 토픽과 파티션을 선택할 수 있습니다.
- 고급 설정에서는 메시지 키를 기반으로 파티션을 선택하거나, 사용자 정의 파티셔너를 사용할 수도 있습니다.

#### 5. 컨슈머(Consumer)

- Kafka 토픽의 메시지를 구독하고 읽는 역할을 합니다.
- 컨슈머는 하나 이상의 토픽을 구독할 수 있으며, 토픽의 파티션으로부터 메시지를 읽습니다.
- 컨슈머 그룹을 형성하여 파티션들로부터 메시지를 분산하여 처리할 수 있습니다.

#### 6. 주키퍼(Zookeeper)

- Kafka 클러스터의 상태, 메타데이터, 브로커, 파티션 정보 등을 관리합니다.
- 주키퍼는 Kafka 클러스터의 브로커들 간의 동기화를 도와 클러스터의 정상적인 운영을 보장합니다.
- Kafka 2.8.0 이후 버전에서는 Kafka 자체 Raft 기반 메타데이터 시스템(KRaft)으로 주키퍼 의존성을 제거하는 방향으로 발전하고 있습니다.

### Kafka 설치 및 기본 설정

Apache Kafka를 설치하고 구성하는 과정은 Kafka 클러스터를 구축하고 운영하는 데 필수적인 첫걸음입니다. 이 섹션에서는 Kafka의 기본 설치 및 구성 절차를 소개합니다.

#### 1. Kafka 설치

- **선행 요구사항**: Kafka는 Java 런타임 환경(JRE)을 필요로 합니다. 따라서, 설치 전에 Java가 설치되어 있는지 확인하세요.
- **다운로드**: Apache Kafka는 Apache Kafka 웹사이트에서 다운로드할 수 있습니다.
- **설치**: 다운로드한 Kafka 압축 파일을 압축 해제하여 설치합니다.

#### 2. Zookeeper 설정

- Kafka는 메타데이터 관리를 위해 Zookeeper를 사용합니다. Kafka와 함께 Zookeeper도 함께 배포됩니다.
- Zookeeper 서비스를 시작하려면, Kafka 설치 디렉토리에서 `bin/zookeeper-server-start.sh` (또는 `.bat` 윈도우의 경우) 스크립트를 실행합니다.

#### 3.Zookeeper 설정 파일 (`zoo.cfg`)의 주요 내용

1. **clientPort**:
    
    - Zookeeper가 클라이언트 연결을 수신하는 포트입니다.
    - 기본값은 2181입니다.
    - 예시: `clientPort=2181`
2. **dataDir**:
    
    - Zookeeper의 데이터 디렉토리를 지정합니다. 이 디렉토리는 Zookeeper의 스냅샷과 트랜잭션 로그를 저장하는 데 사용됩니다.
    - 예시: `dataDir=/var/lib/zookeeper`
3. **dataLogDir**:
    
    - Zookeeper의 트랜잭션 로그를 별도로 저장할 디렉토리를 지정합니다. 이 설정은 선택 사항이지만, 성능 향상을 위해 사용될 수 있습니다.
    - 예시: `dataLogDir=/var/log/zookeeper`
4. **tickTime**:
    
    - Zookeeper 서버에서 사용하는 기본 시간 단위(밀리초)입니다.
    - 클라이언트 세션 타임아웃과 같은 다른 시간 관련 설정의 기준이 됩니다.
    - 예시: `tickTime=2000`
5. **initLimit**:
    
    - 팔로워(Follower) 서버가 리더(Leader) 서버와 초기 연결을 형성할 때까지 기다리는 시간(단위: tickTime)을 설정합니다.
    - 예시: `initLimit=10`
6. **syncLimit**:
    
    - 리더와 팔로워 간에 메시지를 동기화하는 시간 제한(단위: tickTime)을 설정합니다.
    - 예시: `syncLimit=5`
7. **server.X**:
    
    - 클러스터를 형성하는 Zookeeper 서버들의 목록을 정의합니다. 여기서 X는 서버 ID를 의미합니다.
    - 각 서버는 호스트명(IP)과 통신 포트, 투표를 위한 포트를 지정합니다.
    - 예시: `server.1=zookeeper1:2888:3888`

#### 4. Kafka 브로커 실행

- Kafka 브로커 서비스를 시작하려면, `bin/kafka-server-start.sh` (또는 `.bat` 윈도우의 경우) 스크립트를 실행합니다.
- 이 스크립트는 Kafka의 기본 설정 파일인 `config/server.properties`를 사용합니다.

#### 5. Kafka 브로커 기본 설정

- **server.properties**: Kafka 브로커의 주요 설정 파일입니다. 브로커 ID, 네트워크 포트, 로그 디렉토리 등의 설정을 포함합니다.
- **zookeeper.connect**: Zookeeper 서버의 호스트와 포트를 지정합니다.
- **log.dirs**: Kafka 메시지 로그가 저장될 디렉토리를 지정합니다.
- **num.partitions**: 기본 토픽 파티션 수를 설정합니다.


#### 6. 실습 : Kafka 기본 실행

##### Kafka Cluster 생성

테스트를 위해 1노드 Zookeeper 와 3노드 브로커의 Kafka Cluster 를 생성합니다.
```yaml
version: '2'
services:
  zookeeper:
    image: confluentinc/cp-zookeeper:latest
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000

  kafka1:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper
    ports:
      - "9092:9092"
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka1:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 2
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 2
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 2
      KAFKA_CONFLUENT_SUPPORT_METRICS_ENABLE: 'false'

  kafka2:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper
    ports:
      - "9093:9093"
    environment:
      KAFKA_BROKER_ID: 2
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka2:9093
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 2
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 2
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 2
      KAFKA_CONFLUENT_SUPPORT_METRICS_ENABLE: 'false'

  kafka3:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper
    ports:
      - "9094:9094"
    environment:
      KAFKA_BROKER_ID: 3
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka3:9094
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 2
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 2
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 2
      KAFKA_CONFLUENT_SUPPORT_METRICS_ENABLE: 'false'
```

##### 기본 토픽 생성

- Kafka가 실행되고 나면, `bin/kafka-topics.sh` 스크립트를 사용하여 첫 토픽을 생성할 수 있습니다.
- 예를 들어, 토픽을 생성하는 명령은 다음과 같습니다:

```sh
bin/kafka-topics --create --topic my-topic --bootstrap-server localhost:9092 --replication-factor 3 --partitions 1
```

- 생성된 토픽을 확인합니다.
```bash
bin/kafka-topics --bootstrap-server localhost:9092 --describe --topic my-topic
```
#####  테스트

- **프로듀서 테스트**: `bin/kafka-console-producer`를 사용하여 메시지를 토픽에 보낼 수 있습니다.
```bash
bin/kafka-console-producer --bootstrap-server localhost:9092 --topic my-topic
```

- **컨슈머 테스트**: `bin/kafka-console-consumer`를 사용하여 토픽에서 메시지를 읽을 수 있습니다.
```bash
bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic my-topic
```


### Kafka 프로듀서와 컨슈머

Apache Kafka에서 데이터의 생산과 소비는 프로듀서(Producer)와 컨슈머(Consumer) API를 통해 이루어집니다. 이 세션에서는 Kafka 프로듀서와 컨슈머의 기본적인 사용 방법을 살펴보고, 실제로 메시지를 보내고 받는 실습을 진행합니다.

#### 1. 프로듀서 API 사용 방법(with Spring-Boot)

프로듀서는 Kafka 토픽에 메시지를 발행하는 역할을 합니다. Kafka 프로듀서를 사용하는 기본 단계는 다음과 같습니다:

- **Kafka 프로듀서 인스턴스 생성**: spring boot 에서는 KafkaTemplate 을 사용하여 간편하게 메시지를 발송할 수 있습니다.
- Consumer 의 경우도 KafkaListener 어노테이션으로 간단하게 구현할 수 있습니다.

예제 코드
https://github.com/rahul-ghadge/spring-boot-kafka

#### 실습: 간단한 메시지 보내기와 받기

- **실습 목표**: 위에서 제공된 프로듀서 및 컨슈머 예시 코드를 실행하여 Kafka 토픽에 메시지를 보내고, 이 메시지를 구독하여 받는 과정을 실습합니다.
- **실습 절차**:
    1. Kafka 서버와 Zookeeper가 실행 중인지 확인합니다.
    2. 제공된 프로듀서 코드를 실행하여 메시지를 발행합니다.
    3. 제공된 컨슈머 코드를 실행하여 메시지를 수신합니다.


### Kafka 내부 동작 원리

#### 데이터 복제 과정

Kafka는 데이터 복제를 통해 고가용성을 보장하고 데이터 손실을 방지합니다. 데이터 복제 과정은 다음과 같습니다:

1. **Leader-Replica 구조**: 각 파티션에는 하나의 Leader와 여러 개의 Replica(복제)가 있습니다. Leader는 쓰기 작업을 담당하고, Replica는 데이터를 복제합니다.
2. **Producer에 의한 쓰기**: Producer가 데이터를 특정 파티션에 쓰면 Leader는 데이터를 받고, 이를 Replica에게 전달합니다.
3. **Acknowledge**: Replica가 데이터를 복제하고 나면 Leader는 Producer에게 Acknowledgment(확인)을 보냅니다. 이를 통해 데이터가 안전하게 복제되었음을 보장합니다.
4. **분산 복제**: 복제된 데이터는 여러 브로커에 분산 저장되므로 하나의 브로커가 다운되어도 데이터 손실이 발생하지 않습니다.

### 오프셋

#### 오프셋이란?

"카프카는 오프셋 관리를 통한 메시지 재처리, 중복처리 방지 기능 지원"

각 파티션이 수신한 메시지에는 각각의 일련번호가 있습니다. 그래서 파티션 단위로 메시지 위치를 나타내는 오프셋이라는 정보를 통해 컨슈머가 취득하는 메시지의 범위 및 재시도를 제어합니다. 제어를 위한 오프셋 종류는 다음과 같습니다.

- Last Committed Offset : 마지막 커밋 지점
- Log-End-Offset(LEO) : 메시지가 로깅된 마지막 지점, 즉 파티션 데이터의 끝 표시, 브로커에 의해 파티션에 관한 정보로 업데이트
- Current Offset : 컨슈머가 어디까지 데이터를 읽었는지 표시, 컨슈머에서의 데이터 취득을 계기로 업데이트
- Commit Offset : 컨슈머가 어디까지 커밋했는지 표시, 컨슈머 그룹마다 보관되어 업데이트됨, 컨슈머로부터 "여기까지의 오프셋은 처리함"이라는 것을 확인하는 오프셋 커밋을 계기로 업데이트. 특정 토픽에 대해 여러 컨슈머 그룹이 메시지를 취득할 때는 파티션에 대한 Commit Offset도 컨슈머 그럼 숫자만큼만 존재

#### 컨슈머 입장의 오프셋

- Current Position : 애플리케이션 현재 처리 위치, 컨슈머의 포지션이 5라고 하면 0~4까지는 처리한 것이다. 다음 poll()의 첫 레코드는 5이다. 따라서 컨슈머가 처리한 레코드 중의 최고 오프셋보다 +1인 것이다.
- Committed Position : 컨슈머 프로스세가 재시작하는 경우가 있다. 이때는 Committed Position 값을 보고 그 레코드부터 읽는다. Auto Commit 기능을 통해 주기적으로 오프셋을 커밋하거나 commitSync, commitAsync를 사용하여 커밋할 수 있다.

물론 컨슈머는 오프셋을 Offset Topic에 저장해야만 하는 것은 아니며 다른 저장소도 가능합니다. 따라서 다른 저장소에 레코드 처리 결과를 저장하는 것과 오프셋 저장 행위를 원자적으로(atomic) 처리할 수 있습니다. RDBMS와 같은 외부 솔루션을 사용할 수 있습니다. 만약 이렇게 오프셋을 직접 관리하면 다음과 같은 설정이 필요합니다.

- enable.auto.commit=false
- ConsumerRecord 제공 오프셋을 이용하여 오프셋 저장
- 재시작 시 컨슈머 Position 복구 필요. seek 메소드 사용 `TopicPartition​(java.lang.String topic, int partition)`

파티션 할당이 자동으로 이루어지는 경우를 고려해야 합니다. 이때는 ConsumerRebalaceListener를 사용합니다.

#### ConsumerRebalanceListener

파티션이 재조정될 때 실행되는 콜백 메소드를 가진 인터페이스

컨슈머가 직접 파티션을 할당하지 않고 컨슈머 그룹 개념을 통해 파티션이 자동으로 할당되도록 했을 때만 사용할 수 있습니다. 만약 직접 파티션을 할당했다면, 재조정 발생하지 않고 콜백도 호출되지 않습니다.

ConsumerRebalaceListener 는 오프셋을 DB등 다른 저장소에 관리할 때 사용합니다.

콜백 메소드는 파티션이 재조정될 때 poll() 내부에서 호출됩니다. 

#### High Watermark

- High Watermark : 복제 완료된 메시지 지점

복제 사용 시 오프셋 관리를 위해 LEO 외에 High Watermark라는 개념이 있습니다. High Watermark는 복제가 완료된 오프셋입니다. 그래서 LEO와 동일하거나 혹은 오래된 오프셋이 됩니다.

컨슈머 입장에서는 High Watermark까지 기록된 메시지를 취득할 수 있습니다. 만약 LEO에 기록되어 있지만 복제가 완료되지 않은 메시지(즉 High Watermark에 기록되지 않은 메시지)를 취득했을 때, 애매한 타이밍에 문제가 생기면(예: leader가 복제 내리기 전에 죽음) 그 메시지는 재취득할 수 없는 상태가 됩니다.

### commit 관리

데이터를 가져오는 컨슈머 입장

#### 자동 커밋 

- 오프셋, 파티션 관리를 사용자가 하지 않아도 되는 경우, 즉 로그성 데이터 처리 등에 사용합니다.
- enable.auto.commit=true
- auto.commit.interval.ms 설정으로 주기 관리

auto commit이 true이면 poll() 호출 시마다 commit할 타이밍인지 확인합니다. (timer expire 기반)

중복이 발생할 수 있습니다. 인터벌이 5초라고 하면,

1. poll()을 통해 데이터 200개 가져옴 (그리고 오프셋 commit됨)
2. 레코드 200개 중 100개 처리 완료
3. 이 때 재조정 발생 (이유는 파티션 수 증가, 혹은 컨슈머 증감)
4. 컨슈머들이 리어사인
5. 컨슈머는 1. 에서 commit된 오프셋부터 polling
6. 중복처리 (...)

대응방안으로는 poll() 다음에 close()를 호출합니다. close()를 호출하면 ConsumerCoorinator.maybeAutoCommitOffsetsSync()를 호출하게 됩니다.

#### 수동 커밋

- 메시지 처리가 완료될 때까지 메시지를 가져온 것으로 간주되어서는 안된다 (비즈니스 로직)
- enable.auto.commit=false
- 명시적으로 commitSync 호출하여 메시지 처리 & 메시지 가져온 것으로 설정

#### commitSync

void   commitSync​()    
void    commitSync​(java.time.Duration timeout)  
void    commitSync​(java.util.Map<TopicPartition,OffsetAndMetadata> offsets)   
void    commitSync​(java.util.Map<TopicPartition,OffsetAndMetadata> offsets, java.time.Duration timeout)

commitSync를 통해 메시지 처리가 완료되었고 메시지를 가져온 것으로 처리하기 때문에 commitSync를 수행하지 않으면 실패한 현재 오프셋부터 다시 가져올 것이라고 생각할 수 있습니다. 하지만 그냥 이후 오프셋부터 가져오게 됩니다.

실패했던 레코드의 오프셋을 다시 poll 하기 위해 seek() 메소드 사용합니다. (해당 레코드로 되돌아감)
#### 파티션 리밸런싱

파티션 리밸런싱은 컨슈머 그룹 내에서 파티션 할당을 조정하여 공정한 작업 분배를 보장합니다.

1. **파티션 할당**: 컨슈머 그룹의 각 멤버(컨슈머)에게 파티션이 할당됩니다. 기본적으로 모든 컨슈머에게는 1개 이상의 파티션이 할당 되며, 만약 컨슈머 수가 파티션 수보다 많다면 할당이 되지 않는 컨슈머가 존재하게 됩니다.
3. **멤버 추가 또는 제거**: 새로운 멤버가 그룹에 추가되거나 기존 멤버가 나가면 파티션 할당이 조정됩니다.
4. **파티션 재배치**: 파티션 리밸런싱 과정에서 파티션은 컨슈머 간에 재배치될 수 있으며, 이를 통해 작업 부하를 공정하게 분산합니다.

#### 메시지 전송의 내구성과 일관성

Kafka는 메시지 전송의 내구성과 일관성을 보장하기 위해 다음과 같은 메커니즘을 사용합니다:

1. **메시지 저장**: 모든 메시지는 브로커에 저장되며, 디스크에 저장되거나 메모리에 보관됩니다.
2. **복제**: 이미 언급한대로 모든 파티션은 여러 개의 Replica를 가지며 데이터의 복제를 통해 내구성을 확보합니다.
3. **메시지의 순서 보장**: Kafka는 파티션 내에서 메시지의 순서를 보장합니다. 따라서 메시지의 순서가 중요한 경우에도 일관성을 유지합니다.
4. **컨슈머 Offset**: 컨슈머는 처리한 메시지의 위치를 오프셋(Offset)으로 관리하여, 메시지를 중복으로 처리하지 않고 일관성을 유지합니다.

이러한 메커니즘을 통해 Kafka는 고가용성, 내구성 및 일관성을 제공하며 대용량 메시지 스트림 처리에 적합한 시스템으로 작동합니다.


### Kafka Streams 및 Connect

#### Kafka 스트림즈 소개

Kafka Streams는 실시간 스트림 처리를 위한 클라이언트 라이브러리로, Apache Kafka를 사용하여 실시간 데이터 처리 애플리케이션을 구축할 수 있게 해줍니다. Kafka Streams는 단순성과 강력한 스트리밍 기능, 그리고 Kafka 플랫폼과의 높은 통합성을 제공합니다.

- **핵심 기능:**
    - 간단한 스트림 처리, 집계, 조인 등의 작업을 위한 고수준 API 제공
    - 상태 저장, 윈도우, 시간 기반 처리 등 복잡한 스트림 처리 기능 지원
    - 고가용성과 확장성을 위한 분산 처리 모델

#### Kafka 커넥터 사용 사례

Kafka Connect는 데이터 소스와 싱크를 Kafka와 연결하기 위한 프레임워크입니다. 이를 통해 데이터베이스, 로그, 메트릭, 서비스 등 다양한 데이터 소스로부터 데이터를 실시간으로 수집하거나, Kafka에서 외부 시스템으로 데이터를 전송할 수 있습니다.

- **실습을 위한 Kafka Connect 설정:**
    - **목표:** 로컬 파일 시스템의 파일로부터 데이터를 읽어 Kafka 토픽으로 전송하고, 해당 토픽의 데이터를 다시 로컬 파일 시스템으로 출력하는 실습을 진행합니다.
    - **사용 커넥터:** File Source Connector와 File Sink Connector

#### 실습: Kafka 커넥터 설정 및 스트림 처리 작업

##### A. Kafka 커넥터 실습 환경 설정

Spooldir Source Connector Download
https://www.confluent.io/hub/jcustenborder/kafka-connect-spooldir

Download 받은 zip 파일을 ./connect-plugins 디렉토리에 넣고 압축 해제(zip 파일은 삭제)

`docker-compose.yaml` 파일을 사용하여 필요한 Kafka 및 Kafka Connect 컨테이너를 띄웁니다.

```yaml
version: '2'
services:
  zookeeper:
    image: confluentinc/cp-zookeeper:latest
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000

  kafka1:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper
    ports:
      - "9092:9092"
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka1:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 2
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 2
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 2
      KAFKA_CONFLUENT_SUPPORT_METRICS_ENABLE: 'false'

  kafka2:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper
    ports:
      - "9093:9092"
    environment:
      KAFKA_BROKER_ID: 2
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka2:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 2
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 2
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 2
      KAFKA_CONFLUENT_SUPPORT_METRICS_ENABLE: 'false'

  kafka3:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper
    ports:
      - "9094:9092"
    environment:
      KAFKA_BROKER_ID: 3
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://kafka3:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 2
      KAFKA_TRANSACTION_STATE_LOG_MIN_ISR: 2
      KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR: 2
      KAFKA_CONFLUENT_SUPPORT_METRICS_ENABLE: 'false'

  connect:
    image: confluentinc/cp-kafka-connect:latest
    depends_on:
      - kafka1
      - kafka2
      - kafka3
    ports:
      - "8083:8083"
    environment:
      CONNECT_BOOTSTRAP_SERVERS: kafka1:9092,kafka2:9092,kafka3:9092
      CONNECT_REST_PORT: 8083
      CONNECT_GROUP_ID: "kafka-connect-group"
      CONNECT_CONFIG_STORAGE_TOPIC: "kafka-connect-configs"
      CONNECT_OFFSET_STORAGE_TOPIC: "kafka-connect-offsets"
      CONNECT_STATUS_STORAGE_TOPIC: "kafka-connect-status"
      CONNECT_KEY_CONVERTER: "org.apache.kafka.connect.json.JsonConverter"
      CONNECT_VALUE_CONVERTER: "org.apache.kafka.connect.json.JsonConverter"
      CONNECT_KEY_CONVERTER_SCHEMAS_ENABLE: "false"
      CONNECT_VALUE_CONVERTER_SCHEMAS_ENABLE: "false"
      CONNECT_INTERNAL_KEY_CONVERTER: "org.apache.kafka.connect.json.JsonConverter"
 CONNECT_INTERNAL_VALUE_CONVERTER:"org.apache.kafka.connect.json.JsonConverter"
      CONNECT_PLUGIN_PATH: "/usr/share/java"
    volumes: 
	  - ./connect-plugins:/usr/share/java

```



아래 curl 명령어로 Connector 생성

```bash
curl -X POST \
    -H "Content-Type: application/json" \
    --data '{

			"name": "file-source-connector-1",
			"config": {
				"connector.class":"com.github.jcustenborder.kafka.connect.spooldir.SpoolDirLineDelimitedSourceConnector",

      "tasks.max": "10",
      "input.path": "/input/file/path",
      "finished.path": "/finished/file/path",
      "error.path": "/error/file/path",
      "input.file.pattern":".*\\.txt",
      "halt.on.error": false,
      "cleanup.policy": "MOVE",
      "topic": "file-topic",
      "key.converter": "org.apache.kafka.connect.storage.StringConverter",
      "value.converter": "org.apache.kafka.connect.storage.StringConverter",
      "key.converter.schemas.enable": "false",
      "value.converter.schemas.enable": "false",
     
    }

  }' \
    http://localhost:9083/connectors
```

##### B. 실습: 간단한 스트림 처리 작업

Kafka Streams를 사용한 스트림 처리 예제 코드입니다.
```java
import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.KStream;

import java.util.Properties;

public class SimpleStreamApp {

    public static void main(String[] args) {
    
        Properties props = new Properties();
        props.put(StreamsConfig.APPLICATION_ID_CONFIG, "simple-stream-app");
        props.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
        props.put(StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG, Serdes.String().getClass());
        props.put(StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG, Serdes.String().getClass());

        StreamsBuilder builder = new StreamsBuilder();
        KStream<String, String> sourceStream = builder.stream("source-topic");
        sourceStream.flatMapValues(value -> Arrays.asList(value.toLowerCase().split("\\W+")))
                    .to("sink-topic");

        KafkaStreams streams = new KafkaStreams(builder.build(), props);
        streams.start();

        Runtime.getRuntime().addShutdownHook(new Thread(streams::close));
    }
}

```

토픽 내용 모니터링
```bash
kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic source-topic --from-beginning

kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic sink-topic --from-beginning
```


### Kafka 모니터링 및 운영

#### Kafka 모니터링의 중요성

Apache Kafka는 대규모 스트림 처리 및 메시지 큐잉 시스템에서 핵심 구성 요소로 활용됩니다. Kafka의 높은 처리량과 확장성은 실시간 데이터 파이프라인과 애플리케이션에 중요한 역할을 합니다. 이러한 시스템의 복잡성과 중요성 때문에, Kafka 클러스터의 성능과 가용성을 지속적으로 모니터링하는 것은 운영상 매우 중요합니다.

모니터링을 통해 시스템의 현재 상태를 이해하고, 잠재적인 문제를 조기에 발견하여 대응할 수 있습니다. 또한, 성능 최적화와 리소스 관리를 위한 데이터 기반 의사 결정을 지원합니다.

#### 주요 모니터링 메트릭스

Kafka 클러스터를 효과적으로 모니터링하기 위해 다음과 같은 주요 메트릭스에 주목해야 합니다.

- **브로커 메트릭스**: 메시지 입출력률, 액티브 컨트롤러 수, 리더 및 팔로워 지연 시간, 언더레플리케이티드 파티션 수 등
- **토픽 메트릭스**: 토픽별 메시지 크기, 토픽별 메시지 입출력률, 토픽별 파티션 수
- **프로듀서/컨슈머 메트릭스**: 배치 크기, 커밋 지연 시간, 컨슈머 Lag, 컨슈머 처리율
- **시스템 리소스 메트릭스**: CPU 사용량, 메모리 사용량, 디스크 I/O, 네트워크 I/O

#### Kafka 운영을 위한 팁과 베스트 프랙티스

Kafka 클러스터의 운영을 개선하고, 안정성과 성능을 유지하기 위한 몇 가지 중점 사항을 소개합니다.

- **적절한 하드웨어 선택**: Kafka는 네트워크 I/O와 디스크 I/O에 높은 요구사항을 가지고 있으므로, 고성능의 네트워크 인터페이스와 SSD를 사용하는 것이 좋습니다.
- **클러스터와 토픽 구성 최적화**: 브로커 수와 파티션 수를 적절히 설정하여 처리량과 병렬 처리를 최적화합니다. 토픽 설정(예: 세그먼트 크기, 보존 정책)도 사용 사례에 맞게 조정해야 합니다.
- **리플리케이션과 파티셔닝 전략**: 높은 가용성과 내결함성을 위해 적절한 리플리케이션 팩터를 설정하고, 파티셔닝 전략을 통해 데이터를 균일하게 분산시킵니다.
- **모니터링과 로깅**: 주요 메트릭스에 대한 모니터링 시스템을 구축하고, 로그 수집 및 분석 도구를 사용하여 시스템 동작을 지속적으로 관찰합니다.
- **정기적인 유지보수**: 클러스터의 성능을 최적화하고 저장 공간을 관리하기 위해 정기적인 컴팩션과 클린업을 수행합니다.
- **보안 설정**: 데이터 전송 중 암호화(SSL/TLS), 클라이언트 인증, 접근 제어 목록(ACL) 설정을 통해 클러스터 보안을 강화합니다.

Kafka 클러스터를 효과적으로 모니터링하고 운영하기 위해서는 이러한 팁과 베스트 프랙티스를 적극적으로 적용하는 것이 중요합니다. 이를 통해 시스템의 안정성을 보장하고, 예상치 못한 문제로부터 빠르게 회복할 수 있습니다.


### Kafka 튜닝 및 고급 설정

#### Kafka 퍼포먼스 튜닝

Kafka의 퍼포먼스 튜닝은 시스템의 처리량, 지연 시간, 그리고 자원 사용을 최적화하는 과정입니다. 효과적인 튜닝을 위해서는 몇 가지 중요한 설정과 전략에 주목해야 합니다.

- **배치 크기 조정**: 프로듀서와 컨슈머의 배치 크기(`batch.size`, `fetch.min.bytes`)를 조정하여 네트워크 사용과 디스크 I/O를 최적화합니다.
- **로그 세그먼트 크기**: 로그 세그먼트 파일의 크기(`log.segment.bytes`)와 보존 기간(`log.retention.hours`)을 적절히 설정하여 디스크 사용을 관리합니다.
- **리플리케이션과 파티션**: 높은 처리량을 위해 적절한 파티션 수를 설정하고, 데이터의 내구성을 위해 리플리케이션 팩터(`replication.factor`)를 조정합니다.
- **커밋 인터벌 조정**: 컨슈머의 오프셋 커밋 인터벌(`auto.commit.interval.ms`)을 조정하여 처리량과 지연 시간 사이의 균형을 맞춥니다.

#### 고가용성 및 장애 대응

Kafka 클러스터의 고가용성을 보장하고 장애에 효과적으로 대응하기 위한 전략은 다음과 같습니다.

- **멀티 브로커 설정**: 단일 장애 지점을 제거하기 위해 여러 브로커를 사용하여 클러스터를 구성합니다.
- **리플리케이션**: 모든 중요 데이터는 여러 브로커에 걸쳐 리플리케이트되어야 하며, `min.insync.replicas` 설정을 통해 데이터의 내구성을 보장합니다.
- **주키퍼 앙상블**: Zookeeper의 고가용성을 위해 3개 이상의 노드로 구성된 앙상블을 운영합니다.
- **정기적인 백업**: 중요 토픽의 데이터를 정기적으로 백업하여 데이터 손실에 대비합니다.

#### 보안 설정

Kafka 클러스터의 보안을 강화하기 위한 설정은 다음을 포함합니다.

- **네트워크 암호화**: SSL/TLS를 사용하여 브로커 간 및 클라이언트와 브로커 간 통신을 암호화합니다.
- **인증 및 권한 부여**: SASL/PLAIN, SASL/SCRAM 등을 통한 인증 메커니즘을 설정하고, ACL을 사용하여 리소스 접근을 제어합니다.
- **암호화된 데이터 저장**: 디스크에 저장된 데이터를 암호화하여 물리적 접근으로부터 보호합니다.

#### 실습: Kafka 튜닝 실습

이 실습에서는 Kafka 클러스터의 퍼포먼스 튜닝을 직접 경험해보겠습니다. 실습 목표는 프로듀서와 컨슈머의 설정을 조정하여 메시지 처리량을 최대화하는 것입니다.

1. **프로듀서 배치 크기 조정**: `batch.size` 설정을 증가시켜 한 번에 전송할 수 있는 메시지의 크기를 늘립니다.
2. **컨슈머 패치 크기 조정**: `max.partition.fetch.bytes`를 조정하여 컨슈머가 한 번에 가져올 수 있는 데이터의 최대 크기를 증가시킵니다.
3. **파티션 수 변경**: 주요 토픽의 파티션 수를 증가시켜 처리량을 향상시킵니다.
4. **성능 측정**: 변경 전후의 메시지 처리량을 측정하여 튜닝의 효과를 평가합니다.

실습을 통해 Kafka 클러스터의 설정을 조정하고 그 영향을 관찰함으로써, Kafka 시스템의 퍼포먼스 튜닝에 대한 실질적인 경험을 얻을 수 있습니다.

