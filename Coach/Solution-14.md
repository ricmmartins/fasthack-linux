# Desafio 14 - Executando Containers - Guia do Coach 

[< Solução Anterior](./Solution-13.md) - **[Início](./README.md)**

## Notas e Orientações
1. Instale o runtime do Docker

`student@vm01:~$ sudo apt install docker.io`

```bash
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  bridge-utils containerd pigz runc ubuntu-fan
Suggested packages:
  ifupdown aufs-tools cgroupfs-mount | cgroup-lite debootstrap docker-doc rinse zfs-fuse | zfsutils
The following NEW packages will be installed:
  bridge-utils containerd docker.io pigz runc ubuntu-fan
0 upgraded, 6 newly installed, 0 to remove and 24 not upgraded.
Need to get 69.2 MB of archives.
After this operation, 334 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://azure.archive.ubuntu.com/ubuntu focal/universe amd64 pigz amd64 2.4-1 [57.4 kB]
Get:2 http://azure.archive.ubuntu.com/ubuntu focal/main amd64 bridge-utils amd64 1.6-2ubuntu1 [30.5 kB]
Get:3 http://azure.archive.ubuntu.com/ubuntu focal-updates/main amd64 runc amd64 1.1.4-0ubuntu1~20.04.1 [4005 kB]
Get:4 http://azure.archive.ubuntu.com/ubuntu focal-updates/main amd64 containerd amd64 1.6.12-0ubuntu1~20.04.1 [35.3 MB]
Get:5 http://azure.archive.ubuntu.com/ubuntu focal-updates/universe amd64 docker.io amd64 20.10.21-0ubuntu1~20.04.2 [29.0 MB]
Get:6 http://azure.archive.ubuntu.com/ubuntu focal/main amd64 ubuntu-fan all 0.12.13 [34.5 kB]
Fetched 68.5 MB in 1s (66.1 MB/s)
Preconfiguring packages ...
Selecting previously unselected package pigz.
(Reading database ... 69260 files and directories currently installed.)
Preparing to unpack .../0-pigz_2.4-1_amd64.deb ...
Unpacking pigz (2.4-1) ...
Selecting previously unselected package bridge-utils.
Preparing to unpack .../1-bridge-utils_1.6-2ubuntu1_amd64.deb ...
Unpacking bridge-utils (1.6-2ubuntu1) ...
Selecting previously unselected package runc.
Preparing to unpack .../2-runc_1.1.4-0ubuntu1~20.04.1_amd64.deb ...
Unpacking runc (1.1.4-0ubuntu1~20.04.1) ...
Selecting previously unselected package containerd.
Preparing to unpack .../3-containerd_1.6.12-0ubuntu1~20.04.1_amd64.deb ...
Unpacking containerd (1.6.12-0ubuntu1~20.04.1) ...
Selecting previously unselected package docker.io.
Preparing to unpack .../4-docker.io_20.10.21-0ubuntu1~20.04.2_amd64.deb ...
Unpacking docker.io (20.10.21-0ubuntu1~20.04.2) ...
Selecting previously unselected package ubuntu-fan.
Preparing to unpack .../5-ubuntu-fan_0.12.13_all.deb ...
Unpacking ubuntu-fan (0.12.13) ...
Setting up runc (1.1.4-0ubuntu1~20.04.1) ...
Setting up bridge-utils (1.6-2ubuntu1) ...
Setting up pigz (2.4-1) ...
Setting up containerd (1.6.12-0ubuntu1~20.04.1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/containerd.service → /lib/systemd/system/containerd.service.
Setting up ubuntu-fan (0.12.13) ...
Created symlink /etc/systemd/system/multi-user.target.wants/ubuntu-fan.service → /lib/systemd/system/ubuntu-fan.service.
Setting up docker.io (20.10.21-0ubuntu1~20.04.2) ...
Adding group 'docker' (GID 118) ...
Done.
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /lib/systemd/system/docker.socket.
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.18) ...
```

2. Para executar o container Nginx, execute o seguinte comando:

`student@vm01:~$ sudo docker run -d --name mynginx -p 8090:80 nginx`

3. Teste se o container está executando corretamente:

`student@vm01:~$ curl -v http://localhost:8090`

```bash
*   Trying 127.0.0.1:8090...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8090 (#0)
> GET / HTTP/1.1
> Host: localhost:8090
> User-Agent: curl/7.68.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Server: nginx/1.23.2
< Date: Mon, 07 Nov 2022 23:06:14 GMT
< Content-Type: text/html
< Content-Length: 615
< Last-Modified: Wed, 19 Oct 2022 07:56:21 GMT
< Connection: keep-alive
< ETag: "634fada5-267"
< Accept-Ranges: bytes
<
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
* Connection #0 to host localhost left intact
```

