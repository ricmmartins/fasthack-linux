# Challenge 12 - Setting up a WebServer - Coach's Guide 

[< Previous Solution](./Solution-11.md) - **[Home](./README.md)** - [Next Solution >](./Solution-13.md)

## Notes & Guidance
1. Download the sample application [from here](../Student/resources/simple-php-app.tar.gz?raw=true) to your home directory

`student@vm01:~$ cd ~ ;  wget https://raw.githubusercontent.com/ricmmartins/fasthack-linux/main/Student/resources/simple-php-app.tar.gz -O simple-php-app.tar.gz`

2. Extract the content of simple-php-app.tar.gz on your home directory

`student@vm01:~$ tar xzvf simple-php-app.tar.gz`

```bash
simple-php-app/
simple-php-app/README.md
simple-php-app/assets/
simple-php-app/assets/css/
simple-php-app/assets/css/bootstrap-responsive.min.css
simple-php-app/assets/css/bootstrap.min.css
simple-php-app/assets/js/
simple-php-app/assets/js/bootstrap.min.js
simple-php-app/index.php
```

3. Install nginx

`student@vm01:~$ sudo apt install nginx-core`

```bash
Reading package lists... Done
Building dependency tree
Reading state information... Done
Suggested packages:
  nginx-doc
The following NEW packages will be installed:
  nginx-core
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 425 kB of archives.
After this operation, 1250 kB of additional disk space will be used.
Get:1 http://azure.archive.ubuntu.com/ubuntu focal-updates/main amd64 nginx-core amd64 1.18.0-0ubuntu1.2 [425 kB]
Fetched 425 kB in 0s (11.0 MB/s)
Selecting previously unselected package nginx-core.
(Reading database ... 68923 files and directories currently installed.)
Preparing to unpack .../nginx-core_1.18.0-0ubuntu1.2_amd64.deb ...
Unpacking nginx-core (1.18.0-0ubuntu1.2) ...
Setting up nginx-core (1.18.0-0ubuntu1.2) ...
Processing triggers for man-db (2.9.1-1) ...
```

4. Install php-fpm

`student@vm01:~$ sudo apt install php-fpm`

```bash
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  php-common php8.3-cli php8.3-common php8.3-fpm php8.3-opcache php8.3-readline
Suggested packages:
  php-pear
The following NEW packages will be installed:
  php-common php-fpm php8.3-cli php8.3-common php8.3-fpm php8.3-opcache php8.3-readline
0 upgraded, 7 newly installed, 0 to remove and 0 not upgraded.
Need to get 4870 kB of archives.
After this operation, 21.2 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
```

5. Configure Nginx

`student@vm01:~$ cat <<'EOT' > ~/default`
```bash
# Nginx Config
server {
        listen 80;
        root /home/student/simple-php-app;
        index index.php index.html index.htm;
        server_name _;
 
        location / {
            try_files $uri $uri/ =404;
        }
 
        location ~ \.php$ {
            include snippets/fastcgi-php.conf;
            fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
        }
}
``` 
`EOT`

`student@vm01:~$ sudo cp ~/default /etc/nginx/sites-enabled/default`

`student@vm01:~$ sudo systemctl restart php8.3-fpm`

`student@vm01:~$ sudo systemctl restart nginx`

Remember to open port 80 in your firewall or cloud security group

### Advanced challenge

To add SSL we will use [Certbot](https://certbot.eff.org/) to get a certificate from [Let's Encrypt](https://letsencrypt.org/). Here are the steps you need to follow:

* Ensure you have a valid domain with an A record pointing to the server's public IP. A valid domain with an A record defined is a prerequisite for Certbot. If using Azure, you can use Azure App Service Domains to get a domain.  
    
* After addressing the previous step, you must adjust your Nginx config file `/etc/nginx/sites-enabled/default` setting the **server_name** directive to point to the name of your domain. Eg:
    
`student@vm01:~$ sudo sed -i.bkp -e 's/_;/linuxhackathon.com;/g' /etc/nginx/sites-enabled/default`

Then let's proceed to the setup and configurations for Certbot by setting new environment variables: 

```
export DOMAIN_NAME="linuxhackathon.com"
export EMAIL="admin@linuxhackathon.com"
````
_Remember to change according to your domain_

Install snap tool to get certbot:

`student@vm01:~$ sudo snap install core; sudo snap refresh core`

Install and configure Certbot:

`student@vm01:~$ sudo snap install --classic certbot` 

`student@vm01:~$ sudo certbot --nginx -d "${DOMAIN_NAME}" -m "${EMAIL}" --agree-tos -n` 

Restart Nginx:

`student@vm01:~$ sudo systemctl restart nginx` 

Remember to open the port 443 in your firewall or cloud security group
