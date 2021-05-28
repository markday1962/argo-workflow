argo -n argo submit wf-input-parameter-dag.yaml
argo -n argo submit wf-input-parameter-dag.yaml -p message1="Parameter passed from terminal"
argo -n argo submit wf-input-parameter-dag.yaml --parameter-file parameters.yaml
argo -n argo list
argo -n argo delete wf-input-parameter-dag
