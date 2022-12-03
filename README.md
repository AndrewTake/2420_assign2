#2420 assign 2

#Step 1

Create a VPC in San fransico data center.
Create a load balancer in the SF datacentre of your VPC.
Add the droplets to your load balancer.
Create a firewall allowing SSH, and HTTP on port 80 for your load balancer.

<img width="1173" alt="Screenshot 2022-12-02 at 11 03 02 PM" src="https://user-images.githubusercontent.com/88999663/205429252-5c7b51b6-e21e-4a39-83a0-c4f435773e32.png">


<img width="1209" alt="Screenshot 2022-12-02 at 10 59 56 PM" src="https://user-images.githubusercontent.com/88999663/205429127-09bd3afa-d151-4867-9fa2-df818a0604c1.png">

#Step 2

add a new user
useradd -ms /bin/bash andrew
usermod -aG sudo andrew
rsync --archive --chown=andrew:andrew ~/.ssh /home/andrew

<img width="418" alt="Screenshot 2022-12-02 at 10 06 10 PM" src="https://user-images.githubusercontent.com/88999663/205429306-0ea91f4f-442a-44ee-a64b-548f7ac89817.png">

#Step 3

Install a web server on both droplets

Download caddy:
tar xvf https://github.com/caddyserver/caddy/releases/download/v2.6.2/caddy_2.6.2_linux_amd64.tar.gz.
Change caddys owner to root sudo chown root: caddy.
Move caddy to bin directory cp caddy /usr/bin.

<img width="1439" alt="Screenshot 2022-12-02 at 10 53 53 PM" src="https://user-images.githubusercontent.com/88999663/205429567-aca1b94c-3d2d-4c66-8615-e2d86f79c9e8.png">


#Step 4

make directories
<img width="348" alt="Screenshot 2022-12-02 at 11 22 07 PM" src="https://user-images.githubusercontent.com/88999663/205429865-005da749-4ffd-408f-af76-55a2dde92382.png">

make index.html
<img width="703" alt="Screenshot 2022-12-02 at 11 14 01 PM" src="https://user-images.githubusercontent.com/88999663/205429607-5fba6c68-f5a7-4cd7-b786-af99532bce28.png">

make index.js
<img width="618" alt="Screenshot 2022-12-02 at 11 15 04 PM" src="https://user-images.githubusercontent.com/88999663/205429634-d83ac28d-22ad-4b45-af82-2dcaf741a78e.png">

npm init
npm i fastify


#Step 5 Create Caddyfile and the caddy.service

vim /etc/caddy/Caddyfile

<img width="425" alt="Screenshot 2022-12-02 at 11 17 18 PM" src="https://user-images.githubusercontent.com/88999663/205429695-be8aa49d-beeb-4b32-a571-811d612c9213.png">

vim /etc/systemd/system/caddy.service

<img width="704" alt="Screenshot 2022-12-02 at 11 18 52 PM" src="https://user-images.githubusercontent.com/88999663/205429741-2ce06583-b3c1-4ee2-9b0a-f75eaf47e9cd.png">


#Step 6


Download node with volta

curl https://get.volta.sh | bash
source ~/.bashrc
volta install node
This will install node on your droplet or wsl and we can then create a new node project in the src directory

<img width="804" alt="Screenshot 2022-12-02 at 11 23 51 PM" src="https://user-images.githubusercontent.com/88999663/205429922-0cb31fd3-3102-40fa-8678-3497f10747a1.png">



#Step 7

write a service file to restart on failure
<img width="1007" alt="Screenshot 2022-12-02 at 11 28 59 PM" src="https://user-images.githubusercontent.com/88999663/205430086-ce02e6ef-2f60-4a5c-a75f-d8b32f07f912.png">


#Step 8

Test and run server

<img width="844" alt="Screenshot 2022-12-02 at 11 28 25 PM" src="https://user-images.githubusercontent.com/88999663/205430072-d5c70c64-64df-419b-9416-75c1e4aa5db7.png">

#Step 9

I had step 9 working, then broke it by copying code from online https://gist.github.com/jniltinho/9bd76fd13cf3fc4dd60f1a9eec509492#file-laravel-app-conf
used this guys repo and broke everything. :(
