# k8s-redis-cluster

# Create namespace
kubectl create ns redis
kubectl get ns

# Create Storage Class
kubectl apply -f StorageClass.yaml

# Create config map
kubectl apply -n redis -f ConfigMap.yaml
kubectl get configmap -n redis

# Create redis statefull
kubectl apply -n redis -f redis-statefull.yaml
kubectl get pods -n redis

# Create redis service
kubectl apply -n redis -f redis-service.yaml
kubectl get service -n redis

# Check replicate
kubectl -n redis logs redis-0
kubectl -n redis describe pod redis-0

kubectl -n redis exec -it redis-0 -- sh
redis-cli 
auth password
info replication


kubectl -n redis exec -it redis-1 -- sh
redis-cli 
auth password
info replication

# Test replicate
kubectl -n redis exec -it redis-0 -- sh
redis-cli 
auth password

SET emp1 jom
SET emp2 wongnai
SET emp3 lineman

KEYS *
1) "emp3"
2) "emp2"
3) "emp1"

kubectl -n redis exec -it redis-1 -- sh
redis-cli
auth password