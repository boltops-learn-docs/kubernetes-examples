<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/examples/semi-complex/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Semi-Complex Kubernetes App Deployment

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This creates a "semi-complex" app deployment. It contains some typical, real-world resources:

1. [namespace](namespace.yaml): Namespace to group all resources together neatly.
2. [config_map](config_map.yaml): To demo how configmaps work.
3. [secret](secret.yaml): To demo how secrets work.
4. [deployment](deployment.yaml): Run nginx web server pods and uses the configmap and secret.
5. [service](service.yaml): Expose an endpoint to reach the nginx pods.

Am considering this semi-complex because:

* Resources are organized a dedicated namespace vs the default namespace.
* ConfigMaps and Secrets are used which require updating deployment manually.

The kubernetes YAML files will inevitably get more complex when you need:

* multiple process types. IE: web, worker, scheduler.
* multiple environments. IE: dev, test, prod.
* command sidecars. IE: monitoring, sqlproxy.

This example demonstrates a semi-complex app deployment to show how things start to get difficult to manage. Hence folks reach for tools to help like [Kubes](https://kubes.guru/), [Kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/), [Helm](https://helm.sh/).

## Quick Start Commands

Create

    kubectl apply -f namespace.yaml
    kubectl apply -f config_map.yaml
    kubectl apply -f secret.yaml
    kubectl apply -f deployment.yaml
    kubectl apply -f service.yaml

View

    kubectl config set-context --current --namespace=demo
    kubectl get all,cm,secret

Check configmap and secret values

    $ kubectl exec deploy/demo-web -- env | sort | grep DB_
    DB_HOST=localhost
    DB_PASS=pass
    DB_PORT=3306
    DB_USER=user

Delete

    kubectl delete -f service.yaml
    kubectl delete -f deployment.yaml
    kubectl delete -f secret.yaml
    kubectl delete -f config_map.yaml
    kubectl delete -f namespace.yaml
