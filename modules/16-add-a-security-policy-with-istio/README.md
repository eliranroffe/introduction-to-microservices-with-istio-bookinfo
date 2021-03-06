# Adding a security policy with Istio
Note that in our setting, any microservice can access any other microservice. If any of the microservices is compromised, it can attack all the other microservice.
In this learning module we will add a security policy that states that only _reviews_ microservice can access _ratings_ microservice.

1. Let's see that without a security policy, our _sleep_ microservice can call the _ratings_ microservice.
  ```bash
  kubectl exec -it $(kubectl get pod -l app=sleep -o jsonpath='{.items[0].metadata.name}') -- curl http://ratings:9080/ratings/7
  ```

  We will get `{"id":7,"ratings":{"Reviewer1":5,"Reviewer2":4}}` as an output

2. Let's define a security policy (a whitelist) that will allow only the _reviews_ microservice to access the _ratings_ microservice:
  ```bash
  istioctl create -f whitelist-for-ratings.yaml
  ```

3. Now let's see that the _sleep_ microservice cannot access the _ratings_ microservice, as expected:
  ```bash
  kubectl exec -it $(kubectl get pod -l app=sleep -o jsonpath='{.items[0].metadata.name}') -- curl http://ratings:9080/ratings/7
  ```

  This time we will get the following error: `NOT_FOUND:whitelist-for-ratings.listchecker.default:sleep is not whitelisted`, as expected.

4. Access the webpage of the application and check that it works as expected. It will mean that the _reviews_ microservice can still access the _ratings_ microservice, as expected.
