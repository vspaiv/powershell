# powershell

# Delete pods with ImagePullBackOff condition
 kubectl get pods -n prod-ms --field-selector status.phase=Pending -o json | ConvertFrom-Json | Select-Object -ExpandProperty items | Where-Object{ $_.status.containerStatuses.state.waiting.reason -eq "ImagePullB
ackOff" } | ForEach-Object { kubectl delete pod $_.metadata.name -n $_.metadata.namespace } 
