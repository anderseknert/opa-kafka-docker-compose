# Open Policy Agent and Kafka

Example code for running Kafka with client certificates for authentication, and using OPA for authorization decisons.

## Setup

1. Copy an OPA configuration file (`opa-conf.yaml`) into the `opa` directory.
2. Copy the [OPA Kafka Authorizer Plugin](https://github.com/anderseknert/opa-kafka-plugin) into the `plugin` directory.
3. Run the `create_cert.sh` script to create server and client certificates. These will be found in the `cert` directory.
4. `docker compose up`

## Querying Kafka

Using the `alice` user with a client certificate.

### Producing to a topic

```shell
bin/kafka-console-producer.sh --broker-list localhost:9093 --topic test --producer.config path/to/cert/client/alice.properties
> My first message
> My second message
...
Ctrl+c
```

### Consuming from a topic

```shell
bin/kafka-console-consumer.sh --bootstrap-server localhost:9093 --topic test --consumer.config path/to/cert/client/alice.properties --from-beginning
My first message
My second message
...
Ctrl+c

Processed a total of 4 messages
```