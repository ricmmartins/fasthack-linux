# Desafio 03 - Manipulando arquivos - Guia do Coach 

[< Solução Anterior](./Solution-02.md) - **[Home](./README.md)** - [Próxima Solução >](./Solution-04.md)

## Notas e Orientações
1. Encontre no diretório `/var` todos os arquivos que foram modificados nos últimos 60 minutos

`student@vm01:~$ sudo find /var -type f -mmin -60`

```bash
/var/log/waagent.log
/var/log/auth.log
/var/log/kern.log
/var/log/btmp
/var/log/journal/2de8116a95784f3b8a0a87cc7ec8edb3/system.journal
/var/log/journal/2de8116a95784f3b8a0a87cc7ec8edb3/user-1000.journal
/var/log/syslog
/var/lib/waagent/Prod.2.manifest.xml
/var/lib/waagent/logcollector/logs.zip
/var/lib/waagent/logcollector/results.txt
/var/lib/waagent/waagent_status.2.json
/var/lib/logrotate/omsagent-status
/var/lib/update-notifier/updates-available
/var/lib/chrony/chrony.drift
/var/lib/apt/periodic/update-success-stamp
/var/cache/apt/srcpkgcache.bin
/var/cache/apt/pkgcache.bin
/var/opt/omi/log/omi-logrotate.status
/var/opt/microsoft/omsconfig/omsconfig.log
/var/opt/microsoft/omsconfig/omsconfigdetailed.log
/var/opt/microsoft/omsconfig/status/omsconfighost
/var/opt/microsoft/omsconfig/run/python/996/dsc_python_client.pid
/var/opt/microsoft/omsagent/bd86f0a1-de9e-4b93-ac76-ad6c417b11ef/log/omsagent.log
/var/opt/microsoft/omsagent/bd86f0a1-de9e-4b93-ac76-ad6c417b11ef/log/ODSIngestion.status
/var/opt/microsoft/omsagent/bd86f0a1-de9e-4b93-ac76-ad6c417b11ef/state/omsconfig.log.auditd_plugin.pos
/var/opt/microsoft/omsagent/bd86f0a1-de9e-4b93-ac76-ad6c417b11ef/state/out_oms_audit.b5dc259ad4ddf7131.buffer
/var/opt/microsoft/omsagent/bd86f0a1-de9e-4b93-ac76-ad6c417b11ef/state/out_oms_common.b5dc258e41778160b.buffer
/var/opt/microsoft/omsagent/bd86f0a1-de9e-4b93-ac76-ad6c417b11ef/state/omsconfig.log.auditd_dsc_log.pos
/var/opt/microsoft/auoms/auomscollect.lock
```
2. Mostre o tipo de arquivo de `/usr/bin/htop`, `/etc/passwd` e `/usr/bin/passwd`

`student@vm01:~$ file /usr/bin/htop /etc/passwd /usr/bin/passwd`

```bash
/bin/htop: ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=732986edd7d25415061c74c17cb3db139bee2775, for GNU/Linux 3.2.0, stripped
/etc/passwd:     ASCII text
/usr/bin/passwd: setuid ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=6af93256cb810d90b2f96fc052b05b43b954f5b2, for GNU/Linux 3.2.0, stripped
```

