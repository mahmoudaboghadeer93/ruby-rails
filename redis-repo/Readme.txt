###############################################################

3) deploy k8s components:-

$kubectl -n ${namespace} apply -f redis-storage.yaml
$kubectl -n ${namespace} apply -f redis-deploy.yaml
$kubectl -n ${namespace} apply -f redis-svc.yaml


