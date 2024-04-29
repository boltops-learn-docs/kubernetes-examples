<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/examples/config_map/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Simple Kubernetes Config Map Example

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

In this workshop, we'll create these Kubernetes resources:

1. [config_map](config_map.yaml): Config map.
2. [deployment](deployment.yaml): Run nginx web server pods.

## Deploy

Commands:

    kubectl apply -f config_map.yaml
    kubectl apply -f deployment.yaml

## Explore

List all the Kubernetes resources created:

    $ kubectl get all
    NAME                            READY   STATUS    RESTARTS   AGE
    pod/demo-web-6454d6bc76-2kmvg   1/1     Running   0          56s
    pod/demo-web-6454d6bc76-ctplj   1/1     Running   0          56s

    NAME                 TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
    service/kubernetes   ClusterIP   192.168.0.1   <none>        443/TCP   167m

    NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/demo-web   2/2     2            2           56s

    NAME                                  DESIRED   CURRENT   READY   AGE
    replicaset.apps/demo-web-6454d6bc76   2         2         2       56s
    $

## See Config Map Values

    $ kubectl exec deploy/demo-web -- env | sort | grep DB_
    DB_HOST=localhost
    DB_PORT=3306

## Cavaet

Changing config map data and updating the deployment will not update it unless the config map name as changed.

Options are:

* Change the config map name and run `kubectl apply -f deployment.yaml`
* Use `kubectl rollout restart deployment demo-web`

## Clean Up

Let's clean up the resources:

    kubectl delete -f config_map.yaml
    kubectl delete -f deployment.yaml

Confirm all the resources have been removed:

    $ kubectl get all
    NAME                 TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
    service/kubernetes   ClusterIP   192.168.0.1   <none>        443/TCP   167m
    $

## Video

[![Watch the video](https://uploads-learn.boltops.com/yblc2ipsln4m91l3zkl808dviw0y)](https://learn.boltops.com/courses/kubernetes-intro/lessons/kubernetes-configmap-resource)

Note: Premium video content requires a subscription.
