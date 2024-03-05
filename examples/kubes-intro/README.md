<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/examples/kubes-intro/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Kubes Semi-Complex Kubernetes App Deployment Intro Example

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This creates a "semi-complex" app deployment with Kubes. It contains some typical, real-world resources:

1. [namespace](namespace.yaml): Namespace to group all resources together neatly.
2. [config_map](config_map.txt): To demo how configmaps work.
3. [secret](secret.txt): To demo how secrets work.
4. [deployment](deployment.yaml): Run nginx web server pods and uses the configmap and secret.
5. [service](service.yaml): Expose an endpoint to reach the nginx pods.

* It demonstrates Kubes features like layering to deploy multiple environments like dev and prod.

## Quick Start Commands

To check Kubes generated YAML files. Kind of like a DRY run. This is very useful

    kubes compile
    tree .kubes/output
    less .kubes/tmp/full.yaml # to see combined YAML for quick debugging

Deploy

    kubes deploy

You can run apply if you dont need to rebuild the Docker image

    kubes apply

View

    kubes get

Or

    kubectl config set-context --current --namespace=demo-dev
    kubectl get all,cm,secret

Check configmap and secret values

    $ kubes exec -- env | sort | grep DB_
    DB_HOST=localhost
    DB_PASS=pass
    DB_PORT=3306
    DB_USER=user

Delete

    kubes delete

## Multiple Environments

    KUBES_ENV=dev  kubes deploy
    KUBES_ENV=prod kubes deploy

## Notes

* Kubes will prune old ConfigMaps and Secrets automatically.

## Video

[![Watch the video](https://uploads-learn.boltops.com/l6f5zljat76am3fctnrokdf3l7yg)](https://learn.boltops.com/courses/kubernetes-deploy-tools/lessons/kubernetes-kubes-tool-review)

Note: Premium video content requires a subscription.
