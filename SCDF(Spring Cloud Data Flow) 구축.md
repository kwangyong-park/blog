# [TBD] SCDF(Spring Cloud Data Flow) 구축 

Spring Cloud Data Flow Helm을 통한 구축을 위한 방법입니다.

## Database 를 외부용으로 사용시 Install command


### Case 1 

- Database 외부 사용
- Kafka 내부 사용

_현재 작동이 제대로 하지 않는다. 원인 찾는중_

#### Pre conditions
Mysql에 dataflow, skipper 데이터베이스가 존재해야합니다.

```
create schema dataflow collate utf8mb4_general_ci;
create schema skipper collate utf8mb4_general_ci;
```

```
helm install scdf --set mariadb.enabled=false \
 --set externalDatabase.scheme=mariadb \
 --set externalDatabase.host= \
 --set externalDatabase.password=scdf1234 \
 --set externalDatabase.dataflow.user=scdf \
 --set externalDatabase.dataflow.password=scdf1234 \
 --set externalDatabase.dataflow.database=dataflow \
 --set externalDatabase.skipper.user=scdf \
 --set externalDatabase.skipper.password=scdf1234 \
 --set externalDatabase.skipper.database=skipper \
 --set externalDatabase.port=20306 \
 --set rabbitmq.enabled=false \
 --set kafka.enabled=true \
 bitnami/spring-cloud-dataflow --namespace scdf --create-namespace
```

### Case 2

- Database 내부 사용
- Kafka 내부 사용

```
helm install scdf --set rabbitmq.enabled=false \
 --set kafka.enabled=true \
 bitnami/spring-cloud-dataflow --namespace scdf --create-namespace
```
