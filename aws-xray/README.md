# AWS X-Ray for JAVA

1. 建立 User `aws-ot-collector` 並賦予 IAM Policy `AWSXRayDaemonWriteAccess`

2. 拉取 Source Code

```
git clone https://github.com/klin0024/java_apm.git
cd java_apm/aws-xray
```

3. 修改 AWS OTEL Collector 設定檔

- otel-config.yaml
```
exporters:
  logging:
    loglevel: debug
  awsxray:
    region: < AWS REGION >
  awsemf:
    region: < AWS REGION >
```

- docker-compose.yaml
```
environment:
    AWS_REGION: < AWS REGION >
    AWS_ACCESS_KEY_ID: < AWS ACCESS KEY ID >
    AWS_SECRET_ACCESS_KEY: < AWS SECRET ACCESS KEY >
```

4. 啟動 AWS OTEL Collector

```
docker-compose up -d
```

3. 設置環境變數

```
export OTEL_RESOURCE_ATTRIBUTES=service.namespace=< APP Group >
export OTEL_SERVICE_NAME=< APP Name >
export OTEL_TRACES_SAMPLER=always_on
export OTEL_TRACES_EXPORTER=otlp
export OTEL_METRICS_EXPORTER=none
export OTEL_EXPORTER_OTLP_ENDPOINT=http://< AWS OTEL Collector IP >:4317
export JAVA_OPTS="-javaagent:aws-opentelemetry-agent.jar"
```

4. 執行 JAVA 應用程式

```
java $JAVA_OPTS -jar < JAR File >
```

