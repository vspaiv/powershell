# powershell

# Delete pods with ImagePullBackOff condition
kubectl get pods --all-namespaces --field-selector status.phase=Pending -o json | ConvertFrom-Json | Select-Object -ExpandProperty items | Where-Object{ $_.status.containerStatuses.state.waiting.re
ason -eq "ImagePullBackOff" } | ForEach-Object { kubectl delete pod $_.metadata.name -n $_.metadata.namespace }
