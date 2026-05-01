# Desafio 20 - Solução de Problemas no Linux (Projeto Final) - Guia do Coach
[< Solução Anterior](./Solution-19.md) - **[Início](./README.md)**

## Notas e Orientações

Este projeto final possui três cenários independentes. Os alunos devem trabalhar neles em ordem. Cada cenário tem uma fase de configuração que intencionalmente cria um estado com problema, seguida por uma fase de diagnóstico e reparo.

---

## Cenário A — "O Servidor Web Está Fora do Ar"

### Configuração (cria o estado com problema)

```bash
sudo systemctl stop nginx
sudo ufw deny 80/tcp 2>/dev/null
```

> Se o UFW não estiver ativo, o comando `ufw deny` ainda adicionará a regra, mas ela não terá efeito até que o UFW seja habilitado. O problema principal é que o nginx está parado.

### Passo a Passo

1. Verificar o sintoma

`student@vm01:~$ curl -s -o /dev/null -w "%{http_code}" http://localhost:80`

```bash
000
```

> Um código de retorno `000` significa que o curl não conseguiu conectar — o servidor não está escutando.

2. Verificar se o nginx está em execução

`student@vm01:~$ systemctl status nginx`

```bash
○ nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: inactive (dead) since Mon 2025-01-01 12:00:00 UTC; 2min ago
```

> **Causa raiz #1 identificada:** o nginx está `inactive (dead)`.

3. Verificar se a porta 80 está em escuta

`student@vm01:~$ sudo ss -tulnp | grep :80`

> Sem saída — confirmando que nada está escutando na porta 80.

4. Iniciar o nginx

`student@vm01:~$ sudo systemctl start nginx`

`student@vm01:~$ systemctl status nginx`

```bash
● nginx.service - A high performance web server and a reverse proxy server
     Active: active (running) since Mon 2025-01-01 12:05:00 UTC; 2s ago
```

5. Testar novamente

`student@vm01:~$ curl -s -o /dev/null -w "%{http_code}" http://localhost:80`

```bash
200
```

> Se o UFW estiver ativo e tiver uma regra de negação para a porta 80, conexões via localhost ainda podem funcionar (o UFW normalmente permite tráfego de loopback). No entanto, conexões remotas falhariam.

6. Verificar e corrigir o firewall (se o UFW estiver ativo)

`student@vm01:~$ sudo ufw status`

```bash
Status: active

To                         Action      From
--                         ------      ----
22/tcp                     LIMIT IN    Anywhere
80/tcp                     DENY IN     Anywhere
...
```

`student@vm01:~$ sudo ufw delete deny 80/tcp`

```bash
Rule deleted
Rule deleted (v6)
```

`student@vm01:~$ sudo ufw allow 80/tcp`

```bash
Rule added
Rule added (v6)
```

7. Verificação final

`student@vm01:~$ curl -s -o /dev/null -w "%{http_code}" http://localhost:80`

```bash
200
```

> Ambos os problemas estão resolvidos: o nginx está em execução e o firewall permite a porta 80.

---

## Cenário B — "Alerta de Espaço em Disco"

### Configuração (cria os arquivos de teste)

```bash
dd if=/dev/zero of=/tmp/bigfile bs=1M count=100 2>/dev/null
mkdir -p /tmp/oldlogs
for i in $(seq 1 50); do dd if=/dev/zero of=/tmp/oldlogs/app-$i.log bs=1M count=1 2>/dev/null; done
```

> Isso cria um arquivo de 100MB e 50 arquivos de log de 1MB cada (150MB no total).

### Passo a Passo

1. Verificar o uso de disco

