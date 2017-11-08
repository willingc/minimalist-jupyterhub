# Cheatsheet: Setting up Helm

From terminal:

```bash
# run Helm's installer script
curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash

# initialize helm on your K8s cluster (run only once per K8s cluster)
      kubectl --namespace kube-system create sa tiller
      kubectl create clusterrolebinding tiller \
          --clusterrole cluster-admin \
          --serviceaccount=kube-system:tiller
      helm init --service-account tiller

# verify versions >= 2.4.1
helm version
```
