# Installing on Kubernetes

## Installing with `kubectl`

#### What you'll need

1. Kubernetes v1.8+ or higher deployed. We recommend using [minikube](https://kubernetes.io/docs/getting-started-guides/minikube/) to get a demo cluster up quickly.
1. [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed on your local machine.

Once your Kubernetes cluster is up and running, run the following command to deploy QLoo and Gloo to the `gloo-system` namespace:

```bash
# install Gloo
kubectl apply -f \
    https://raw.githubusercontent.com/solo-io/gloo/master/install/kube/install.yaml

# install QLoo
kubectl apply -f \
    https://raw.githubusercontent.com/solo-io/qloo/master/install/kube/install.yaml
```


## Installing with `qlooctl`

#### What you'll need

1. Kubernetes v1.8+ or higher deployed. We recommend using [minikube](https://kubernetes.io/docs/getting-started-guides/minikube/) to get a demo cluster up quickly.
1. [`kubectl`](https://kubernetes.io/docs/tasks/tools/install-kubectl/) installed on your local machine.
1. [`qlooctl`](https://github.com/solo-io/qloo/releases/) installed on your local machine.

Once your Kubernetes cluster is up and running, run the following command to deploy QLoo and Gloo to the `gloo-system` namespace:

```bash
qlooctl install kube 
```

## Confirming the installation

Check that the Gloo pods and services have been created:

```bash
kubectl get all -n gloo-system
NAME                                           READY     STATUS    RESTARTS   AGE
pod/control-plane-757bd75db7-9vw59             1/1       Running   0          2h
pod/function-discovery-7df6bd4fcd-26rx8        1/1       Running   0          2h
pod/ingress-77c7bd6577-kdgdd                   1/1       Running   0          2h
pod/kube-ingress-controller-78bfc4c84d-8tvjr   1/1       Running   0          2h
pod/qloo-6b79fdc655-n7j6n                      2/2       Running   0          2h
pod/upstream-discovery-59bc6f7889-g65z6        1/1       Running   0          2h

NAME                    TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)                         AGE
service/control-plane   ClusterIP      10.96.24.217     <none>        8081/TCP                        3h
service/ingress         LoadBalancer   10.111.152.102   <pending>     8080:31972/TCP,8443:30576/TCP   3h
service/qloo            LoadBalancer   10.106.92.208    <pending>     9090:31470/TCP                  3h

NAME                                      DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/control-plane             1         1         1            1           3h
deployment.apps/function-discovery        1         1         1            1           3h
deployment.apps/ingress                   1         1         1            1           3h
deployment.apps/kube-ingress-controller   1         1         1            1           3h
deployment.apps/qloo                      1         1         1            1           3h
deployment.apps/upstream-discovery        1         1         1            1           3h

NAME                                                 DESIRED   CURRENT   READY     AGE
replicaset.apps/control-plane-757bd75db7             1         1         1         3h
replicaset.apps/function-discovery-7df6bd4fcd        1         1         1         3h
replicaset.apps/ingress-77c7bd6577                   1         1         1         3h
replicaset.apps/kube-ingress-controller-78bfc4c84d   1         1         1         3h
replicaset.apps/qloo-6b79fdc655                      1         1         1         3h
replicaset.apps/upstream-discovery-59bc6f7889        1         1         1         3h
```

Everything should be up and running. If this process does not work, please [open an issue](https://github.com/solo-io/qloo/issues/new). We are happy to answer
questions on our [diligently staffed Slack channel](https://slack.solo.io/).

See [Getting Started on Kubernetes](../getting_started/kubernetes/1.md) to get started creating your first GraphQL endpoint with QLoo.
