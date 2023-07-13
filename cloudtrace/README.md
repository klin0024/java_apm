# GCP Cloud Trace for JAVA

1. 建立 SA `cloudtrace-sa` 並賦予角色 `roles/cloudtrace.agent`

2. 拉取 Source Code

```
git clone https://github.com/klin0024/java_apm.git
cd java_apm/cloudtrace
```

3. 設置環境變數

```
export GOOGLE_CLOUD_PROJECT=< Project ID >
export GOOGLE_APPLICATION_CREDENTIALS=< Service Account Key >
export OTEL_TRACES_EXPORTER=google_cloud_trace
export OTEL_METRICS_EXPORTER=none
export JAVA_OPTS="-javaagent:opentelemetry-javaagent.jar -Dotel.javaagent.extensions=opentelemetry-operations-java.jar"
```

4. 執行 JAVA 應用程式

```
java $JAVA_OPTS -jar app.jar
```

