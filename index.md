# Jaeger Tracing Helm Repository

![Jaeger](https://www.jaegertracing.io/img/jaeger-logo.png)

## Add the Jaeger Tracing Helm repository

```bash
helm repo add jaegertracing https://weknow-network.github.io/jaeger-helm-charts-otpl
```

## Install Jaeger

```bash
helm upgrade -i jaeger jaegertracing/jaeger
```

For more details on installing Jaeger please see the [chart's README](https://github.com/jaegertracing/helm-charts/tree/master/charts/jaeger).

## Install Jaeger Operator

```bash
helm upgrade -i jaeger-operator jaegertracing/jaeger-operator
```

## Deploy for Open Telemetry image

Replace the images for `jaegertracing/jaeger-opentelemetry-*`

```bash
helm upgrade -i jaeger -n jaeger-otpl-v1 --set tag=latest --set provisionDataStore.cassandra=false --set provisionDataStore.elasticsearch=true --set provisionDataStore.kafka=false --set storage.type=elasticsearch  --set ingester.image=jaegertracing/jaeger-opentelemetry-ingester --set agent.image=jaegertracing/jaeger-opentelemetry-agent --set collector.image=jaegertracing/jaeger-opentelemetry-collector --set collector.service.http.port=55680  --set admin.port=13133 jaegertracing/jaeger
```

### using local '.' instead of 'jaegertracing/jaeger'

```bash
helm dependency update ./charts/jaeger

helm upgrade -i jaeger -n jaeger-otpl-v1 --set tag=latest --set provisionDataStore.cassandra=false --set provisionDataStore.elasticsearch=true --set provisionDataStore.kafka=false --set storage.type=elasticsearch  --set ingester.image=jaegertracing/jaeger-opentelemetry-ingester --set agent.image=jaegertracing/jaeger-opentelemetry-agent --set collector.image=jaegertracing/jaeger-opentelemetry-collector --set collector.service.http.port=55680  --set admin.port=13133 ./charts/jaeger
```

### Pack

```bash
helm package -u -d out .
```

For more details on installing Jaeger Operator please see the [chart's README](https://github.com/jaegertracing/helm-charts/tree/master/charts/jaeger-operator).
