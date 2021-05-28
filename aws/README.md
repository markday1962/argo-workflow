## Notes
Create secret files to be used in secrets
```
echo xxx> aws_access_key.txt
echo yyy> aws_secret_access_key.txt
```
Create S3 bucket
```
aws s3 mb aistemos-argo-wf
```
Create secret in the argo namespace
```
kubectl -n argo create secret generic argo-aws-credentials --from-file=access_key_id=aws_access_key.txt
kubectl -n argo create secret generic argo-aws-credentials --from-file=secret_access_key=aws_secret_access_key.txt
```

### S3 as default logging artifact
To make S3 the default logging artifact repository, we first need to edit the
`workflow-controller-configmap` configmap, could be improved with gitops.
```
kubectl -n argo edit workflow-controller-configmap
```
Updating the config map to the following
```
data:
  artifactRepository: |
    archiveLogs: true
    s3:
      bucket: aistemos-argo-wf
      endpoint: s3.amazonaws.com
      accessKeySecret:
         name: aws-credential
        key: access_key_id
      secretKeySecret:
        aws-credentials-test
        key: secret_access_key
```
