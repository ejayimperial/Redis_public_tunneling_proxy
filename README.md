# Installation

````
sudo apt-get update &&   sudo apt-get upgrade
sudo apt install awscli && 
sudo apt install redis-tools && 
 sudo apt install nginx -y  && 
sudo apt install net-tools

 sudo apt install stunnel
 cd /etc/stunnel/
touch /etc/stunnel/redis-cli.conf
sudo  nano /etc/stunnel/redis-cli.conf
````  

<b>Touch Nano redis-cli.conf</b>
````  
fips = no
setuid = root
setgid = root
pid = /var/run/stunnel.pid
debug = 7 
delay = yes
options = NO_SSLv2
options = NO_SSLv3
[redis-cli]
   client = yes
   accept = 127.0.0.1:6379
   connect = encrypt.**********.amazonaws.com:6379
[redis-cli-replica]
   client = yes
   accept = 127.0.0.1:6380
   connect = encrypt..**********.amazonaws.com:6379
````  
````  
sudo stunnel /etc/stunnel/redis-cli.conf
sudo netstat -tulnp | grep -i stunnel

sudo nano /etc/nginx/nginx.conf
````  

<b>Nano nginx.conf</b>
````  
stream {
    server {
        listen 6379;
        proxy_pass 127.0.0.1:6379;
    }
    server {
        listen 6380;
        proxy_pass 127.0.0.1:6380;
    }
}

sudo systemctl restart nginx #systemd
````
