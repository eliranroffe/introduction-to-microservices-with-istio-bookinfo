# Tutorial cleanup

1. Undeploy Bookinfo:
  ```bash
  kubectl delete -f <(istioctl kube-inject -f ../03-run-bookinfo-with-kubernetes/bookinfo.yaml)
  kubectl delete -f <(istioctl kube-inject -f ../03-run-bookinfo-with-kubernetes/ingress.yaml)
  kubectl delete -f <(istioctl kube-inject -f ../05-adding-a-new-version-of-a-microservice/bookinfo-reviews-v2-with-app-label.yaml)
  kubectl delete -f <(istioctl kube-inject -f ../10-ab-testing-with-istio/bookinfo-reviews-v3.yaml)
  kubectl delete -f ../../istio-*/samples/sleep/sleep.yaml
  ```

2. Undeploy Istio with all addons:
  ```bash
  kubectl delete -f ../../istio-*/install/kubernetes/istio.yaml
  ```