3. Vá para o seu diretório home e baixe [azure-linux.svg](https://docs.microsoft.com/en-us/learn/achievements/azure-linux.svg) e [InfographicRC2.pdf](https://azure.microsoft.com/mediahandler/files/resourcefiles/infographic-reliability-with-microsoft-azure/InfographicRC2.pdf)

`student@vm01:~$ cd ~; wget https://docs.microsoft.com/en-us/learn/achievements/azure-linux.svg`

```bash
--2022-04-08 00:01:28--  https://docs.microsoft.com/en-us/learn/achievements/azure-linux.svg
Resolving docs.microsoft.com (docs.microsoft.com)... 104.112.140.13, 2600:1419:bc00:493::353e, 2600:1419:bc00:48e::353e
Connecting to docs.microsoft.com (docs.microsoft.com)|104.112.140.13|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [image/svg+xml]
Saving to: 'azure-linux.svg'

azure-linux.svg                                                                    [ <=>                                                                                                                                                              ]   1.58M  --.-KB/s    in 0.02s

2022-04-08 00:01:28 (67.5 MB/s) - 'azure-linux.svg' saved [1651731]
```

`student@vm01:~$ wget https://azure.microsoft.com/mediahandler/files/resourcefiles/infographic-reliability-with-microsoft-azure/InfographicRC2.pdf`

```bash
--2022-11-09 12:44:18--  https://azure.microsoft.com/mediahandler/files/resourcefiles/infographic-reliability-with-microsoft-azure/InfographicRC2.pdf
Resolving azure.microsoft.com (azure.microsoft.com)... 13.107.42.16, 2620:1ec:21::16
Connecting to azure.microsoft.com (azure.microsoft.com)|13.107.42.16|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 993229 (970K) [application/pdf]
Saving to: 'InfographicRC2.pdf'

InfographicRC2.pdf            100%[=================================================>] 969.95K  4.19MB/s    in 0.2s

2022-11-09 12:44:19 (4.19 MB/s) - 'InfographicRC2.pdf' saved [993229/993229]
```

4. Exiba o tipo de arquivo de azure-linux.svg e InfographicRC2.pdf

`student@vm01:~$ file azure-linux.svg InfographicRC2.pdf`

```bash
azure-linux.svg:     SVG Scalable Vector Graphics image
InfographicRC2.pdf: PDF document, version 1.5
```

5. Renomeie azure-linux.svg para azure-linux.pdf 

`student@vm01:~$ mv azure-linux.svg azure-linux.pdf`

6. Exiba o tipo de arquivo de azure-linux.pdf e InfographicRC2.pdf

`student@vm01:~$ file azure-linux.pdf InfographicRC2.pdf`

```bash
azure-linux.pdf:     SVG Scalable Vector Graphics image
InfographicRC2.pdf: PDF document, version 1.5
```

7. Crie um diretório `~/lab` e entre nele.

`student@vm01:~$ mkdir ~/lab ; cd ~/lab`

8. Crie o arquivo today.log e o arquivo yesterday.log em lab.

`student@vm01:~$ touch today.log yesterday.log`

9. Verifique a data e hora de criação

`student@vm01:~$ ls -l`

```bash
total 0
-rw-rw-r-- 1 student student 0 Apr  7 23:50 today.log
-rw-rw-r-- 1 student student 0 Apr  7 23:50 yesterday.log
```

10. Altere a data de yesterday.log para corresponder à data de ontem

`student@vm01:~$ touch -t 202204061200 yesterday.log (substitute 20220407 with yesterday date - 20220406 as e.g. )`

11. Verifique a data e hora de criação novamente

`student@vm01:~$ ls -l`

```bash
total 0
-rw-rw-r-- 1 student student 0 Apr  7 23:50 today.log
-rw-rw-r-- 1 student student 0 Apr  6 12:00 yesterday.log
```

12. Crie um diretório chamado `~/testbackup` e copie todos os arquivos de `~/lab` para ele.

`student@vm01:~$ mkdir ~/testbackup ; cp -r ~/lab  ~/testbackup/ ; ls -R  ~/testbackup`

13. Use um comando para remover o diretório `~/testbackup` e todos os arquivos dentro dele.

`student@vm01:~$ rm -rf ~/testbackup `

14. Crie um diretório `~/logbackup` e copie os arquivos `*.log` de `/var/log` para ele

`student@vm01:~$ mkdir ~/logbackup ; cp -r /var/log/*.log ~/logbackup ; ls -l ~/logbackup`

```bash
total 1796
-rw-r--r-- 1 rmmartins rmmartins    383 Apr 11 15:39 alternatives.log
-rw-r----- 1 rmmartins rmmartins 907368 Apr 11 15:39 auth.log
-rw-r----- 1 rmmartins rmmartins   7717 Apr 11 15:39 cloud-init-output.log
-rw-r--r-- 1 rmmartins rmmartins 307950 Apr 11 15:39 cloud-init.log
-rw-r--r-- 1 rmmartins rmmartins  33526 Apr 11 15:39 dpkg.log
-rw-r----- 1 rmmartins rmmartins 371034 Apr 11 15:39 kern.log
-rw-r--r-- 1 rmmartins rmmartins   2290 Apr 11 15:39 ubuntu-advantage-timer.log
-rw-r--r-- 1 rmmartins rmmartins 190238 Apr 11 15:39 waagent.log
```
15. Conte o número de linhas do arquivo `/etc/wgetrc`

`student@vm01:~$ wc -l /etc/wgetrc`

```bash
138 /etc/wgetrc
```

16. Conte o número de palavras do arquivo `/etc/hdparm.conf`

`student@vm01:~$ wc -w /etc/hdparm.conf`

```bash
854 /etc/hdparm.conf
```