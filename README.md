# LSC – Lab 6 – Kubernetes 


## 1.	Creating the Kubernetes Cluster
```
minikube start --driver=docker
```

## 2.	Installing Helm 
```
choco install kubernetes-helm
helm version
```

## 3.	Installing NFS Server + Provisioner
```
helm repo add nfs-ganesha-server-and-external-provisioner https://kubernetes-sigs.github.io/nfs-ganesha-server-and-external-provisioner/
helm repo update
helm install nfs-server-provisioner nfs-ganesha-server-and-external-provisioner/nfs-server-provisioner -f nfs-values.yaml
```

## 4.	Creating configuration files
 
## 5.	Applying configuration files
```
kubectl apply -f pvc.yaml
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f upload.yaml
```
## 6.	Checking the application's status
```
kubectl get pvc
kubectl get pods 
kubectl get svc
```

## 7.	Displaying the number of pods in Kubernetes
```
kubectl get pods -l app=web
```

## 8.	Assigning the pod name to a variable
```
$podName = "nginx-deployment-85b868776c-c7fb9"
```

## 9.	Displaying the content of the index.html file
```
kubectl exec -it $podName -- cat /usr/share/nginx/html/index.html
```
```
<h1>Hello from NFS!</h1>
``` 

## 10.	Using Minikube to Access the Application
```
minikube service nginx-service –url
kubectl get svc
```
```
kubectl port-forward svc/nginx-service 7070:80
```

### Files included
- nfs-values.yaml – Configures the NFS server for storage and networking settings in Kubernetes.
- pvc.yaml – Defines a Persistent Volume Claim to request storage for the application.
- deployment.yaml – Specifies the configuration for deploying the NGINX server, including replicas and container image.
- service.yaml – Exposes the NGINX deployment to the outside world through a service.
- upload.yaml – Uploads HTML content to the mounted storage.
