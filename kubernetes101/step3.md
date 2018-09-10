So far our app has been deployed to _pods_ and is being load balanced by a _service_. Now we want to create an _ingress controller_ to direct incoming traffic to the right service.

## Task
Copy the definition from below. This creates an _ingress controller_ based on Nginx and creates a load balancer _service_ for the ingress controller.

`minikube addons enable ingress`{{execute}}


<pre class="file dockerfile" data-filename="routing.yaml" data-target="replace">
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: webapp-ingress
spec:
  rules:
  - host: [[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com
    http:
      paths:
      - path: /app1
        backend:
          serviceName: webapp1-svc
          servicePort: 80
</pre>

https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/