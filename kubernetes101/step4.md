## Task
<pre class="file dockerfile" data-filename="routing.yaml" data-target="replace">
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: webapp-ingress
spec:
  rules:
  - host: https://[[HOST_SUBDOMAIN]]-30080-[[KATACODA_HOST]].environments.katacoda.com/
    http:
      paths:
      - path: /app
        backend:
          serviceName: webapp1-svc
          servicePort: 80
</pre>

https://[[HOST_SUBDOMAIN]]-30080-[[KATACODA_HOST]].environments.katacoda.com/