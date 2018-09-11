In the previous step we created a deployment with 1 replica. So we have one pod running our app. Pods are ephemeral, which means that everytime a new pod is created or our spec is updated it get's a new internal IP. To be able to counter this we create a _service_.

## Task
Copy the definition from below. This creates a _service_ which selects all pods which are labeled with _webapp1_ and exposes it on an internal IP. Once we get multiple replicas of our pods this will also act as a _load balancer_.

<pre class="file dockerfile" data-filename="service.yaml" data-target="replace">
apiVersion: v1
kind: Service
metadata:
  name: webapp1-svc
  labels:
    app: webapp1
spec:
  type: ClusterIP
  ports:
  - port: 80
  selector:
    app: webapp1
</pre>

Once this is copied into the editor you can type in the following command in the terminal to create the service.

`kubectl apply -f service.yaml`{{execute}}

To see if the deployment is ready, type the following command in the terminal.

`kubectl get services`{{execute}}

## Pro tip
We can also give our service an external IP. Do this by changing the type to `LoadBalancer`.