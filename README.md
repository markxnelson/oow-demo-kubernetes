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

Obtain the external IP address (need to wait about a minute for it to start up):

```
kubectl describe service oow-load-balancer
```

Now you can access the web app and REST services using the external IP address, e.g.

http://1.2.3.4:7001/licenseplates/index.jsp

GET http://1.2.3.4:7001/licenseplates/rest/plates/list

POST http://1.2.3.4:7001/licenseplates/rest/plates/add
Header: Content-Type=application/json
Body:
{"address":"5 Long Road","imageURL":"http://i.imgur.com/b9KZ8Ql.jpg","owner":"Mark Nelson","plateNumber":"ABC-1453","state":"NJ"}

