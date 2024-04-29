<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/aws/irsa/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# IRSA IAM roles for service accounts EKS Demo

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

Shows you how to use IRSA: [IAM roles for service accounts](https://docs.aws.amazon.com/eks/latest/userguide/iam-roles-for-service-accounts.html)

1. [deployment](deployment.yaml): Run nginx web server pods.
2. [service_account](service_account.yaml): The ServiceAccount is associated with the IAM role with an annotation.

## Create IAM Role

You must create the IAM first.

## Deploy

Note: Update the annotation with the IAM role you created.

Commands:

    kubectl create ns demo-dev
    kubectl config set-context --current --namespace=demo-dev
    kubectl apply -f service_account.yaml
    kubectl apply -f deployment.yaml

## Clean Up

Let's clean up the resources:

    kubectl config set-context --current --namespace=default
    kubectl delete ns demo-dev

Confirm all the resources have been removed:

    kubectl get all

## Video

[![Watch the video](https://uploads-learn.boltops.com/s467lsnmfwuzm87veydefj8gudsl)](https://learn.boltops.com/courses/aws-eks/lessons/eks-iam-role-for-service-account-irsa-introduction)

Note: Premium video content requires a subscription.
