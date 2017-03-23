# AWS EC2 Container Service ELK stack


Based on the official images:

* [elasticsearch](https://github.com/elastic/elasticsearch-docker)
* [logstash](https://github.com/elastic/logstash-docker)
* [kibana](https://github.com/elastic/kibana-docker)

**Note**: Other branches in this project are available:

# Requirements

## Setup

1. Install [Docker](http://docker.io).
2. Install [ecs-cli](http://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_Configuration.html).
3. Clone this repository

## Increase `vm.max_map_count` on your host

You need to increase the `vm.max_map_count` kernel setting on your Docker host.
To do this follow the recommended instructions from the Elastic documentation: [Install Elasticsearch with Docker](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#docker-cli-run-prod-mode)


## Configure ecs-cli tools

```bash
$ ecs-cli configure --region us-west-2 --access-key $AWS_ACCESS_KEY_ID --secret-key $AWS_SECRET_ACCESS_KEY --cluster ecs-elk
INFO[0000] Saved ECS CLI configuration for cluster (ecs-elk)
```

## Create a task in cluster

```bash
$ ecs-cli compose ---project-name ecs-elk -file docker-compose.yml up
INFO[0000] Using ECS task definition                     TaskDefinition=ecscompose-ecscompose-ecs-elk:1
```

### To Create a service for elk

```bash
$ ecs-cli compose --project-name ecs-elk --file docker-compose.yml service up
INFO[0001] Using ECS task definition                     TaskDefinition=ecscompose-ecs-elk:3                   TaskDefinition=ecscompose-ecs-elk:1
```
