# ossm-complete demo

module contains stuff to be done during demo

# TODO: Tempo compactor requires minio bucket to be setup for dt so will block
# Resolved through TODO: ACTION [MINIO-SETUP]

# TODO: ACTION [MINIO-SETUP] -> minio bucket setup

oc port-forward svc/minio 9000:9000 -n tempo &
sleep 2

curl -sL https://dl.min.io/client/mc/release/linux-amd64/mc -o /tmp/mc
chmod +x /tmp/mc

/tmp/mc alias set minio http://localhost:9000 tempo tempo123
/tmp/mc mb minio/tempo
/tmp/mc ls minio

kill %1


# TODO: Debug OTEL integration with istio

```
WAYPOINT=$(kubectl get pod -n bookinfo -l gateway.istio.io/managed=istio.io-mesh-controller -o jsonpath='{.items[0].metadata.name}')
echo $WAYPOINT
```

```
istioctl proxy-config listener -n bookinfo $WAYPOINT -o json | \
  python3 -c "
import json, sys
data = json.load(sys.stdin)
for r in data:
    for fc in r.get('filterChains', []):
        for f in fc.get('filters', []):
            ht = f.get('typedConfig', {}).get('httpFilters', [])
            tc = f.get('typedConfig', {}).get('tracing', {})
            if tc:
                print(json.dumps(tc, indent=2))
"
```


# TODO: Confirm ztunnel logs mtls

port 15008

oc logs -n ztunnel -l app=ztunnel | grep ":15008" | head -20

oc logs -n ztunnel -l app=ztunnel | grep -E "src.identity|dst.identity" | head -20

oc logs -n ztunnel -l app=ztunnel |   grep "connection complete" |   grep -E "spiffe://" |   awk '{print $0}' |   tail -5

