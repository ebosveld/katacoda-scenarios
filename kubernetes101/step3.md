So far our app has been deployed to _pods_ and is being load balanced by a _service_. Now we want to create an _ingress controller_ to direct incoming traffic to the right service.

## Task
Normally we'd create an _ingress controller_ by a definition as we've done with the other steps, but in this sandbox that is not possible. Fortunately the tool allows us to enable an addon to do that. Execute the following command.

`minikube addons enable ingress`{{execute}}

Now we need to tell the ingress controller how to route the traffic. We do this by creating an _ingress_ component with routing rules. In the following example we use `[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com` as hostname so we can actually try it out. We map /app1 to the load balancing service called _webapp1-svc_.

Copy the definition below.

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

Once this is copied into the editor you can type in the following command in the terminal to create the routing rules.
`kubectl apply -f routing.yaml`{{execute}}

Check the status using the following commands:
`kubectl get ing`{{execute}}

`kubectl describe ing`{{execute}}

Check the page using the following link:
https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/app1