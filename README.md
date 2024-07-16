For this project us must have a Kubernetes cluster.  

Please note towards the end of the project you have deployed serveral services that can only be accessed via localhost's IP. We will be changing the services to have thier ports forward to the cluster IP for access. 

- I had a Rocky Linux headless cluseter that caused some confussion on that step. 

# Install Helm for your OS  

## Grab the   
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts  
helm repo update  

helm install <nameOfYourChoice> prometheus-community/kube-prometheus-stack  


Now check that pods and services are up and running  

kubectl get pod - to show the pods in this Namespace  

## Gathering the services names for port-forwarding  
kubectl get services  
### This will show more details like the Nodeports  
kubectl get services -n default  

## To test port-forwarding if you are on a host with a GUI  
kubectl port-forward service/prometheus-stack-grafana 3000:80  

## To create a Namespace and install the stack  
helm install prometheus-stack prometheus-community/kube-prometheus-stack --namespace=monitoring --create-namespace -f values.yml  