# Desafio 13 - Protegendo um Servidor - Guia do Coach 
[< Solução Anterior](./Solution-12.md) - **[Início](./README.md)** - [Próxima Solução >](./Solution-14.md)

## Notas e Orientações
1. Certifique-se de que as listas de distribuição estão atualizadas 

`student@vm01:~$ sudo apt update`

```bash
Hit:1 http://azure.archive.ubuntu.com/ubuntu focal InRelease
Get:2 http://azure.archive.ubuntu.com/ubuntu focal-updates InRelease [114 kB]
Get:3 http://azure.archive.ubuntu.com/ubuntu focal-backports InRelease [108 kB]
Get:4 http://azure.archive.ubuntu.com/ubuntu focal-security InRelease [114 kB]
Get:5 http://azure.archive.ubuntu.com/ubuntu focal/universe amd64 Packages [8628 kB]
Get:6 http://azure.archive.ubuntu.com/ubuntu focal/universe Translation-en [5124 kB]
Get:7 http://azure.archive.ubuntu.com/ubuntu focal/universe amd64 c-n-f Metadata [265 kB]
Get:8 http://azure.archive.ubuntu.com/ubuntu focal/multiverse amd64 Packages [144 kB]
Get:9 http://azure.archive.ubuntu.com/ubuntu focal/multiverse Translation-en [104 kB]
Get:10 http://azure.archive.ubuntu.com/ubuntu focal/multiverse amd64 c-n-f Metadata [9136 B]
Get:11 http://azure.archive.ubuntu.com/ubuntu focal-updates/main amd64 Packages [2197 kB]
Get:12 http://azure.archive.ubuntu.com/ubuntu focal-updates/main Translation-en [385 kB]
Get:13 http://azure.archive.ubuntu.com/ubuntu focal-updates/main amd64 c-n-f Metadata [16.0 kB]
Get:14 http://azure.archive.ubuntu.com/ubuntu focal-updates/restricted amd64 Packages [1381 kB]
Get:15 http://azure.archive.ubuntu.com/ubuntu focal-updates/restricted Translation-en [196 kB]
Get:16 http://azure.archive.ubuntu.com/ubuntu focal-updates/restricted amd64 c-n-f Metadata [600 B]
Get:17 http://azure.archive.ubuntu.com/ubuntu focal-updates/universe amd64 Packages [973 kB]
Get:18 http://azure.archive.ubuntu.com/ubuntu focal-updates/universe Translation-en [222 kB]
Get:19 http://azure.archive.ubuntu.com/ubuntu focal-updates/universe amd64 c-n-f Metadata [21.8 kB]
Get:20 http://azure.archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 Packages [29.9 kB]
Get:21 http://azure.archive.ubuntu.com/ubuntu focal-updates/multiverse Translation-en [7940 B]
Get:22 http://azure.archive.ubuntu.com/ubuntu focal-updates/multiverse amd64 c-n-f Metadata [664 B]
Get:23 http://azure.archive.ubuntu.com/ubuntu focal-backports/main amd64 Packages [45.7 kB]
Get:24 http://azure.archive.ubuntu.com/ubuntu focal-backports/main Translation-en [16.3 kB]
Get:25 http://azure.archive.ubuntu.com/ubuntu focal-backports/main amd64 c-n-f Metadata [1420 B]
Get:26 http://azure.archive.ubuntu.com/ubuntu focal-backports/restricted amd64 c-n-f Metadata [116 B]
Get:27 http://azure.archive.ubuntu.com/ubuntu focal-backports/universe amd64 Packages [24.0 kB]
Get:28 http://azure.archive.ubuntu.com/ubuntu focal-backports/universe Translation-en [16.0 kB]
Get:29 http://azure.archive.ubuntu.com/ubuntu focal-backports/universe amd64 c-n-f Metadata [864 B]
Get:30 http://azure.archive.ubuntu.com/ubuntu focal-backports/multiverse amd64 c-n-f Metadata [116 B]
Get:31 http://azure.archive.ubuntu.com/ubuntu focal-security/main amd64 Packages [1822 kB]
Get:32 http://azure.archive.ubuntu.com/ubuntu focal-security/main Translation-en [301 kB]
Get:33 http://azure.archive.ubuntu.com/ubuntu focal-security/main amd64 c-n-f Metadata [11.2 kB]
Get:34 http://azure.archive.ubuntu.com/ubuntu focal-security/restricted amd64 Packages [1289 kB]
Get:35 http://azure.archive.ubuntu.com/ubuntu focal-security/restricted Translation-en [183 kB]
Get:36 http://azure.archive.ubuntu.com/ubuntu focal-security/universe amd64 Packages [743 kB]
Get:37 http://azure.archive.ubuntu.com/ubuntu focal-security/universe Translation-en [137 kB]
Get:38 http://azure.archive.ubuntu.com/ubuntu focal-security/universe amd64 c-n-f Metadata [15.3 kB]
Get:39 http://azure.archive.ubuntu.com/ubuntu focal-security/multiverse amd64 Packages [22.2 kB]
Get:40 http://azure.archive.ubuntu.com/ubuntu focal-security/multiverse Translation-en [5376 B]
Get:41 http://azure.archive.ubuntu.com/ubuntu focal-security/multiverse amd64 c-n-f Metadata [508 B]
Fetched 24.7 MB in 5s (5224 kB/s)
Reading package lists... Done
Building dependency tree
Reading state information... Done
24 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

2. Certifique-se da instalação do pacote fail2ban

`student@vm01:~$ sudo apt install fail2ban`

```bash
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following additional packages will be installed:
  python3-pyinotify whois
