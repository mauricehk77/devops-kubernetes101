# devops-kubernetes101

Kubernetes 

{intro} 

https://pek3b.qingstor.com/kubesphere-docs/png/20200328170549.png
![alt text](https://pek3b.qingstor.com/kubesphere-docs/png/20200328170549.png)


Installation on Mac 

Basics 

How to create a namespace? 

{namespace} 

# kubectl get namespace -A 
# kubectl apply -f namespace.yaml

/*delete namesapce*/
# kubectl delete -f namespace.yaml

How to deploy an application? 
# kubectl apply -f deployment.yaml 

# kubectl get deployments -n development

# kubectl get pod -n development 

/*delete pod **/
# kubectl delete pod {pod-ID} -n development

How to check health of a pod?

check event log 
# kubectl describe pod {pod-ID} -n development

deploy BusyBox 
(deploy with default namespace)
# kubectl apply -f deployment_w_busybox.yaml 
# kubectl get pods 
# kubectl get pods -n development -o wide


/*login BusyBox pod bash*/
# kubectl exec -it {busybox-ID} -- /bin/sh
# wget 10.244.0.3:3000

DEMO - deploy "quote app"
1. create a quote.yaml
2. # kubectl apply -f quote.yaml
3. test with busybox 


DEMO - load balancer service
1. create a service.yaml
2. create a deployment.yaml
3. # minikube tunnel (*** remeber to enter password)
4. # kubectl apply -f service.yaml
5. # kubectl apply -f deployment.yaml
6. # kubectl get service -n development  --check IP
7. get to broswer and visit http://127.0.0.1

DEMO - security
(prevent 1.DDoS attack, 2.steal data , 3.mining crypto)
(solution: run as nonRoot; readonly Root file system; scan IoC file with snyk CLI https://docs.snyk.io/getting-started)

1. install snyk and setup account
2. create security.yaml
3. # snyk iac test security.yaml 
4. modify runAsNonRoot: true
5. modify readOnlyRootFilesystem: true
