# A Seamless Transition: Migrating Your Service Mesh Observability from Jaeger to OpenTelemetry

for a detailed description of the steps please follow the
Red Hat developer blog [A Seamless Transition: Migrating Your Service Mesh Observability from Jaeger to OpenTelemetry](todo)

## The jaeger-all-in-onememory service (Jaeger CR)

```
oc create -f jaeger/namespace.yml
```
```
oc create -f jaeger/subscription.yml
```

### create the Jaeger instance

```
oc create -f jaeger/instance.yml
```

## The Tempo Stack service (TempoStack CR)

```
oc create -f tempo/namespace.yml
```

```
oc create -f tempo/subscription.yml
```

### create the Tempo instance

```
oc -n tempo create secret generic tempo-s3 \
  --from-literal=bucket=tempo \ 
  --from-literal=endpoint=https://s3.example.com \
  --from-literal=access_key_id=access_key_id \
  --from-literal=access_key_secret=access_key_secret \
  --dry-run=client \
  -o yaml > tempo-s3-secret.yml
```

```
oc create -f tempo-s3-secret.yml
```

```
oc create -f tempo/instance.yml
```

### create the Cluster Observability instance

```
oc create -f coo/namespace.yml
```

```
oc create -f coo/subscription.yml
```

```
oc create -f coo/uiplugin.yml
```

### create the OpenTelemetry collector instance

```
oc create -f opentelemetry/namespace.yml
```

```
oc create -f opentelemetry/subscription.yml
```

```
oc create -f opentelemetry/istio-namespace.yml
```

```
oc create -f opentelemetry/otc.yml
```

### create the ServiceMesh v2 instance

```
oc create -f ossm2/subscription.yml
```

```
oc create -f ossm2/smcp.yml
```

```
oc create -f ossm2/telemetry.yml
```

### create the ServiceMesh v3 instance

```
oc create -f ossm3/subscription.yml
```

```
oc create -f ossm2/istio.yml
```

```
oc create -f ossm2/telemetry.yml
```

