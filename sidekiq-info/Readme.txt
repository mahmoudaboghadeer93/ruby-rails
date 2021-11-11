docker build -t sidekiq --build-arg USER_ID=$(id -u) --build-arg GROUP_ID=$(id -g)  -f Dockerfile .
