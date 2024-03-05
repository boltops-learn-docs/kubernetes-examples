<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/aws/sgp/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Pod Security Group EKS Demo

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

Shows you how to use Pod Security Groups: [Security groups for pods](https://docs.aws.amazon.com/eks/latest/userguide/security-groups-for-pods.html)

1. [security_group_policy](security_group_policy.yaml): The ServiceGroupPolicy assigns the security group to pods with matching labels.
2. [deployment](deployment.yaml): Run nginx web server pods.
3. [service](service.yaml): Expose an endpoint to reach the nginx pods.

## Create Security Group

You must create the Security Group first.

## Deploy

Note: Update the `securityGroups.groupIds` with the Security Group you created.

Commands:

    kubectl create ns demo-dev
    kubectl config set-context --current --namespace=demo-dev

    kubectl apply -f security_group_policy.yaml
    kubectl apply -f deployment.yaml
    kubectl apply -f service.yaml

## Clean Up

Let's clean up the resources:

    kubectl config set-context --current --namespace=default
    kubectl delete ns demo-dev

Confirm all the resources have been removed:

    kubectl get all

## Video

[![Watch the video](https://uploads-learn.boltops.com/zsmn6c6g891ekq4va6gccyey1irm)](https://learn.boltops.com/courses/aws-eks/lessons/eks-security-groups-for-pods)

Note: Premium video content requires a subscription.
