# Instructions to run the demo in Kubernetes

Note: These instructions are tested with Google Cloud Platform. 

Create secrets to allow you to pull the images:

```
kubectl create secret docker-registry regsecret --docker-server=container-registry.oracle.com --docker-username=YOUR_USERNAME --docker-password=YOUR_PASSWORD --docker-email=YOUR_EMAIL
kubectl create secret docker-registry quaysecret --docker-server=quay.io --docker-username=YOUR_USERNAME --docker-password=YOUR_PASSWORD --docker-email=YOUR_EMAIL
```

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

