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

## Reflection on Rolling Update & Kubernetes Manifest File

**What is the difference between Rolling Update and Recreate deployment strategy?**

For Rolling Update, Kubernetes will incrementally update all of the relevant pods running the service in the cluster, while still maintaining old versions during the update. This means that the update is slowly rolled out, without introducing any downtime during the update. On the other hand the Recreate strategy will terminate all existing versions of the replicas and replacing them with the updated version. This decreases resource usage during updates, since they don't have to sustain and keep the old version, while adding the new version during the update, however it also means that during the update, the service will be down and unusable.

**Try deploying the Spring Petclinic REST using Recreate deployment strategy and document your attempt. and Prepare different manifest files for executing Recreate deployment strategy.**

To utilise the Recreate strategy I just took the deployment.yaml used previously and changed the strategy from RollingUpdate to Recreate. To actually utilise this new strategy I had deleted my minikube cluster, started a minkube cluster again, and applied the newly made yaml file (along with the service.yaml file made previously)

**What do you think are the benefits of using Kubernetes manifest files?**

The use of manifest files allows us for better efficiency, scalability and maintainability when deploying our projects. It is efficient, because as opposed to having to manually write all of the commands to deploy and expose the service with all of the necessary options set is more time consuming than just writing kubectl apply -f <manifest file>'. It allows for maintainability due to the fact that as long as you don't haphazardly edit the manifest files, all of the settings you set for the initial service will remain the same. This means that there is no chance for you to accidentally set an option incorrectly that may take a while to identify. Lastly, it allows for scalability since the yaml file itself is clear documentation of the settings of the deployment, as well as being easily configurable. Overall, it's simpler and less time consuming to just use a manifest file than having to type out all of the commands while ensuring that there are no errors.

**Deployment for group aspect**
https://tart-bass-sirered-2a271606.koyeb.app/
