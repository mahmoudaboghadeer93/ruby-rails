
###############################################################
1) firstly build image for it:-
$ cd drkiq/
$ docker build -t drkiq:latest --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g)  -f Dockerfile.rails .

2) tag it with ECR registry ID , push it to ecr:-
$docker tag drkiq:latest ${ecrUrl}/drkiq:latest
$docker push ${ecrUrl}/drkiq:latest

3) deploy k8s deployment , services , configmap:-
$kubectl -n ${namespace} apply -f drkiq-cofigmap.yaml
$kubectl -n ${namespace} apply -f drkiq-deploy.yaml
$kubectl -n ${namespace} apply -f drkiq-svc.yaml

4) then use this image inside deployment:-
$ kubectl -n ${namespace} set image deployment/drkiq drkiq= ${ecrUrl}'/'drkiq:latest

5) check it :-
$kubectl -n ${namespace} rollout status deployment/drkiq

6) then exec inside pod (kubectl -n ${namespace} exec -it ${pod_name} bash) , run these commands :-
$bundle exec rake db:reset
$bundle exec rake db:migrate
