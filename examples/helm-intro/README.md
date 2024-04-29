<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/examples/helm-intro/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Helm Semi-Complex Kubernetes App Deployment Example

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This creates a "semi-complex" app deployment with helm. It contains some typical, real-world resources:

1. [namespace](namespace.yaml): Namespace to group all resources together neatly.
2. [config_map](config_map.txt): To demo how configmaps work.
3. [secret](secret.txt): To demo how secrets work.
4. [deployment](deployment.yaml): Run nginx web server pods and uses the configmap and secret.
5. [service](service.yaml): Expose an endpoint to reach the nginx pods.

## Structure

Here's the general structure:

    ├── Chart.yaml
    ├── README.md
    ├── templates
    │   ├── configmap.yaml
    │   ├── deployment.yaml
    │   ├── _helpers.tpl
    │   ├── NOTES.txt
    │   ├── secret.yaml
    │   ├── service.yaml
    │   └── serviceaccount.yaml
    └── values.yaml

One interesting note about how helm works with namespaces is that the `--namespace` option, helm switches to the namespace to creates the resources. So the namespace field does not have to be set in the YAML files themselves.

## Create Different Environments

dev:

    helm install chart-dev . --namespace chart-dev --create-namespace -f values/dev.yaml
    helm ls -n chart-dev
    kubectl get all,cm,secret,sa -n chart-dev

prod:

    helm install chart-prod . --namespace chart-prod --create-namespace -f values/prod.yaml
    helm ls -n chart-prod
    kubectl get all,cm,secret,sa -n chart-prod

## Upgrade

    helm upgrade chart-dev . --namespace chart-dev -f values/dev.yaml
    helm upgrade chart-prod . --namespace chart-prod -f values/prod.yaml

## Cleanup

    helm uninstall chart-dev -n chart-dev
    kubectl delete ns chart-dev  # cleanup namespace
    helm uninstall chart-prod -n chart-prod
    kubectl delete ns chart-prod # cleanup namespace

## Video

[![Watch the video](https://uploads-learn.boltops.com/oobuo0q2cy91yklrggqj0x8sp5yo)](https://learn.boltops.com/courses/kubernetes-deploy-tools/lessons/kubernetes-helm-tool-review)

Note: Premium video content requires a subscription.