Suggested packages:
  mailx monit sqlite3 python-pyinotify-doc
The following NEW packages will be installed:
  fail2ban python3-pyinotify whois
0 upgraded, 3 newly installed, 0 to remove and 24 not upgraded.
Need to get 444 kB of archives.
After this operation, 2400 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://azure.archive.ubuntu.com/ubuntu focal/universe amd64 fail2ban all 0.11.1-1 [375 kB]
Get:2 http://azure.archive.ubuntu.com/ubuntu focal/main amd64 python3-pyinotify all 0.9.6-1.2ubuntu1 [24.8 kB]
Get:3 http://azure.archive.ubuntu.com/ubuntu focal/main amd64 whois amd64 5.5.6 [44.7 kB]
Fetched 444 kB in 0s (1485 kB/s)
Selecting previously unselected package fail2ban.
(Reading database ... 58571 files and directories currently installed.)
Preparing to unpack .../fail2ban_0.11.1-1_all.deb ...
Unpacking fail2ban (0.11.1-1) ...
Selecting previously unselected package python3-pyinotify.
Preparing to unpack .../python3-pyinotify_0.9.6-1.2ubuntu1_all.deb ...
Unpacking python3-pyinotify (0.9.6-1.2ubuntu1) ...
Selecting previously unselected package whois.
Preparing to unpack .../archives/whois_5.5.6_amd64.deb ...
Unpacking whois (5.5.6) ...
Setting up whois (5.5.6) ...
Setting up fail2ban (0.11.1-1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/fail2ban.service → /lib/systemd/system/fail2ban.service.
Setting up python3-pyinotify (0.9.6-1.2ubuntu1) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for systemd (245.4-4ubuntu3.18) ...
```

`student@vm01:~$ cat /var/log/fail2ban.log`

```bash
2022-11-07 22:23:14,005 fail2ban.server         [2435]: INFO    --------------------------------------------------
2022-11-07 22:23:14,006 fail2ban.server         [2435]: INFO    Starting Fail2ban v0.11.1
2022-11-07 22:23:14,007 fail2ban.observer       [2435]: INFO    Observer start...
2022-11-07 22:23:14,010 fail2ban.database       [2435]: INFO    Connected to fail2ban persistent database '/var/lib/fail2ban/fail2ban.sqlite3'
2022-11-07 22:23:14,013 fail2ban.database       [2435]: WARNING New database created. Version '4'
2022-11-07 22:23:14,014 fail2ban.jail           [2435]: INFO    Creating new jail 'sshd'
2022-11-07 22:23:14,042 fail2ban.jail           [2435]: INFO    Jail 'sshd' uses pyinotify {}
2022-11-07 22:23:14,048 fail2ban.jail           [2435]: INFO    Initiated 'pyinotify' backend
2022-11-07 22:23:14,050 fail2ban.filter         [2435]: INFO      maxLines: 1
2022-11-07 22:23:14,086 fail2ban.filter         [2435]: INFO      maxRetry: 5
2022-11-07 22:23:14,087 fail2ban.filter         [2435]: INFO      findtime: 600
2022-11-07 22:23:14,087 fail2ban.actions        [2435]: INFO      banTime: 600
2022-11-07 22:23:14,087 fail2ban.filter         [2435]: INFO      encoding: UTF-8
2022-11-07 22:23:14,088 fail2ban.filter         [2435]: INFO    Added logfile: '/var/log/auth.log' (pos = 0, hash = aa3acac0baef2549bdff739fd0d460e8ef00fba0)
2022-11-07 22:23:14,093 fail2ban.jail           [2435]: INFO    Jail 'sshd' started
```

3. Certifique-se de que o Fail2Ban iniciará automaticamente durante o boot da VM

`student@vm01:~$ sudo systemctl status fail2ban`

```bash
● fail2ban.service - Fail2Ban Service
     Loaded: loaded (/lib/systemd/system/fail2ban.service; enabled; vendor preset: enabled)
     Active: active (running) since Mon 2022-11-07 22:23:13 UTC; 1min 47s ago
       Docs: man:fail2ban(1)
   Main PID: 2435 (f2b/server)
      Tasks: 5 (limit: 9530)
     Memory: 16.5M
     CGroup: /system.slice/fail2ban.service
             └─2435 /usr/bin/python3 /usr/bin/fail2ban-server -xf start

Nov 07 22:23:13 rmmartins systemd[1]: Starting Fail2Ban Service...
Nov 07 22:23:13 rmmartins systemd[1]: Started Fail2Ban Service.
Nov 07 22:23:14 rmmartins fail2ban-server[2435]: Server ready
```

4. Certifique-se de que o Fail2Ban está habilitado para proteger o serviço SSH

Certifique-se de que a seção [sshd] está presente e descomentada:

`student@vm01:~$ cat /etc/fail2ban/jail.conf`

```bash
[sshd]

# To use more aggressive sshd modes set filter parameter "mode" in jail.local:
# normal (default), ddos, extra or aggressive (combines all).
# See "tests/files/logs/sshd" or "filter.d/sshd.conf" for usage example and details.
#mode   = normal
port    = ssh
logpath = %(sshd_log)s
backend = %(sshd_backend)s
```

`student@vm01:~$ sudo fail2ban-client status sshd`

```bash
Status for the jail: sshd
|- Filter
|  |- Currently failed: 0
|  |- Total failed:     0
|  `- File list:        /var/log/auth.log
`- Actions
   |- Currently banned: 0
   |- Total banned:     0
   `- Banned IP list:
```

5. Altere a porta padrão do SSH de 22 para 2222

`student@vm01:~$ sudo su`
`root@vm01:/home/student# sed -i 's/#Port 22/Port 2222/g' /etc/ssh/sshd_config; systemctl restart sshd`

6. Configure chaves SSH para melhorar o método de conexão ao servidor

Neste exercício vamos usar o Windows Subsystem for Linux, mas você pode seguir [estas instruções](https://www.ssh.com/academy/ssh/putty/windows/puttygen) para usar o Putty. 

Usando o [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install) no seu computador local, gere um par de chaves SSH digitando:

`$ ssh-keygen`

```bash
rmmartins@DESKTOP-58U032B:~$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/home/rmmartins/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /home/rmmartins/.ssh/id_rsa
Your public key has been saved in /home/rmmartins/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:3xDVbIS9eE8Ij2ktzFzoIku6c7BF0pqmV89jBtME1Yw rmmartins@DESKTOP-58U032B
The key's randomart image is:
+---[RSA 3072]----+
|         ..+.B.  |
|        . E.* *  |
|       . ..= X o |
|      . = o.@ * .|
|       BS=.o o o |
|      * *..o    .|
|     o * =. .    |
|    . = . *      |
|     . o o .     |
+----[SHA256]-----+
```

Agora precisamos copiar a Chave Pública SSH para o servidor. A maneira mais simples é usar o ssh-copy-id. Então, no seu computador local, digite:

`$ ssh-copy-id <username>@<virtualmachine.ip> -p 2222`

_Note que a porta 2222 é usada, pois alteramos de 22 para 2222 anteriormente_

```bash
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/user/.ssh/id_rsa.pub"
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
user@20.3.122.121's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh -p '2222' 'user@20.3.122.121'"
and check to make sure that only the key(s) you wanted were added.
```

_Note que se sua chave privada SSH foi salva em outro local diferente do padrão /home/<user>/.ssh/id_rsa, você terá que especificar para a conexão como ssh -p '2222' 'user@20.3.122.121 -i <caminho.da.sua.chave.privada.ssh>'_

Então desabilite a autenticação por senha no servidor:

`student@vm01:~$ sudo nano /etc/ssh/sshd_config`

Procure por uma diretiva chamada PasswordAuthentication (ela pode estar comentada). Descomente a linha removendo o # no início da linha e defina o valor como no:

```bash
PasswordAuthentication no
```
Reinicie o serviço SSH

`student@vm01:~$ sudo systemctl restart ssh`