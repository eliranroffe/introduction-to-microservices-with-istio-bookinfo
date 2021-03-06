# Deploy Bookinfo application that uses _ratings_ microservice in Kubernetes

This learning module shows you an application of four microservices: _productpage_, _details_, _ratings_ and _reviews_. The application is called Bookinfo and is described [here](https://istio.io/docs/guides/bookinfo.html). Consider the application there as the final version, in which the _reviews_ microservice has three versions _v1_, _v2, _v3_. In this module we start with the application with the first version of the _reviews_ microservice, _v1_. In the next modules, we will evolve the application.

1. Skim `bookinfo.yaml` - this is a Kubernetes deployment spec of the app. Notice the services and the deployments, and also the replication: 3 replicas of each microservice.

1. Deploy to Kubernetes.
  ```
  kubectl apply -f bookinfo.yaml
  ```
1. Check the pods status. Notice that each microservice has three pods.
   ```
   kubectl get pods
   ```
1. Edit `ingress.yaml` - specify your host instead of `your host`.
    * For Bluemix, get your host by running: `bx cs clusters`, `bx cs cluster-get <your cluster>`, `Ingress subdomain` field.

1. Deploy your ingress:
   ```
   kubectl apply -f ingress.yaml
   ```

1. Access `http://<your host>/productpage`.

1. Observe how microservices call each other, for example, _reviews_ calls _ratings_ microservice by the URL `http://ratings:9080/ratings`:
   ```bash
   more ../samples/bookinfo/src/reviews/reviews-application/src/main/java/application/rest/LibertyRestEndpoint.java
   ```

   Observe the following line:
   ```java
   private final static String ratings_service = "http://ratings:9080/ratings";
   ```
