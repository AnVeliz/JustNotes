Modify HOSTS file to have static addresses for the services we are going to use:

127.0.0.1 gitea
127.0.0.1 drone


Create docker network:
docker network create gitea-net




GITEA

set login and password for both gitea server and postgresql in 001-docker-compose-gitea.yml
go to localhost:3000 and set user name and password there plus email
click set up button


docker-compose.exe -f 001-docker-compose-gitea.yml up -d





DRONE
go to settings in gitea and create OAuth application

name: drone
redirect URL: http://drone:3001/login



get OAuth secret and set them to docker-compose-drone.yml:

client id: fd2ebbfe-f30a-4a9c-a5e4-5a9af3e078a9
client secret: YNtkT0tw9aMm9C7mkQBLCkLVduK4tjhpOjzSPe67BlkM

generate secret for runners connecting using e.g.: openssl rand -hex 16
secret: bea26a2221fd8090ea38720fc445eca6
set the secret to docker-compose-drone.yml


docker-compose.exe -f 002-docker-compose-drone-server.yml up -d



DRONE_AGENT
set drone server host, protocol and secret key in 003-docker-compose-drone-agent.yml

docker-compose.exe -f 003-docker-compose-drone-agent.yml up -d
