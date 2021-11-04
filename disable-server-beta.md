### Disabling the cost-analyzer-server Container

Kubecost supports configuring inclusion of the cost-analyzer-server container in the cost-analyzer pod by modifying `.Values.kubecost.disableServer` in your [values.yaml](https://github.com/kubecost/cost-analyzer-helm-chart/blob/49601682dcbdcfe67b724aa5c0d5bcd346b98a4f/cost-analyzer/values.yaml#L198).
  
### Saved Report Parameters  
Currently this is a beta feature, and disabling the container can lead to unexpected behavior. Listed here are potential issues that may be encountered.

All endpoints with the format `<your-kubecost-address>/api/` are unavailable when the server is disabled. For allocation and asset API queries, as well as for Prometheus/Thanos, these can be routed to `<your-kubecost-address>/model/` instead. However, there are a number of endpoints which do not have a `/model/` equivalent:
- `/cpuRequestsVsUsage`
- `/clusterName`
- `/secretsIssue`
- `/allJobs`
- `/podsByDeployment`
- `/podsToMove`
- `/s3PriceData`
- `/addAthenaBucket`
- `/getAthenaBucket`
- `/getSpotInfo`
- `/setSpotInfo`
- `/getNamespaceAttributes`
- `/setNamespaceAttributes`
- `/getBudget`
- `/setBudget`

Cluster autoscaling functionality is also tied to the server, making endpoints such as `/api/explainCA` and `/api/nodeTurndownChecks` similarly inaccessible.

Finally, note that certain frontend features will not work without the server, chiefly `savings.html`. However, the allocation and asset reports pages will function regardless.

Implementation of these features independent from the server is projected to happen by the end of December 2021.


