###############################################################

3) deploy k8s deployment , services , configmap:-

$kubectl -n ${namespace} apply -f postgres-storage.yaml
$kubectl -n ${namespace} apply -f postgres-configmap.yaml
$kubectl -n ${namespace} apply -f postgres-deploy.yaml
$kubectl -n ${namespace} apply -f postgres-svc.yaml


