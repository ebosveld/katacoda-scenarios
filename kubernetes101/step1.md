To get started we're going to create a deployment object. This is one of the most commonly used object and represents a set of containers - or _replicas_.
## Task
Copy the definition from below. This launches an application called _webapp1_ which uses the `katacoda/docker-http-server` docker image for it's containers on port _80_. This is just a basic NGINX web server which echoes the host name back.

<pre class="dockerfile" data-filename="deployment.yaml" data-target="replace">
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: webapp1
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: webapp1
    spec:
      containers:
      - name: webapp1
        image: katacoda/docker-http-server:latest
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: webapp1-svc
  labels:
    app: webapp1
spec:
  ports:
  - port: 80
  selector:
    app: webapp1
</pre>

Once this is copied into the editor you can type in the following command in the terminal to start the deployment.
`kubectl create -f deployment.yaml`{{execute}}

To see if the deployment is ready, type the following command in the terminal.
`kubectl get deployments`{{execute}}

To see the actual pods, use the following command.
`kubectl get pods`{{execute}}

## Pro tip
Never used Katacoda before? Noticed there's a button "copy to editor" next to the code samples? Also you can click on the commands and it will be executed in the terminal.