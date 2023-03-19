# docker network for api-1 services

```
docker network create api-1-network
```

# get containers started

```
$ docker-compose up -d
```

# get the data initialized

* open pgadmin in browser at url: "http://localhost", user: "user@domain.com", pw: "SuperSecret"
* with pgadmin, click add server
  * perhaps named "local postgres"
  * host name "api_1_postgres"
  * user name "postgres"
  * password "password"
* with pgadmin, with databases selected
  * click on icon to open sql window, paste contents of ddl/Music-database.sql, execute
* with pgadmin, with Music database selected,
  * click on icon to open sql window, paste contents of ddl/albums-table.sql
* with pgadmin, add a couple of records to albums table

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

$ aws --endpoint-url=http://localstack:4566 sns subscribe --topic-arn arn:aws:sns:us-east-1:000000000000:album-update-events --protocol sqs --notification-endpoint arn:aws:sqs:us-east-1:000000000000:album-queue    --output table | cat


$ # Topic-arn         arn:aws:sns:us-east-1:000000000000:album-update-events
$ # QueueUrl          http://localstack:4566/000000000000/album-queue
$ # QueueArn          arn:aws:sqs:us-east-1:000000000000:album-queue 

$ aws --endpoint-url=http://localstack:4566 sns list-topics
$ aws --endpoint-url=http://localstack:4566 sqs list-queues

```


