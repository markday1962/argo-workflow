## Notes
Create password file
```
echo Password123 > test_password_file.txt
```
Once the test_password_file.txt has bee created open the file and remove the CRLF
Create Secret
```
kubectl -n argo create secret generic test-secret --from-file=test-password=test_password_file.txt
```
