



# Demo Scenario

```
% helm install yb-demo yugabytedb/yugabyte \
--set resource.master.requests.cpu=0.5,resource.master.requests.memory=0.5Gi,\
resource.tserver.requests.cpu=0.5,resource.tserver.requests.memory=0.5Gi,\
replicas.master=1,replicas.tserver=3 --namespace yb-demo
W1111 12:22:11.374918   60910 warnings.go:70] policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
W1111 12:22:11.377085   60910 warnings.go:70] policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
W1111 12:22:11.404141   60910 warnings.go:70] policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
W1111 12:22:11.404147   60910 warnings.go:70] policy/v1beta1 PodDisruptionBudget is deprecated in v1.21+, unavailable in v1.25+; use policy/v1 PodDisruptionBudget
NAME: yb-demo
LAST DEPLOYED: Thu Nov 11 12:22:11 2021
NAMESPACE: yb-demo
STATUS: deployed
REVISION: 1
TEST SUITE: None
NOTES:
1. Get YugabyteDB Pods by running this command:
  kubectl --namespace yb-demo get pods

2. Get list of YugabyteDB services that are running:
  kubectl --namespace yb-demo get services

3. Get information about the load balancer services:
  kubectl get svc --namespace yb-demo

4. Connect to one of the tablet server:
  kubectl exec --namespace yb-demo -it yb-tserver-0 bash

5. Run YSQL shell from inside of a tablet server:
  kubectl exec --namespace yb-demo -it yb-tserver-0 -- /home/yugabyte/bin/ysqlsh -h yb-tserver-0.yb-tservers.yb-demo

6. Cleanup YugabyteDB Pods
  For helm 2:
  helm delete yb-demo --purge
  For helm 3:
  helm delete yb-demo -n yb-demo
  NOTE: You need to manually delete the persistent volume
  kubectl delete pvc --namespace yb-demo -l app=yb-master
  kubectl delete pvc --namespace yb-demo -l app=yb-tserver

```

- run below command to access the YB Dashboard

 `minikube tunnel`


- need to check the tserver's dashboard 

`kubectl --namespace yb-demo port-forward svc/yb-tservers 9000:9000`






