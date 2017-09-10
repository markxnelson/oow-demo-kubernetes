# Instructions to run the demo in Kubernetes

Note: These instructions are tested with Google Cloud Platform. 

Create the database deployment:

```
kubectl create -f database-deployment.yaml
```

Create a database service: 

```
kubectl create -f database-service.yaml
```

Create the weblogic deployment:

```
kubectl create -f weblogic-deployment.yaml
```

Create a weblogic service:

```
kubectl create -f weblogic-service.yaml
```

Expose the weblogic service using a load balancer:

```
kubectl expose deployment weblogic --type=LoadBalancer --name=oow-load-balancer
```

