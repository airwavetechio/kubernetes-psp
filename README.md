# Kubernetes Pod Security Policies

## Minikube setup
```
minikube start --extra-config=apiserver.enable-admission-plugins=PodSecurityPolicy --addons=pod-security-policy
```



## Testing a policy
* First, you need to remove the default restricted role binding. This will give you a clear idea of how things work. 
```
kubectl  delete clusterrolebinding default:restricted
```
* Next, apply our example pod security policy
```
kubectl apply -f example-psp.yml
```
* Create a fake user
```
kubectl create serviceaccount fakeuser
```
* Create a cluter role and bind it to the fakeuser
```
kubectl apply -f role.yml
```
* Test the deploy (it should fail and give an explanation of why)
```
kubectl --as=system:serviceaccount:default:fakeuser apply -f test-deploy.yml
```

