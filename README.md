# Raspberry Pi 3 Model A+ 1.4Ghz 512Mb com WiFi 2.4/5GHz + Bluetooth 4.2 - Raspberry Pi

## Setup

## SSH: ssh <pi@raspberrypi.local> pi@raspberrypi

## Docker + Portainer

````console
sudo apt update
sudo apt-get upgrade
sudo reboot

curl -ssl <https://get.docker.com> | sh
sudo usermode -aG docker pi
docker service ls
docker ps
sudo reboot

sudo docker pull portainer/portainer-ce:latest
docker image ls

sudo docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.socket:/var/run/docker.socket -v portainer_data:/data portainer/portainer-ce:latest

````

### Access

<http://raspberrypi:9000/>

### Resume

Setup SSH on RaspberryPi:
Code to install docker: curl -ssl <https://get.docker.com> | sh
code to install Portainer : sudo docker run -d -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:linux-arm

## RabbitMQ

````console
 docker run -it --name rabbitmq -p 5672:5672 -p 15672:15672 -p 1883:1883 -p 15675:15675 rabbitmq:3
 ````

Assign name and allocate pseudo-TTY (--name, -it)

Access:

<http://raspberrypi.local:15672/>

User: guest
Password: guest

amqp :: 5672
clustering :: 25672
http :: 15672
http/prometheus :: 15692
http/web-mqtt :: 15675
mqtt :: 1883

### SSH into a Container

Use docker ps to get the name of the existing container.
Use the command docker exec -it 'container name' /bin/bash to get a bash shell in the container.
exit

## Enable rabbitmq_mqtt

 Eg.:

 ````console

docker exec -it 38c2f3acbaef /bin/bash

rabbitmq-plugins list

rabbitmq-plugins enable rabbitmq_management

rabbitmq-plugins enable rabbitmq_management

rabbitmq-plugins enable rabbitmq_top

rabbitmq-plugins enable rabbitmq_mqtt

docker run -it --name rabbitmq -p 5672:5672 -p 15672:15672 -p 1883:1883 -p 15675:15675 rabbitmq:3
````

## Commads

````console
 hostname -I

````

## GitHub

````console
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/joaosgomes/Raspberry_Pi_3_Model_A.git
git push -u origin main
````

## References

(How to install Docker (and Portainer) on a RaspberryPi)
<https://www.youtube.com/watch?v=O7G3oatg5DA>

(Running RabbitMQ Locally with Docker)
<https://www.youtube.com/watch?v=-0g-1ckQgBo>
