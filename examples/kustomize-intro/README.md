<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/examples/kustomize-intro/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Kustomize Semi-Complex Kubernetes App Deployment Intro Example

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This creates a "semi-complex" app deployment with kustomize. It contains some typical, real-world resources:

1. [namespace](namespace.yaml): Namespace to group all resources together neatly.
2. [config_map](config_map.txt): To demo how configmaps work.
3. [secret](secret.txt): To demo how secrets work.
4. [deployment](deployment.yaml): Run nginx web server pods and uses the configmap and secret.
5. [service](service.yaml): Expose an endpoint to reach the nginx pods.

* It demonstrates Kustomize features like commonLabels, namespace, and config map and secret generation.
* Comments are left in to show and explain what Kustomize does.

## Quick Start Commands

Check kustomize generated YAML file. Kind of like a DRY run. This is very useful

    kubectl kustomize .

Create

    kubectl apply -k .

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

    kubectl delete -k .

## Notes

* Kustomize doesn't seem to do a great job of cleaning up old configmaps and secrets. There's a command but it requires the standalone kustomize tool and must be manually ran. See [kustomize/issues/876](https://github.com/kubernetes-sigs/kustomize/issues/876)

## Video

[![Watch the video](https://uploads-learn.boltops.com/t1rv863pozeyrwvsndt8a5yw1r2y)](https://learn.boltops.com/courses/kubernetes-deploy-tools/lessons/kubernetes-kustomize-tool-review)

Note: Premium video content requires a subscription.
