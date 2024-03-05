<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/examples/secret/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Simple Kubernetes Secret Example

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

In this workshop, we'll create these Kubernetes resources:

1. [secret](secret.yaml): Secret.
2. [deployment](deployment.yaml): Run nginx web server pods.

## Deploy

Commands:

    kubectl apply -f secret.yaml
    kubectl apply -f deployment.yaml

## See Secret Values

    $ kubectl exec deploy/demo-web -- env | sort | grep DB_
    DB_USER=user
    DB_PASS=pass

## Cavaet

Changing secret data and updating the deployment will not update it unless the secret name as changed.

Options are:

* Change the secret name and run `kubectl apply -f deployment.yaml`
* Use `kubectl rollout restart deployment demo-web`

## Tips

You can use base64 to see confirm the values:

    $ echo "dXNlcg==" | base64 -d
    user
    $ echo "cGFzcw==" | base64 -d
    pass

And to encode

    $ echo "user" | base64
    dXNlcgo=
    $ echo "pass" | base64
    cGFzcwo=

## Clean Up

Let's clean up the resources:

    kubectl delete -f secret.yaml
    kubectl delete -f deployment.yaml

Confirm all the resources have been removed:

    $ kubectl get all∑
    NAME                 TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
    service/kubernetes   ClusterIP   192.168.0.1   <none>        443/TCP   167m
    $

## Video

[![Watch the video](https://uploads-learn.boltops.com/ho85oe4skogk50153gg8sml05xby)](https://learn.boltops.com/courses/kubernetes-intro/lessons/kubernetes-secret-resource)

Note: Premium video content requires a subscription.
