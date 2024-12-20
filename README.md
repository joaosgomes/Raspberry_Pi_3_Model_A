# Raspberry Pi 3 Model A+ 1.4Ghz 512Mb com WiFi 2.4/5GHz + Bluetooth 4.2 - Raspberry Pi



![https://www.raspberrypi.com](https://www.raspberrypi.com/app/uploads/2022/02/COLOUR-Raspberry-Pi-Symbol-Registered.png)


<iframe title="tarefa2" width="1024" height="1060" src="https://app.powerbi.com/view?r=eyJrIjoiMzdmMjdhNDgtMWI3Yi00NzkyLTk3NGMtZjFiZWM1ZTI5NTAzIiwidCI6ImFkMjhjNjI1LWYyY2EtNGU5MS1iNmQ2LTE4OTIyYmM5MzkxYyIsImMiOjh9" frameborder="0" allowFullScreen="true"></iframe>

## Setup

## SSH: ssh <pi@raspberrypi.local> pi@raspberrypi

## xrdp + Windows Remote Desktop Connection

````console
Install https://github.com/stascorp/rdpwrap (Windows Home Only)

sudo apt install xrdp
````


## Find Ip Address

````console

ipconfig

nmap -sn 192.168.1.0/24

nmap  192.168.1.0/24



# Find ip of MAC Address B8:27:EB:CE:A0:C0 (Raspberry Pi Foundation))  

arp -a | findstr b8-27-eb

# ping mdns raspberrypi.local
ping raspberrypi

ping raspberrypi -4
````



## Docker + Portainer


### Docker 
![](https://www.docker.com/wp-content/uploads/2023/08/logo-guide-logos-1.svg)



````console
sudo apt update
sudo apt-get upgrade
sudo reboot

curl -ssl <https://get.docker.com> | sh
sudo usermode -aG docker pi
docker service ls
docker ps
sudo reboot

````

### Portainer

![](https://www.portainer.io/hubfs/portainer-logo-black.svg)

````console
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

![](https://www.rabbitmq.com/img/logo-rabbitmq.svg)

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


---

## Configure Cloudflared Tunnel

![](https://cf-assets.www.cloudflare.com/slt3lc6tev37/1wf4qdGsPqa2UUSEoa4Yyg/3250a65f210bbb7062ab4dd9a9bdf213/logo-cloudflare-dark.svg)

````console
ssh pi@raspberrypi.local


# Fetch the file
wget https://github.com/cloudflare/cloudflared/releases/download/2023.8.2/cloudflared-linux-armhf

# Move it to our bin directory so we can just call it
sudo mv cloudflared-linux-armhf /usr/local/bin/cloudflared

# Go To
cd /usr/local/bin

# Make it executable
sudo chmod +x cloudflared

# Now head to Cloudflare Zero Trust Dashboard -> Access -> Tunnels and create a tunnel

sudo cloudflared service install xxxxxx

# Create a .ssh Directory id not Exist
mkdir ~/.ssh

nano config

# Add the following to the config:

Host raspberrypi-ssh.joaosilvagomes.com
ProxyCommand /usr/local/bin/cloudflared access ssh --hostname %h

# ssh


# Browser rendering

# Check https://developers.cloudflare.com/cloudflare-one/applications/non-http/#rendering-in-the-browser

pi@raspberrypi:~/.ssh $ ssh pi@raspberrypi-ssh.joaosilvagomes.com
A browser window should have opened at the following URL:

If the browser failed to open, please visit the URL above directly in your browser.


pi@raspberrypi:/ $ cd home/pi/.cloudflared/


sudo systemctl enable cloudflared

sudo systemctl start cloudflared


````


| Public hostname                                    | Path | Service                |
| -------------------------------------------------- | ---- | ---------------------: |
| https://raspberrypi-portainer.joaosilvagomes.com   | *    | http://localhost:9000  |
| https://raspberrypi-rabbitmq.joaosilvagomes.com    | *    | http://localhost:15672 |
| https://raspberrypi-ssh.joaosilvagomes.com         | *    | ssh://localhost:22     |
| ws://raspberrypi-mqtt.joaosilvagomes.com/ws        | *    | http://localhost:15675 |
| https://raspberrypi-magicmirror.joaosilvagomes.com | *    | http://localhost:8080  |

*Tested MQTT via https://github.com/joaosgomes/mqtt_amqp_rabbitmq using ws Protocol*

<https://www.rabbitmq.com/web-mqtt.html>

<https://community.cloudflare.com/t/mqtt-trough-cloudflare-tunnel/503599/10>

# References:

https://hongchai.medium.com/setting-up-cloudflared-on-a-raspberry-pi-3b-c40a667ac022

https://pimylifeup.com/raspberry-pi-cloudflare-tunnel/

https://blog.cloudflare.com/ssh-raspberry-pi-400-cloudflare-tunnel-auditable-terminal/

https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/use-cases/ssh/#1-connect-the-server-to-cloudflare-1

https://developers.cloudflare.com/cloudflare-one/applications/non-http/#rendering-in-the-browser

https://www.rabbitmq.com/web-mqtt.html

https://community.cloudflare.com/t/mqtt-trough-cloudflare-tunnel/503599/10
