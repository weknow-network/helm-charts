# Jaeger Helm Charts

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![](https://github.com/jaegertracing/helm-charts/workflows/Release%20Charts/badge.svg?branch=main)](https://github.com/jaegertracing/helm-charts/actions)

This functionality is in beta and is subject to change. The code is provided as-is with no warranties. Beta features are not subject to the support SLA of official GA features.

## Usage

[Helm](https://helm.sh) must be installed to use the charts.
Please refer to Helm's [documentation](https://helm.sh/docs/) to get started.

Once Helm is set up properly, add the repo as follows:

```console
$ helm repo add jaeger-otpl https://weknow-network.github.io/jaeger-helm-charts-otpl
$ helm repo add jaegertracing https://jaegertracing.github.io/helm-charts
```

You can then run `helm search repo jaegertracing` to see the charts.

## Contributing

We'd love to have you contribute! Please refer to our [contribution guidelines](CONTRIBUTING.md) for details.

## License

[Apache 2.0 License](./LICENSE).

## Deploy as Open Telemetry

Replace the images for `jaeger-otpl/jaeger-opentelemetry-*`

[Read more](https://www.jaegertracing.io/docs/1.21/opentelemetry/)

```bash
helm upgrade -i jaeger -n jaeger-otpl-v1 \
        --set tag=latest \
        --set provisionDataStore.cassandra=false \
        --set provisionDataStore.elasticsearch=true \
        --set provisionDataStore.kafka=false \
        --set storage.type=elasticsearch  \
        --set ingester.image=jaegertracing/jaeger-opentelemetry-ingester \
        --set agent.image=jaegertracing/jaeger-opentelemetry-agent \
        --set collector.image=jaegertracing/jaeger-opentelemetry-collector \
        --set collector.service.http.port=55680  \
        --set admin.port=13133 \
        jaeger-otpl/jaeger
```

```bash
# one line
helm upgrade -i jaeger -n jaeger-otpl-v1 --set tag=latest --set provisionDataStore.cassandra=false --set provisionDataStore.elasticsearch=true --set provisionDataStore.kafka=false --set storage.type=elasticsearch  --set ingester.image=jaegertracing/jaeger-opentelemetry-ingester --set agent.image=jaegertracing/jaeger-opentelemetry-agent --set collector.image=jaegertracing/jaeger-opentelemetry-collector --set collector.service.http.port=55680  --set admin.port=13133 jaeger-otpl/jaeger
```

### using local '.' instead of 'jaeger-otpl/jaeger'

```bash
helm dependency update
```

```bash
helm upgrade -i jaeger -n jaeger-otpl-v1 \
        --set tag=latest \
        --set provisionDataStore.cassandra=false \
        --set provisionDataStore.elasticsearch=true \
        --set provisionDataStore.kafka=false \
        --set storage.type=elasticsearch  \
        --set ingester.image=jaegertracing/jaeger-opentelemetry-ingester \
        --set agent.image=jaegertracing/jaeger-opentelemetry-agent \
        --set collector.image=jaegertracing/jaeger-opentelemetry-collector \
        --set collector.service.http.port=55680  \
        --set admin.port=13133 \
        .
```

```bash
# one line
helm upgrade -i jaeger -n jaeger-otpl-v1 --set tag=latest --set provisionDataStore.cassandra=false --set provisionDataStore.elasticsearch=true --set provisionDataStore.kafka=false --set storage.type=elasticsearch  --set ingester.image=jaegertracing/jaeger-opentelemetry-ingester --set agent.image=jaegertracing/jaeger-opentelemetry-agent --set collector.image=jaegertracing/jaeger-opentelemetry-collector --set collector.service.http.port=55680  --set admin.port=13133 .
```

### Pack

```bash
helm package -u -d out .
```
