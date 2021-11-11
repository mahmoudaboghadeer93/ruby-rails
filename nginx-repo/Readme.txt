###############################################################
1) firstly build image for it:-
$docker build -t nginx:latest   -f Dockerfile-nginx .

2) tag it with ECR registry ID , push it to ecr:-
$docker tag nginx-dkriq:latest ${ecrUrl}/nginx:latest
$docker push ${ecrUrl}/nginx:latest

3) deploy k8s deployment , services , configmap:-
$kubectl -n ${namespace} apply -f nginx-deploy.yaml
$kubectl -n ${namespace} apply -f nginx-svc.yaml

4) then use this image inside deployment:-
$ kubectl -n ${namespace} set image deployment/nginx nginx= ${ecrUrl}'/'nginx:latest

5) check it :-
$kubectl -n ${namespace} rollout status deployment/nginx
