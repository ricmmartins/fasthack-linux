# Desafio 16 - systemd e Gerenciamento de Serviços - Guia do Coach
[< Solução Anterior](./Solution-15.md) - **[Início](./README.md)** - [Próxima Solução >](./Solution-17.md)

## Notas e Orientações

1. Listar todos os serviços ativos

`student@vm01:~$ systemctl list-units --type=service --state=active`

```bash
  UNIT                               LOAD   ACTIVE SUB     DESCRIPTION
  cron.service                       loaded active running Regular background program processing daemon
  dbus.service                       loaded active running D-Bus System Message Bus
  getty@tty1.service                 loaded active running Getty on tty1
  networkd-dispatcher.service        loaded active running Dispatcher daemon for systemd-networkd
  rsyslog.service                    loaded active running System Logging Service
  ssh.service                        loaded active running OpenBSD Secure Shell server
  systemd-journald.service           loaded active running Journal Service
  systemd-logind.service             loaded active running User Login Management
  systemd-networkd.service           loaded active running Network Configuration
  systemd-resolved.service           loaded active running Network Name Resolution
  systemd-udevd.service              loaded active running Rule-based Manager for Device Events and Files
  ...
```

2. Verificar o status do serviço SSH

`student@vm01:~$ systemctl status ssh`

```bash
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; enabled; preset: enabled)
     Active: active (running) since Mon 2025-01-01 10:00:00 UTC; 2h ago
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 700 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 750 (sshd)
      Tasks: 1 (limit: 4657)
     Memory: 5.2M
        CPU: 120ms
     CGroup: /system.slice/ssh.service
             └─750 "sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups"
```

> No Ubuntu 24.04, o serviço SSH é chamado `ssh` (e não `sshd` como em algumas outras distribuições).

3. Verificar se o nginx está instalado e em execução

`student@vm01:~$ systemctl status nginx`

Se o nginx não estiver instalado, você verá:

```bash
Unit nginx.service could not be found.
```

Instale-o:

`student@vm01:~$ sudo apt install -y nginx`

Depois verifique novamente:

`student@vm01:~$ systemctl status nginx`

```bash
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Mon 2025-01-01 12:00:00 UTC; 10s ago
       Docs: man:nginx(8)
    Process: 1234 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 1235 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 1236 (nginx)
      Tasks: 3 (limit: 4657)
     Memory: 4.8M
        CPU: 50ms
     CGroup: /system.slice/nginx.service
             ├─1236 "nginx: master process /usr/sbin/nginx -g daemon on; master_process on;"
             ├─1237 "nginx: worker process"
             └─1238 "nginx: worker process"
```

4. Parar o serviço nginx e verificar

`student@vm01:~$ sudo systemctl stop nginx`

`student@vm01:~$ systemctl status nginx`

```bash
○ nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: inactive (dead) since Mon 2025-01-01 12:05:00 UTC; 5s ago
    Process: 1235 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
   Main PID: 1236 (code=exited, status=0/SUCCESS)
        CPU: 50ms
```

> Observe que o status mudou de `active (running)` para `inactive (dead)`.

5. Iniciar o nginx novamente

`student@vm01:~$ sudo systemctl start nginx`

`student@vm01:~$ systemctl is-active nginx`

```bash
active
```

6. Reiniciar o nginx

`student@vm01:~$ sudo systemctl restart nginx`

`student@vm01:~$ systemctl is-active nginx`

```bash
active
```

7. Desabilitar o nginx de iniciar no boot

`student@vm01:~$ sudo systemctl disable nginx`

```bash
Synchronizing state of nginx.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install disable nginx
Removed "/etc/systemd/system/multi-user.target.wants/nginx.service".
```

`student@vm01:~$ systemctl is-enabled nginx`

```bash
disabled
```

8. Reabilitar o nginx no boot

`student@vm01:~$ sudo systemctl enable nginx`

```bash
Synchronizing state of nginx.service with SysV service script with /usr/lib/systemd/systemd-sysv-install.
Executing: /usr/lib/systemd/systemd-sysv-install enable nginx
Created symlink /etc/systemd/system/multi-user.target.wants/nginx.service → /usr/lib/systemd/system/nginx.service.
```

`student@vm01:~$ systemctl is-enabled nginx`

```bash
enabled
```

9. Visualizar as últimas 20 linhas dos logs do nginx

`student@vm01:~$ journalctl -u nginx --no-pager -n 20`

```bash
Jan 01 12:00:00 vm01 systemd[1]: Starting nginx.service - A high performance web server and a reverse proxy server...
Jan 01 12:00:00 vm01 nginx[1234]: nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
Jan 01 12:00:00 vm01 nginx[1234]: nginx: configuration file /etc/nginx/nginx.conf test is successful
Jan 01 12:00:00 vm01 systemd[1]: Started nginx.service - A high performance web server and a reverse proxy server.
```

10. Visualizar todos os logs da última hora

`student@vm01:~$ journalctl --since "1 hour ago" --no-pager | tail -30`

> Isso exibirá as 30 linhas mais recentes de todas as entradas de log do sistema da última hora. A saída variará dependendo da atividade do sistema.

11. Criar um serviço systemd personalizado

`student@vm01:~$ sudo tee /etc/systemd/system/hello.service << 'EOF'`

```bash
[Unit]
Description=Hello World Service
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/echo "Hello from systemd!"
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
EOF
```

`student@vm01:~$ sudo systemctl daemon-reload`

`student@vm01:~$ sudo systemctl start hello`

`student@vm01:~$ sudo systemctl status hello`

```bash
● hello.service - Hello World Service
     Loaded: loaded (/etc/systemd/system/hello.service; disabled; preset: enabled)
     Active: active (exited) since Mon 2025-01-01 12:30:00 UTC; 5s ago
    Process: 2000 ExecStart=/usr/bin/echo Hello from systemd! (code=exited, status=0/SUCCESS)
   Main PID: 2000 (code=exited, status=0/SUCCESS)
        CPU: 2ms
```

> O status mostra `active (exited)` porque o tipo do serviço é `oneshot` com `RemainAfterExit=yes`. Isso significa que o serviço foi executado uma vez e concluído, mas o systemd o considera "ativo" porque ele deve permanecer nesse estado.

`student@vm01:~$ journalctl -u hello --no-pager`

```bash
Jan 01 12:30:00 vm01 systemd[1]: Starting hello.service - Hello World Service...
Jan 01 12:30:00 vm01 echo[2000]: Hello from systemd!
Jan 01 12:30:00 vm01 systemd[1]: Finished hello.service - Hello World Service.
```

> A mensagem "Hello from systemd!" é visível na saída do journal, confirmando que o serviço foi executado com sucesso.
