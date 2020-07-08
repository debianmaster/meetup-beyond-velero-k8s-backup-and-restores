## Install velero

```
velero install \
--provider aws \
--plugins velero/velero-plugin-for-aws:v1.0.0 \
--bucket velero \
--use-volume-snapshots=false \
--secret-file ./credentials-velero \
--use-restic \
--backup-location-config region=minio,s3ForcePathStyle="true",s3Url=http://13.250.45.75.nip.io:9000
```

## Deploy app
```
kubectl apply -f https://bit.ly/k8s-app
```

## Take backup from default namespace
```
velero create backup backup1 --snapshot-volumes --include-namespaces=default
```

## Simulate disaster
```
k delete all,pvc --all -n default
```


## Restore
```
velero create restore restore1 
```

## Check workload
```
kubectl get all,pvc -n default
```


