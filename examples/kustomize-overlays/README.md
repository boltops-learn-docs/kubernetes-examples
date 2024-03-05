<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/examples/kustomize-overlays/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Kustomize More-Complex Kubernetes App Deployment Example with Separate Environments

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

Blog Post: [Kustomize vs Helm vs Kubes: Kubernetes Deploy Tools](https://blog.boltops.com/2020/11/05/kustomize-vs-helm-vs-kubes-kubernetes-deploy-tools)

Overlays example with namespace to separate environments like dev and prod.

## Structure

Here's the general structure

    ├── base
    │   ├── deployment.yaml
    │   ├── kustomization.yaml
    │   └── service.yaml
    └── overlays
        ├── dev
        │   ├── config_map.txt
        │   ├── deployment.yaml
        │   ├── kustomization.yaml
        │   ├── namespace.yaml
        │   └── secret.txt
        └── prod
            ├── config_map.txt
            ├── deployment.yaml
            ├── kustomization.yaml
            ├── namespace.yaml
            └── secret.txt

## Dry Run

    kubectl kustomize overlays/dev
    kubectl kustomize overlays/prod

## Apply

    kubectl apply -k overlays/dev
    kubectl apply -k overlays/prod

## Video

[![Watch the video](https://uploads-learn.boltops.com/t1rv863pozeyrwvsndt8a5yw1r2y)](https://learn.boltops.com/courses/kubernetes-deploy-tools/lessons/kubernetes-kustomize-tool-review)

Note: Premium video content requires a subscription.
