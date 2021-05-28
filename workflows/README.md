### Workflow Templates
https://argoproj.github.io/argo-workflows/workflow-templates/
Create argo template that is stored in the cluster
```
argo -n argo template create wftmpl-dag.yaml
```
List argo templates
```
argo -n argo template list
```
Submit workflow template to create a new workflow
```
argo -n argo submit --from workflowtemplate/wftmpl-dag
```
Updating a template involves first deleting the template, then recreating it.
```
argo -n argo delete wftmpl-dag
argo -n argo template create wftmpl-dag.yaml
```
If deleting a template is prefered it can be updated with kubectl by editing
the template and applying it.
```
kubectl -n argo apply -f wftmpl-dag.yaml
```

### Cluster Workflow Templates
As the name implies a cluster workflow template is available across all name
spaces in the cluster

Create cluster workflow template
```
argo -n argo cluster-template create clusterwftmpl-dag.yaml
```
List cluster template in all namespaces
```
argo -n argo cluster-template list
```

### Workflow archiving
When workflow archiving is enabled they are archived in a postgres database

```
kubectl -n argo port-forward deployment/postgres 5432:5432
```
pgadmin can now be used to connect to the database
```
Username: postgres
Password: password
```
The table argo_archived_workflows contains the archived workflows
