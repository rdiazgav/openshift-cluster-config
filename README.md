Install the cluster operator from OperatorHUB and create a defaul instance for ArgoCD.


Then give the serviceAccount permission to admin the cluster.

```shell
oc adm policy add-cluster-role-to-user cluster-admin -z openshift-gitops-argocd-application-controller -n openshift-gitops
```

```shell
oc rollout status deploy/openshift-gitops-server -n openshift-gitops
```

To get the route

```shell
oc get routes openshift-gitops-server -n openshift-gitops -o jsonpath='{.spec.host}{"\n"}'
```

To get the admin password

```shell
oc  get secret openshift-gitops-cluster -n openshift-gitops -ojsonpath='{.data.admin\.password}' | base64 -d ; echo
```

## Deploying this Repo

To configure your cluster to this repo run

```
oc apply -k https://github.com/rdiazgav/openshift-cluster-config/cluster-config/config/overlays/default
```

This will configure your server with the following.

Cluster Configurations:
* Container Security Operator installed
* Pipelines Operator installed
* Sealed Secrets installed
* BDG application, exposing an APP that shows green or blue bubbles depending on the colour attribute you will find on the deployment file:



