# SCDF(Spring Cloud Data Flow) Debezium 구축

Spring Cloud Data Flow CDC Debezium 구축을 위한 방법입니다.

## config 

### Database Connection Options
* app.cdc-debezium.cdc.config.database.hostname
* app.cdc-debezium.cdc.config.database.password
* app.cdc-debezium.cdc.config.database.port
* app.cdc-debezium.cdc.config.database.server.id
* app.cdc-debezium.cdc.config.database.server.name
* app.cdc-debezium.cdc.config.database.user
* app.cdc-debezium.cdc.config.database.whitelist

### CDC Options
* app.cdc-debezium.cdc.config.include.query=true
* app.cdc-debezium.cdc.connector=mysql
* app.cdc-debezium.cdc.flattening.enabled=false

### CDC Engine Offset Options

* app.cdc-debezium.cdc.name
* app.cdc-debezium.cdc.offset.flush-interval=6000
* app.cdc-debezium.cdc.offset.storage=file

### Snapshot

* app.cdc-debezium.cdc.config.snapshot.locking.mode
* app.cdc-debezium.cdc.config.snapshot.mode


#### Offset Storage Options for Kafka
[Stack overflow](https://stackoverflow.com/questions/70620417/why-debezium-connector-cant-connect-to-a-sasl-activated-broker)

* app.cdc-debezium.cdc.config.database.history.consumer.sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required username=''  password=''
* app.cdc-debezium.cdc.config.database.history.consumer.sasl.mechanism=SCRAM-SHA-512
* app.cdc-debezium.cdc.config.database.history.consumer.security.protocol=SASL_SSL
* app.cdc-debezium.cdc.config.database.history.consumer.ssl.truststore.location=
* app.cdc-debezium.cdc.config.database.history.consumer.ssl.truststore.password=
* app.cdc-debezium.cdc.config.database.history.kafka.bootstrap.servers=
* app.cdc-debezium.cdc.config.database.history.kafka.topic=
* app.cdc-debezium.cdc.config.database.history.producer.request.size=10000
* app.cdc-debezium.cdc.config.database.history.producer.sasl.jaas.config=org.apache.kafka.common.security.scram.ScramLoginModule required username=''  password=''
* app.cdc-debezium.cdc.config.database.history.producer.sasl.mechanism=SCRAM-SHA-512
* app.cdc-debezium.cdc.config.database.history.producer.security.protocol=SASL_SSL
* app.cdc-debezium.cdc.config.database.history.producer.ssl.truststore.location=
* app.cdc-debezium.cdc.config.database.history.producer.ssl.truststore.password=


### Volume Mount Options
[Spring Cloud Data Flow Reference](https://docs.spring.io/spring-cloud-dataflow/docs/current/reference/htmlsingle/#configuration-kubernetes-deployer)

* app.cdc-debezium.cdc.schema=true
* deployer.cdc-debezium.kubernetes.volume-mounts=[{name: '', mountPath: '/mnt'}]
* deployer.cdc-debezium.kubernetes.volumes=[{name: '', persistentVolumeClaim: { claimName: '', readOnly: 'false' }}]

### Application Memory Options
[Spring Cloud Data Flow Reference](https://docs.spring.io/spring-cloud-dataflow/docs/current/reference/htmlsingle/#_environment_variables)

* deployer.cdc-debezium.memory=2048
* deployer.cdc-debezium.kubernetes.environment-variables=JAVA_OPTIONS=-Xmx1024m



## Troubleshooting

####  org.apache.kafka.common.errors.TimeoutException: Expiring 4 record(s) for xxx ms has passed since batch creation

TBD 


[Stack overflow](https://stackoverflow.com/questions/53223129/kafka-producer-timeoutexception)

[Stack overflow](https://stackoverflow.com/questions/49868753/debezium-flush-timeout-and-outofmemoryerror-errors-with-mysql)

* app.cdc-debezium.cdc.config.request.timeout.ms

* app.cdc-debezium.cdc.config.max.request.size

#### Snapshot 취득 시 다음 설정을 통해 global read lock 

snapshot.mode = never → snapshot을 취득하지 않고, binlog를 처음부터 읽는다. binlog가 DB 생성 시점부터 모두 남아있을 경우에만 사용 가능
snapshot.locking.mode = none → snapshot 취득 시 lock을 사용하지 않는다. snapshot 취득 도중에 DDL이 발생하면 문제가 발생하므로 해당 과정에 DDL이 없어야 한다. 

* app.cdc-debezium.cdc.config.snapshot.locking.mode=none
* app.cdc-debezium.cdc.config.snapshot.mode=never


