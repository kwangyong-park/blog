# SCDF(Spring Cloud Data Flow) 구축

Spring Cloud Data Flow Helm을 통한 구축을 위한 방법입니다.


### Case 1 

- Database 내부 사용
- Kafka 내부 사용

```
helm install scdf --set rabbitmq.enabled=false \
 --set kafka.enabled=true \
 bitnami/spring-cloud-dataflow --namespace scdf --create-namespace
```
