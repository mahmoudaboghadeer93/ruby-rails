###############################################################
1) firstly build image for it:-
$ docker build -t sidekiq:latest --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g)  -f Dockerfile .

2) tag it with ECR registry ID , push it to ecr:-
$docker tag drkiq:latest ${ecrUrl}/sidekiq:latest
$docker push ${ecrUrl}/sidekiq:latest

3) deploy k8s deployment , services , configmap:-
$kubectl -n ${namespace} apply -f sidekiq-deploy.yaml

4) then use this image inside deployment:-
$ kubectl -n ${namespace} set image deployment/sidekiq sidekiq= ${ecrUrl}'/'sidekiq:latest

5) check it :-
$kubectl -n ${namespace} rollout status deployment/sidekiq
