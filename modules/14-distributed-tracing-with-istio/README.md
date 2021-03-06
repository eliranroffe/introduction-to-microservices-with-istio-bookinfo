# Distributed tracing with Istio
In this learning module, we will add [Zipkin distributed trace system](https://zipkin.io) as part of our Istio infrastructure.

1. Deploy a Zipkin instance:
  ```bash
  kubectl apply -f ../../istio-*/install/kubernetes/addons/zipkin.yaml
  ```
2. Check the pods at istio-system namespaces and wait for the pod of Zipkin to start running:
  ```bash
  kubectl get pods -n istio-system
  ```
2. Perform port forwarding from the Zipkin instance to the local machine:
  ```bash
  kubectl port-forward -n istio-system $(kubectl get pod -n istio-system -l app=zipkin -o jsonpath='{.items[0].metadata.name}') 9411:9411 &
  ```

3. Access the Zipkin dashboard on local machine: http://localhost:9411
