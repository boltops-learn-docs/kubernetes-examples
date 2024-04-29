<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-learn/kubernetes-examples/blob/master/google/ilb-https-pre-shared/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# GKE Ingress HTTPS Internal Load Balancer Kubernetes Example

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

We'll create these Kubernetes resources:

1. [deployment](deployment.yaml): Run nginx web server pods.
2. [service](service.yaml): Expose an endpoint to reach the nginx pods.
3. [ingress](ingress.yaml): Expose an endpoint to reach the nginx pods.

Relevant Google Cloud Docs: [Configuring Ingress for Internal HTTP(S) Load Balancing: HTTPS between client and load balancer](https://cloud.google.com/kubernetes-engine/docs/how-to/internal-load-balance-ingress#https_between_client_and_load_balancer)

## Create Google SSL Cert

    export GOOGLE_REGION=us-central1
    gcloud compute ssl-certificates create google-ssl-cert-$GOOGLE_REGION-v1 --region $GOOGLE_REGION --certificate certificate.crt --private-key private.key

## Deploy

Go back to ilb-https-pre-shared folder

    cd ~/environment/kubernetes-examples/google/ilb-https-pre-shared

Commands:

    kubectl apply -f deployment.yaml
    kubectl apply -f service.yaml
    kubectl apply -f ingress.yaml

Example with output:

    $ kubectl apply -f deployment.yaml
    deployment.apps/demo-web created
    $ kubectl apply -f service.yaml
    service/demo-web created
    $ kubectl apply -f ingress.yaml
    ingress/demo-web created
    $

## Explore

List all the Kubernetes resources created:

    $ kubectl get all
    NAME                            READY   STATUS    RESTARTS   AGE
    pod/demo-web-6454d6bc76-2kmvg   1/1     Running   0          56s
    pod/demo-web-6454d6bc76-ctplj   1/1     Running   0          56s

    NAME                 TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
    service/demo-web     ClusterIP   192.168.0.89   <none>        80/TCP    52s
    service/kubernetes   ClusterIP   192.168.0.1   <none>        443/TCP   167m

    NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
    deployment.apps/demo-web   2/2     2            2           56s

    NAME                                  DESIRED   CURRENT   READY   AGE
    replicaset.apps/demo-web-6454d6bc76   2         2         2       56s
    $

Notice the replicaset is created by the deployment.  The replicaset in turn creates the pods. We only directly manage the deployment and service resources.

Hop into the pod container and `curl localhost`:

    $ kubectl exec -ti pod/demo-web-6454d6bc76-2kmvg bash
    # curl -s localhost | grep title
    <title>Welcome to nginx!</title>
    # curl -s 192.168.0.89 | grep title
    <title>Welcome to nginx!</title>
    # curl -s demo-web.default | grep title
    <title>Welcome to nginx!</title>
    # curl -s demo-web | grep title
    <title>Welcome to nginx!</title>
    # exit
    $

Notice we can curl with localhost, the service IP, or friendly DNS endpoints. The pretty endpoints are automatically created by Kubernetes.

## Tester Container

Using a container to test can be useful. Example

    $ kubectl run tester -ti --rm --restart=Never --image amazonlinux:2 bash
    # curl -s 192.168.0.89 | grep title

Note: You might have to add the root to:

    /etc/ssl/certs/ca-bundle.crt

## Clean Up

Let's clean up the resources:

    kubectl delete -f ingress.yaml
    kubectl delete -f service.yaml
    kubectl delete -f deployment.yaml

Confirm all the resources have been removed:

    $ kubectl get all
    NAME                 TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)   AGE
    service/kubernetes   ClusterIP   192.168.0.1   <none>        443/TCP   167m
    $
