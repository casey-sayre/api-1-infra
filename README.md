# docker network for api-1 services

```
docker network create api-1-network
```

# localstack

Create queue, topic, subscription so API can inform websocket server of updates

```
$ aws configure
AWS Access Key ID: 123
AWS Secret Access Key: xxx
Default region name: us-east-1
Default output format: None
```

```
$ aws --endpoint-url=http://localstack:4566 sns create-topic --name album-update-events --output table | cat

$ aws --endpoint-url=http://localstack:4566 sqs create-queue --queue-name album-queue --output table | cat

$ aws --endpoint-url=http://localstack:4566 sns list-topics

$ aws --endpoint-url=http://localstack:4566 sqs list-queues

$ aws --endpoint-url=http://localstack:4566 sns subscribe --topic-arn arn:aws:sns:us-east-1:000000000000:album-update-events --protocol sqs --notification-endpoint arn:aws:sqs:us-east-1:000000000000:album-queue    --output table | cat


topic-arn         arn:aws:sns:us-east-1:000000000000:album-update-events

QueueUrl          http://localstack:4566/000000000000/album-queue
QueueArn          arn:aws:sqs:us-east-1:000000000000:album-queue 

SubscriptionArn   arn:aws:sns:us-east-1:000000000000:album-update-events:2f26e887-ab45-4baf-b28e-d0b4f5b58d84


```


