On the previous step we created routing rules. If you clicked on the link, you should now see the hostname of the pod echoed on the screen. For every refresh this should be the same, since we have only one pod deployed. Let's scale that up.

https://[[HOST_SUBDOMAIN]]-80-[[KATACODA_HOST]].environments.katacoda.com/app1

## Task
To scale an app, we can do it two ways: by command or by definition. By command we use the following:
`kubectl scale deployments/webapp1 --replicas=4`{{execute}}

If you want to change it by definition, change the replica value in `deployment.yaml`. Then apply the new definition by running the following command:

`kubectl apply -f deployment.yaml`{{execute}}

Now refresh the app. You should see different hostnames echoed on the screen.

You can also check the amount of pods by running the following command:

`kubectl get pods webapp1`{{execute}}

`kubectl get deployment webapp1`{{execute}}