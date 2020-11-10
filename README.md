# Kubernetes Pod Security Policies

## Minikube setup
`minikube start --extra-config=apiserver.enable-admission-plugins=PodSecurityPolicy --addons=pod-security-policy`




## Test policy
```
kubectl apply -f psp.yml
kubectl create serviceaccount fakeuser
kubectl create rolebinding fakeeditor --clusterrole=edit --serviceaccount=default:fakeuser
kubectl --as=system:serviceaccount:default:fakeuser apply -f test-deploy.yml
kubectl describe pods pause
```
