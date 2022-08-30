# Determine Supported Values for Helm Chart

Helm charts can be configured with yaml files. 
When I first tried this I was totally clueless about helm and didn't even have it installed.
I knew my Helm chart was at https://googlecloudplatform.github.io/spark-on-k8s-operator, but that's pretty much it.

```bash
$ brew install helm
[...]

$ helm repo add spark https://googlecloudplatform.github.io/spark-on-k8s-operator
"spark" has been added to your repositories

$ helm search repo spark
NAME                	CHART VERSION	APP VERSION        	DESCRIPTION
spark/spark-operator	1.1.25       	v1beta2-1.3.7-3.1.1	A Helm chart for Spark on Kubernetes operato

❯ helm show values spark/spark-operator
# Default values for spark-operator.
# This is a YAML-formatted file.
# Declare variables to be passed into your templates.

# replicaCount -- Desired number of pods, leaderElection will be enabled
# if this is greater than 1
replicaCount: 1
[...]
```

That's it.