`student@vm01:~$ df -h`

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G   5.2G   24G  18% /
tmpfs           2.0G     0  2.0G   0% /dev/shm
tmpfs           393M  1.1M  392M   1% /run
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/sda15      105M  6.1M   99M   6% /boot/efi
tmpfs           393M   12K  393M   1% /run/user/1000
```

> Os valores exatos variam. O aluno deve observar o nível de uso atual.

2. Descobrir o que está consumindo espaço em /tmp

`student@vm01:~$ du -sh /tmp/* 2>/dev/null | sort -rh | head -10`

```bash
100M    /tmp/bigfile
50M     /tmp/oldlogs
4.0K    /tmp/practice.log
4.0K    /tmp/mycron
...
```

> **Causa raiz identificada:** `/tmp/bigfile` (100MB) e `/tmp/oldlogs/` (50MB) estão consumindo mais espaço.

3. Encontrar arquivos maiores que 10MB

`student@vm01:~$ find /tmp -size +10M -exec ls -lh {} \; 2>/dev/null`

```bash
-rw-rw-r-- 1 student student 100M Jan  1 12:00 /tmp/bigfile
```

4. Contar arquivos de log antigos

`student@vm01:~$ find /tmp/oldlogs -name "*.log" -type f | wc -l`

```bash
50
```

5. Limpar

`student@vm01:~$ rm /tmp/bigfile`

`student@vm01:~$ rm -rf /tmp/oldlogs`

6. Verificar se o espaço em disco foi recuperado

`student@vm01:~$ df -h`

```bash
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        30G   5.1G   24G  18% /
...
```

> O espaço usado deve ter diminuído aproximadamente 150MB.

---

## Cenário C — "Mistério do Alto Uso de CPU"

### Configuração (cria o processo descontrolado)

```bash
nohup bash -c 'while true; do echo "busy" > /dev/null; done' &
```

> Isso cria um loop infinito em um processo bash que consumirá quase 100% de um núcleo de CPU.

### Passo a Passo

1. Verificar a carga do sistema

`student@vm01:~$ uptime`

```bash
 12:10:00 up  2:10,  1 user,  load average: 1.05, 0.78, 0.42
```

> Uma média de carga acima de 1.0 em uma máquina de núcleo único (ou acima do número de núcleos de CPU) indica pressão de CPU. A média de 1 minuto (primeiro número) será a mais alta, pois o processo acabou de ser iniciado.

2. Identificar os maiores consumidores de CPU

`student@vm01:~$ ps aux --sort=-%cpu | head -10`

```bash
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
student     2500 99.0  0.1   7488  3456 pts/0    R    12:08   2:15 bash -c while true; do echo "busy" > /dev/null; done
root           1  0.1  0.5 168936 11584 ?        Ss   10:00   0:05 /sbin/init
root         610  0.0  0.3  25332  7168 ?        Ss   10:00   0:01 /lib/systemd/systemd-resolved
student     1800  0.0  0.2  10568  5376 pts/0    Ss   11:00   0:00 -bash
...
```

> **Causa raiz identificada:** O PID 2500 é um processo bash executando a 99% de CPU com o comando `while true; do echo "busy" > /dev/null; done`.

Alternativamente, usando `top`:

`student@vm01:~$ top -b -n 1 | head -20`

```bash
top - 12:10:00 up 2:10,  1 user,  load average: 1.05, 0.78, 0.42
Tasks: 105 total,   2 running, 103 sleeping,   0 stopped,   0 zombie
%Cpu(s): 50.2 us,  0.3 sy,  0.0 ni, 49.3 id,  0.0 wa,  0.0 hi,  0.2 si,  0.0 st
MiB Mem :   1963.2 total,    923.4 free,    512.8 used,    527.0 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.   1315.6 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2500 student   20   0    7488   3456   3200 R  99.0   0.2   2:15.23 bash
      1 root      20   0  168936  11584   8448 S   0.1   0.6   0:05.12 systemd
    610 root      20   0   25332   7168   6400 S   0.0   0.4   0:01.34 systemd-resolve
```

3. Encontrar o processo bash descontrolado e seu PID

> A partir da saída acima, o PID `2500` é o culpado (o PID real variará em cada sistema).

4. Verificar o que o processo está fazendo

`student@vm01:~$ cat /proc/2500/cmdline | tr '\0' ' '`

```bash
bash -c while true; do echo "busy" > /dev/null; done
```

> Isso confirma que o processo está executando o loop infinito. O `tr '\0' ' '` converte bytes nulos (que separam argumentos em `/proc/*/cmdline`) em espaços para legibilidade.

5. Matar o processo

`student@vm01:~$ kill 2500`

6. Se não parar, forçar o encerramento

`student@vm01:~$ kill -9 2500`

> `kill` envia SIGTERM (sinal 15) que pede ao processo para encerrar graciosamente. `kill -9` envia SIGKILL que o termina imediatamente. Para este loop infinito, `kill` (SIGTERM) deve funcionar, pois o processo bash irá tratá-lo.

7. Verificar se o uso de CPU voltou ao normal

`student@vm01:~$ uptime`

```bash
 12:12:00 up  2:12,  1 user,  load average: 0.65, 0.72, 0.45
```

> A média de carga de 1 minuto deve começar a cair. Pode levar alguns minutos para as três médias de carga se normalizarem, pois são médias móveis exponenciais (1 minuto, 5 minutos, 15 minutos).

8. Verificar o uso de memória

`student@vm01:~$ free -h`

```bash
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       512Mi       923Mi       1.0Mi       527Mi       1.3Gi
Swap:             0B          0B          0B
```

> A memória deve estar normal — o processo descontrolado era intensivo em CPU, não em memória. A coluna `available` é o melhor indicador de memória utilizável (inclui cache recuperável).
