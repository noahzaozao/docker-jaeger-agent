# docker-jaeger-agent

## pre-requirements

- Centos 7
- docker 18.09 with docker swarm

## .env

```bash
cp .env-trunk .env
vi .env
JAEGER_ACCESS_TOKEN=[YOUR_ACCESS_TOKEN]
```

## docker-compose.yml

```yaml
version: '3.3'

services:
    jaeger-agent:
      image: jaegertracing/jaeger-agent
      command: ["--reporter.grpc.host-port=tracing-analysis-dc-sh.aliyuncs.com:1883", "--jaeger.tags=Authentication=$JAEGER_ACCESS_TOKEN"]
      ports:
        - "5775:5775/udp"
        - "6831:6831/udp"
        - "6832:6832/udp"
        - "5778:5778"
      restart: on-failure
```

## deploy_jaeger_agent.sh

```bash
docker-compose up -d jaeger-agent
```

