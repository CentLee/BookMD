# Kafka & RabbitMQ Diff

### 메시지를 처리한다는 점에서 유사한 점을 가지지만, 주로 사용되는 사례가 어느정도 차이가 있으며 이 둘을 같이 사용하면 조금더 포커싱을 해서 효율적으로 사용할 수 있다.

### 비동기 처리:
- Kafka: Kafka는 주로 이벤트 스트림 처리를 위한 메시지 큐로서 디자인되었습니다. 메시지를 일괄 처리(batch processing)하며, 이는 비동기 처리에 적합합니다. Kafka에서 메시지는 영구적으로 저장되고, 데이터 스트림으로 활용됩니다.

- RabbitMQ: RabbitMQ는 메시지 큐와 메시지 브로커로서 다양한 메시징 패턴을 지원합니다. 비동기 처리 역시 가능하지만, RabbitMQ는 메시지를 즉시 처리하거나 지연 처리하는 데 더 유연하게 사용할 수 있습니다.

### 대용량 데이터 처리:
- Kafka: Kafka는 대용량 데이터 스트리밍 처리에 특히 적합한 플랫폼입니다. 다수의 프로듀서에서 메시지를 생성하고, 여러 컨슈머에서 병렬로 처리할 수 있으며, 데이터를 영구적으로 저장합니다.

- RabbitMQ: RabbitMQ도 대용량 데이터 처리를 할 수 있지만, 주로 일반적인 메시지 큐 용도로 사용됩니다. 데이터를 영구적으로 저장하는 것은 가능하지만, 주요 목적은 메시지 큐의 미들웨어 역할입니다.

### 구현 및 사용 사례:
- Kafka: Kafka는 이벤트 스트리밍, 로그 처리, 실시간 데이터 처리 등 대규모 데이터 스트림 처리에 주로 사용됩니다.

- RabbitMQ: RabbitMQ는 메시지 큐, 작업 큐, 이벤트 기반 아키텍처, 메시지 브로커 등 다양한 메시징 시나리오에 사용됩니다.

#### 사용사례를 제가 했던 화상회의 프로젝트로 엮는다면 클라이언트가 미디어 서버와 데이터 채널을 맺고 방이 만들어지거나 하는 이벤트 메시지에 대한 처리는 RabbitMQ 전용으로, 
#### 미디어 서버로 오는 영상 및 음성에 대한 스트림 데이터는 Kafka 전용으로 처리한다면 둘을 효과적으로 사용할 수 있다고 생각합니다.