No Network Security Group associado à sua máquina virtual, abra a porta 8090.

4. Para o desafio avançado, aqui estão os passos:

Crie o Dockerfile

No seu diretório home, crie um arquivo chamado Dockerfile com o seguinte conteúdo:

`student@vm01:~$ cat <<'EOT' > ~/Dockerfile`

```bash
FROM nginx
COPY default.conf /etc/nginx/conf.d/default.conf
COPY index.html /usr/share/nginx/html/index.html
```
`EOT`

Crie o arquivo de configuração do Nginx que será adicionado ao container:

`student@vm01:~$ cat <<'EOT' > ~/default.conf`

```bash
server {
    listen       80;
    listen  [::]:80;
    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
}
```
`EOT`

Crie o conteúdo que será exibido no Nginx:

`student@vm01:~$ cat <<'EOT' > ~/index.html`

```bash
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Sample Container App</title>
    <style>
        body {
            background-color: green;
        }

        h1 {
            color: red;
            font-size: 5em;
        }
    </style>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
```
`EOT`

Agora vamos construir a imagem:

`student@vm01:~$ sudo docker build -t my-custom-nginx .`

```bash
Sending build context to Docker daemon  14.26MB
Step 1/3 : FROM nginx
 ---> 88736fe82739
Step 2/3 : COPY default.conf /etc/nginx/conf.d/default.conf
 ---> 0299edfebe33
Step 3/3 : COPY index.html /usr/share/nginx/html/index.html
 ---> 327cfbad4093
Successfully built 327cfbad4093
Successfully tagged my-custom-nginx:latest
```

Vamos executar nosso container mapeando a porta 80 do container para a porta 8080 do host:

`student@vm01:~$ sudo docker run -d --name my-custom-nginx -p 8080:80 my-custom-nginx`

```bash
8f367dbe3c02f78e3c63aa1e4c63df4dec5c0e3bcf44a79d4c91c49af37e8fa3
```

Vamos testar:

`student@vm01:~$ curl -v http://localhost:8080`

```bash
*   Trying 127.0.0.1:8080...
* TCP_NODELAY set
* Connected to localhost (127.0.0.1) port 8080 (#0)
> GET / HTTP/1.1
> Host: localhost:8080
> User-Agent: curl/7.68.0
> Accept: */*
>
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Server: nginx/1.23.2
< Date: Mon, 07 Nov 2022 23:21:20 GMT
< Content-Type: text/html
< Content-Length: 285
< Last-Modified: Mon, 07 Nov 2022 23:18:40 GMT
< Connection: keep-alive
< ETag: "6369a190-11d"
< Accept-Ranges: bytes
<
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Sample Container App</title>
    <style>
        body {
            background-color: green;
        }

        h1 {
            color: red;
            font-size: 5em;
        }
    </style>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
* Connection #0 to host localhost left intact
```

Publique a imagem no Docker Hub:

Então vamos criar uma tag:

`student@vm01:~$ sudo docker tag my-custom-nginx rmmartins/my-custom-nginx`

Faça login na sua conta Docker:

`student@vm01:~$ sudo docker login`

Envie sua imagem para o Docker Hub:

`student@vm01:~$ sudo docker push rmmartins/my-custom-nginx`

```bash
Using default tag: latest
The push refers to repository [docker.io/rmmartins/my-custom-nginx]
ccebfb51bc22: Pushed
9e48ed2fc160: Pushed
4b8862fe7056: Mounted from library/nginx
8a70d251b653: Mounted from library/nginx
30b9f4f09bbc: Mounted from library/nginx
60048dd75064: Mounted from library/nginx
8192bee30e0d: Mounted from library/nginx
7eb91ab3a488: Mounted from library/nginx
latest: digest: sha256:2b18ff0ad9b8b73a86e41aaa74c02cbb2fd0be66189b0b96d3abf8b9bba3a2c3 size: 1985
```

E se você quiser conectar ao seu container em execução e verificar internamente:

`student@vm01:~$ sudo docker exec -it my-custom-nginx /bin/bash`

```bash
root@8f367dbe3c02:/# ls /usr/share/nginx/html/
50x.html  index.html
root@8f367dbe3c02:/# cat /usr/share/nginx/html/index.html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Sample Container App</title>
    <style>
        body {
            background-color: green;
        }

        h1 {
            color: red;
            font-size: 5em;
        }
    </style>
</head>
<body>
    <h1>Hello World</h1>
</body>
</html>
root@8f367dbe3c02:/# exit
```