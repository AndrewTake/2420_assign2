# 2420 assign 2

# ip: http://137.184.246.254 <br />

## DO NOT USE SAFARI. 
I had issues with the safari browser. Chrome and Firefox work best. 
<br />
<br />

# Step 1

<br />
<br />
Create a VPC in San fransico data center. <br />
Create a load balancer in the SF datacentre of your VPC. <br />
Add the droplets to your load balancer. <br />
Create a firewall allowing SSH, and HTTP on port 80 for your load balancer. <br />

<img width="1173" alt="Screenshot 2022-12-02 at 11 03 02 PM" src="https://user-images.githubusercontent.com/88999663/205429252-5c7b51b6-e21e-4a39-83a0-c4f435773e32.png">


<img width="1209" alt="Screenshot 2022-12-02 at 10 59 56 PM" src="https://user-images.githubusercontent.com/88999663/205429127-09bd3afa-d151-4867-9fa2-df818a0604c1.png">
<br />
<br />

# Step 2

<br />
<br />
add a new user <br />
useradd -ms /bin/bash andrew <br />
usermod -aG sudo andrew <br />
rsync --archive --chown=andrew:andrew ~/.ssh /home/andrew <br />

<img width="418" alt="Screenshot 2022-12-02 at 10 06 10 PM" src="https://user-images.githubusercontent.com/88999663/205429306-0ea91f4f-442a-44ee-a64b-548f7ac89817.png">
<br />
<br />

# Step 3

<br />
<br />

## Install a web server on both droplets

Download caddy:

tar xvf https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_linux_amd64.tar.gz. <br />
Change caddys owner to root sudo chown root: caddy. <br />
Move caddy to bin directory cp caddy /usr/bin. <br />

<img width="1439" alt="Screenshot 2022-12-02 at 10 53 53 PM" src="https://user-images.githubusercontent.com/88999663/205429567-aca1b94c-3d2d-4c66-8615-e2d86f79c9e8.png">
<br />
<br />

# Step 4

<br />
<br />

## make directories

<img width="348" alt="Screenshot 2022-12-02 at 11 22 07 PM" src="https://user-images.githubusercontent.com/88999663/205429865-005da749-4ffd-408f-af76-55a2dde92382.png">

## make index.html

<img width="703" alt="Screenshot 2022-12-02 at 11 14 01 PM" src="https://user-images.githubusercontent.com/88999663/205429607-5fba6c68-f5a7-4cd7-b786-af99532bce28.png">

## make index.js

<img width="618" alt="Screenshot 2022-12-02 at 11 15 04 PM" src="https://user-images.githubusercontent.com/88999663/205429634-d83ac28d-22ad-4b45-af82-2dcaf741a78e.png">

npm init
npm i fastify

Go to /var/www and put your index.html file in there <br />
make sure that hello_world.service is in /etc/systemd/system <br />
make sure that caddy.service is in /etc/systemd/system <br />
make sure that Caddyfile is in /etc/caddy/Caddyfile <br />
use systemctl daemon-reload to restart server <br />
systemctl restart caddy.service <br />
inside of /opt/node put your src/index.js files. make sure to install node <br />

<br />
<br />

# Step 5 

<br />
<br />

## Create Caddyfile and the caddy.service

<br />
<br />
vim /etc/caddy/Caddyfile

<img width="425" alt="Screenshot 2022-12-02 at 11 17 18 PM" src="https://user-images.githubusercontent.com/88999663/205429695-be8aa49d-beeb-4b32-a571-811d612c9213.png">

vim /etc/systemd/system/caddy.service

<img width="704" alt="Screenshot 2022-12-02 at 11 18 52 PM" src="https://user-images.githubusercontent.com/88999663/205429741-2ce06583-b3c1-4ee2-9b0a-f75eaf47e9cd.png">
<br />
<br />

# Step 6

<br />
<br />

## Download node with volta

curl https://get.volta.sh | bash <br />
source ~/.bashrc <br />
volta install node <br />
This will install node on your droplet or wsl and we can then create a new node project in the src directory <br />

<img width="804" alt="Screenshot 2022-12-02 at 11 23 51 PM" src="https://user-images.githubusercontent.com/88999663/205429922-0cb31fd3-3102-40fa-8678-3497f10747a1.png">

<br />
<br />

# Step 7

<br />
<br />

## write a service file to restart on failure

<img width="1007" alt="Screenshot 2022-12-02 at 11 28 59 PM" src="https://user-images.githubusercontent.com/88999663/205430086-ce02e6ef-2f60-4a5c-a75f-d8b32f07f912.png">
<br />
<br />

# Step 8

<br />
<br />

## Test and run server

RUN THE CODE BELOW TO START SERVER <br />

Write the code into both droplets. <br />

`systemctl enable caddy.service
systemctl start caddy.service
systemctl status caddy.service

systemctl enable network.service
systemctl start network.service
systemctl status network.service`
<br />
<br />

# Step 9

<br />
<br />

## Testing that the deployment works

<img width="1042" alt="Screenshot 2022-12-03 at 1 41 03 AM" src="https://user-images.githubusercontent.com/88999663/205434502-58335fa0-e37f-4a10-bdb9-323aefd6899e.png">

Go to the ip of the loadbalancer. <br />
Check to see if your html message is visible. <br />
Visit both droplets and check to make sure that both messages work. <br />
Visit ip/api and check to see that both droplets are active.

