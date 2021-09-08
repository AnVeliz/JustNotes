### Modify HOSTS file to have static addresses for the services we are going to use (or change DNS records on domain level)</br>
127.0.0.1 gitea</br>
127.0.0.1 drone</br>

### Create docker network</br>
docker network create gitea-net</br>

### Set up and configure Gitea</br>
-> docker-compose.exe -f 001-docker-compose-gitea.yml up -d</br>
Navigate to Gitea page in your browser and set login + password + email</br>
Click set up button</br>

### Set up Drone</br>
Go to settings in gitea and create OAuth application</br>

name: drone</br>
redirect URL: http://drone/login</br>

You will get OAuth secrets which you should set to docker-compose-drone.yml e.g.:</br>

client id: fd2ebbfe-f30a-4a9c-a5e4-5a9af3e078a9</br>
client secret: YNtkT0tw9aMm9C7mkQBLCkLVduK4tjhpOjzSPe67BlkM</br>

Then you need to generate a secret for runners which should be connected to your Drone server:</br>
-> openssl rand -hex 16</br>

You will get e.g.:</br>
secret: bea26a2221fd8090ea38720fc445eca6</br>

Set the secret to docker-compose-drone.yml</br>

Run the container:</br>
docker-compose.exe -f 002-docker-compose-drone-server.yml up -d</br>

### Set up a Drone agent
Set drone server host, protocol and secret key in 003-docker-compose-drone-agent.yml

Run the container
docker-compose.exe -f 003-docker-compose-drone-agent.yml up -d
