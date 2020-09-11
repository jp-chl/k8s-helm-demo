# k8s-helm-demo

This is a simple demo in order to deploy a microservice with Helm.

## Helm installation (on linux)

(Version 3 is used)

``` curl -sSL https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash ```

```helm version --short```
> (v3.3.0+g8a4aeec)

```helm repo add stable https://kubernetes-charts.storage.googleapis.com/```

```helm completion bash >> ~/.bash_completion```

```. /etc/profile.d/bash_completion.sh```

```. ~/.bash_completion```

``` source <(helm completion bash)```

---
``` helm repo add stable https://kubernetes-charts.storage.googleapis.com/```

``` helm repo update```

``` helm repo add bitnami https://charts.bitnami.com/bitnami```

``` helm repo update```

---

## Demo

``` kubectl create ns nstest```

``` helm install --debug --dry-run poc-helm k8s-demo```
> _(helm install options expectedName folder)_

_(Check all templates are valid)_

``` helm install poc-helm k8s-demo```

> _(service, deployment and pod must be up and running correctly)_

Check environmental variables are set correctly in pods:

```kubectl exec -ti $(kubectl get pods -n nstest -o jsonpath='{.items[0].metadata.name}') -n nstest -- /bin/bash```
* In the pod, run: ```env|sort -u|head -3```

> _You should have found the environmental variables set in [deployment template](k8s-demo/templates/deployment)_

Cleanup:

``` helm uninstall poc-helm```
