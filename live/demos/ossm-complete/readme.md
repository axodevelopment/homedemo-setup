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