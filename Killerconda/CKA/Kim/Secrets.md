
View Secrets
```bash
kubectl get secrets 
```

View Secrets in JSON
```bash
kubectl get secrets <secrets_name> -o json
```

Output:
```bash
{
    "apiVersion": "v1",
    "data": {
        "DB_PASSWORD": "c2VjcmV0"
    },
    "kind": "Secret",
    "metadata": {
        "creationTimestamp": "2025-05-07T06:43:08Z",
        "name": "database-data",
        "namespace": "database-ns",
        "resourceVersion": "2746",
        "uid": "f746a8ef-a755-47de-949d-3561eeb90182"
    },
    "type": "Opaque"
}
```

## Decode the PASSWORD

### Extract the password using jsonpath
```bash
kubectl get secrets <secret_name> -o jsonpath='.{data.DB_PASSWORD}'
```

Output:
```bash
c2VjcmV0
```

### Decode the output
```bash
echo "c2VjcmV0" | base64 --decode
```

Output:
```bash
secret
```

### Final Merged Command
```bash
kubectl get secret <secret-name> -o jsonpath='{.data.DB_PASSWORD}' | base64 --decode
```

Output:
```bash
secret
```
