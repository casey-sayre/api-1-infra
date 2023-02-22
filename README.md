docker pull dpage/pgadmin4
docker run -p 80:80 \
    -e 'PGADMIN_DEFAULT_EMAIL=user@domain.com' \
    -e 'PGADMIN_DEFAULT_PASSWORD=SuperSecret' \
    --network="api-network" --name="pgadmin" \
    -d dpage/pgadmin4

```
aws --region=us-east-1 --endpoint=http://localhost:9324 sqs create-queue \
--queue-name=test
```

```
aws --region=us-east-1 --endpoint=http://localhost:9324 sqs list-queues
```

```
aws --region=us-east-1 --endpoint=http://localhost:9324 sqs send-message \
--queue-url http://localhost:9324/000000000000/test \
--message-body "{object:[{key:value, anotherkey:anothervalue}]}" \
--delay-seconds 5
```

```
aws sqs receive-message --queue-url http://localhost:9324/000000000000/test
```

# docker network for api-1 services

```
docker network create api-1-network
```

# localstack

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


