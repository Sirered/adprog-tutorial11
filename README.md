# adprog-tutorial11

## Reflection on Hello Minikube

**Compare the application logs before and after you exposed it as a Service.**

Before exposing the service, there were only 2 logs stating which servers had been established (a TCP server in port 8080 and a UDP server on port 8081). When I expose the service, it instantly opens up my browser to access the end point, after which if I check the logs I see a GET request being received with the URI of just '/'. From there whenever I reloaded the page or accessed the endpoint again, it would log a GET request for each visit. Thus I can conclude that the logs tell me whenever there is an event, which includes requests to the service and the logs do increase every time I open the app.

**initial logs**
![image](https://github.com/Sirered/adprog-tutorial11/assets/126568984/dcc1f223-dce7-4cec-bcd5-3d0a2e9d8d23)

**after exposing**
![image](https://github.com/Sirered/adprog-tutorial11/assets/126568984/6f05f123-e459-4652-9574-e5ec0a782634)

**accessing app multiiple times**

![image](https://github.com/Sirered/adprog-tutorial11/assets/126568984/822718dd-71fa-4cea-9372-3ac24c86c220)

**Notice that there are two versions of `kubectl get` invocation during this tutorial section.**

-n stands for --namespace. A namespace basically acts like a separate workspace, where all services and processes initialised or handled in one namespace will only show up in that namespace, similar to SCHEMAs in a database or a branch in github. Normally when you don't specify namespace, it will default to the namespace named default, so since we didn't specify a namespace when creating our services, our services will be found on the default namespace and when we call kubectl get services, without specifying namespace, it will also only retrieve the services found on default, hence why we see the services we created when running that command. Kubernetes also provides a namespace named kube-system specifically to hold system components or infrastructure-related resources, including the metric-server service, hence why you can only see the metric-server when you run the command with -n kube-system. Hence overall, stuff we make without specifying namespace will be found on default and will be fetched when we run the get with no namespace specified, while packages and addons will likely run on kube-system, which means that we would have to specify the kube-system namespace to get them.

