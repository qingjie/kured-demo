
```
# ssh to node:
kubectl debug node/aks-agentpool-16711687-vmss000002 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0
#: https://docs.microsoft.com/en-us/azure/aks/node-access


# Schedule Node restarts with Kured:

helm repo add kured https://weaveworks.github.io/kured

helm upgrade kured kured/kured --namespace kured --install --create-namespace \
--set nodeSelector."beta\.kubernetes\.io/os"=linux \
--set configuration.startTime=9am \
--set configuration.endTime=5pm \
--set configuration.timeZone="America/New_York"
# --set configuration.rebootDays="[mo,tu,we,th,fr]"

kubectl get po -n kured -o wide

kubectl logs kured-vbgc6 -n kured

helm delete kured -n kured
```
