# Desafio 18 - Agendamento de Tarefas com Cron - Guia do Coach
[< Solução Anterior](./Solution-17.md) - **[Início](./README.md)** - [Próxima Solução >](./Solution-19.md)

## Notas e Orientações

1. Verificar se o cron está em execução

`student@vm01:~$ systemctl status cron`

```bash
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Mon 2025-01-01 10:00:00 UTC; 3h ago
       Docs: man:cron(8)
   Main PID: 800 (cron)
      Tasks: 1 (limit: 4657)
     Memory: 428.0K
        CPU: 15ms
     CGroup: /system.slice/cron.service
             └─800 /usr/sbin/cron -f -P
```

> No Ubuntu 24.04, o serviço cron é chamado `cron` (e não `crond` como em algumas outras distribuições).

2. Visualizar o crontab do usuário atual

`student@vm01:~$ crontab -l`

```bash
no crontab for student
```

> Isso é esperado se nenhum cron job foi configurado ainda.

3. Entender a sintaxe do cron

Os cinco campos são:

```
┌───────────── minuto (0 - 59)
│ ┌───────────── hora (0 - 23)
│ │ ┌───────────── dia do mês (1 - 31)
│ │ │ ┌───────────── mês (1 - 12)
│ │ │ │ ┌───────────── dia da semana (0 - 7, onde 0 e 7 são domingo)
│ │ │ │ │
* * * * * comando a executar
```

Exemplos comuns:
- `*/5 * * * *` — a cada 5 minutos
- `0 * * * *` — a cada hora no minuto 0
- `30 2 * * *` — todos os dias às 2:30 AM
- `0 0 * * 0` — todo domingo à meia-noite
- `0 9 1 * *` — primeiro dia de cada mês às 9:00 AM

4. Criar uma tarefa agendada

`student@vm01:~$ echo '*/5 * * * * echo "Cron is alive at $(date)" >> /tmp/cron-test.log' > /tmp/mycron`

`student@vm01:~$ crontab /tmp/mycron`

```bash
crontab: installing new crontab
```

`student@vm01:~$ crontab -l`

```bash
*/5 * * * * echo "Cron is alive at $(date)" >> /tmp/cron-test.log
```

5. Verificar se o cron job foi executado (após esperar 5 minutos)

`student@vm01:~$ cat /tmp/cron-test.log`

```bash
Cron is alive at Mon Jan  1 12:05:00 UTC 2025
Cron is alive at Mon Jan  1 12:10:00 UTC 2025
```

> Se o arquivo ainda não existir, o cron job ainda não foi disparado. Aguarde até o próximo intervalo de 5 minutos (por exemplo, :00, :05, :10, :15...).

6. Criar um script de limpeza e agendá-lo

`student@vm01:~$ cat > /tmp/cleanup.sh << 'EOF'`

```bash
#!/bin/bash
find /tmp -name "*.log" -mtime +7 -delete 2>/dev/null
echo "Cleanup ran at $(date)" >> /var/log/cleanup.log
EOF
```

`student@vm01:~$ chmod +x /tmp/cleanup.sh`

Adicionar ao cron:

`student@vm01:~$ echo '0 0 * * * /tmp/cleanup.sh' >> /tmp/mycron`

`student@vm01:~$ crontab /tmp/mycron`

```bash
crontab: installing new crontab
```

`student@vm01:~$ crontab -l`

```bash
*/5 * * * * echo "Cron is alive at $(date)" >> /tmp/cron-test.log
0 0 * * * /tmp/cleanup.sh
```

> **Nota:** O script de limpeza escreve em `/var/log/cleanup.log`, que requer permissões de root. Se estiver executando como um usuário não-root, o cron job falhará silenciosamente ao tentar escrever nesse log. Em um cenário real, você executaria via `sudo crontab -e` (crontab do root) ou escreveria em um local acessível ao usuário.

7. Visualizar cron jobs do sistema

`student@vm01:~$ ls -la /etc/cron.d/ /etc/cron.daily/ /etc/cron.hourly/`

```bash
/etc/cron.d/:
total 20
drwxr-xr-x  2 root root 4096 Jan  1  2025 .
drwxr-xr-x 90 root root 4096 Jan  1  2025 ..
-rw-r--r--  1 root root  201 Jan  1  2024 e2scrub_all

/etc/cron.daily/:
total 28
drwxr-xr-x  2 root root 4096 Jan  1  2025 .
drwxr-xr-x 90 root root 4096 Jan  1  2025 ..
-rwxr-xr-x  1 root root  376 Jan  1  2024 apport
-rwxr-xr-x  1 root root 1478 Jan  1  2024 apt-compat
-rwxr-xr-x  1 root root  123 Jan  1  2024 dpkg
-rwxr-xr-x  1 root root  377 Jan  1  2024 logrotate

/etc/cron.hourly/:
total 8
drwxr-xr-x  2 root root 4096 Jan  1  2025 .
drwxr-xr-x 90 root root 4096 Jan  1  2025 ..
```

> Scripts colocados em `/etc/cron.daily/` são executados uma vez por dia pelo sistema. Da mesma forma, `/etc/cron.hourly/`, `/etc/cron.weekly/` e `/etc/cron.monthly/` existem para outros intervalos.

8. Instalar e usar `at` para uma tarefa única

`student@vm01:~$ sudo apt install -y at`

`student@vm01:~$ echo "echo 'One-time task ran at $(date)' >> /tmp/at-test.log" | at now + 1 minute`

```bash
warning: commands will be executed using /bin/sh
job 1 at Mon Jan  1 12:31:00 2025
```

`student@vm01:~$ atq`

```bash
1       Mon Jan  1 12:31:00 2025 a student
```

> O comando `atq` mostra os jobs na fila. O número do job (1), horário agendado, letra da fila (a) e nome do usuário são exibidos.

9. Verificar se o job `at` foi executado (após esperar 1 minuto)

`student@vm01:~$ cat /tmp/at-test.log`

```bash
One-time task ran at Mon Jan  1 12:31:00 UTC 2025
```

`student@vm01:~$ atq`

```bash
```

> Após o job ser executado, `atq` mostrará uma lista vazia — o job foi removido da fila.

10. Limpar — remover seu crontab

`student@vm01:~$ crontab -r`

`student@vm01:~$ crontab -l`

```bash
no crontab for student
```

> O flag `-r` remove o crontab inteiro do usuário atual. Use com cuidado — não há prompt de confirmação.
