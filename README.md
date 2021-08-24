# Kubernetes aka K8


![](https://github.com/khanmaster/Kubernetes_deployment/blob/main/k8-labels.png)

- Deploymentment with K8 

- Let's create `nginx-deployment.yml`

```
# K8 works with API versions to declare the resourcdes

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment # naming the deployment


spec:
  selector:
    matchLabels:
      app: nginx # look for this label to match with k8 service
  
  # Let's create 2 replica sets of this instances/pods
  replicas: 2 
  
  # template to use it's label for K8 service to launch in the browser
  template:
    metadata:
      labels:
        app: nginx
   
    # Let's define the container spec
    spec:
      containers:
      - name: nginx 
        image: ahskhan/eng89automatednginx:latest
        ports:
        - containerPort: 80
```
-`kubectl create -f nginx-deployment.yml`
- Let's create a service to expose our deployment globally

- create `nginx-service.yml`
```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: "2021-08-23T11:07:26Z"
  name: nginx-deployment
  namespace: default
  resourceVersion: "40883"
  uid: 9190ab75-d61c-4ff4-a3d1-0d293fa8d72e
spec:
  clusterIP: 10.103.15.174
  clusterIPs:
  - 10.103.15.174
  externalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - nodePort: 30442
    port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx
  sessionAffinity: None
  type: LoadBalancer
status:
  loadBalancer:
    ingress:
    - hostname: localhost
  ```

  - `kubectl create -f nginx-service.yml`
