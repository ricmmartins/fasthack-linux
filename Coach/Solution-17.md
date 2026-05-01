# Desafio 17 - Processamento de Texto com sed, awk e Pipes - Guia do Coach
[< Solução Anterior](./Solution-16.md) - **[Início](./README.md)** - [Próxima Solução >](./Solution-18.md)

## Notas e Orientações

1. Criar um arquivo de log de exemplo para os exercícios

`student@vm01:~$ sudo cp /var/log/syslog /tmp/practice.log 2>/dev/null || journalctl --no-pager -n 200 > /tmp/practice.log`

> No Ubuntu 24.04, `/var/log/syslog` existe se o rsyslog estiver instalado. Caso contrário, o fallback usa `journalctl` para gerar um log de prática. Qualquer uma das fontes funciona para os exercícios.

2. Usar `cut` para extrair os três primeiros campos

`student@vm01:~$ cut -d' ' -f1-3 /tmp/practice.log | head -10`

```bash
Jan 01 10:00:00
Jan 01 10:00:01
Jan 01 10:00:01
Jan 01 10:00:02
Jan 01 10:00:03
Jan 01 10:00:05
Jan 01 10:00:05
Jan 01 10:00:10
Jan 01 10:00:10
Jan 01 10:00:15
```

> Se estiver usando a saída do `journalctl`, o formato pode diferir ligeiramente (por exemplo, `Jan 01 10:00:00` vs um timestamp mais longo). Ajuste os números dos campos se necessário.

3. Encontrar as 10 palavras mais frequentes na coluna 5

`student@vm01:~$ awk '{print $5}' /tmp/practice.log | sort | uniq -c | sort -rn | head -10`

```bash
     45 systemd[1]:
     23 systemd-resolved[610]:
     18 sshd[750]:
     12 networkd-dispatcher[680]:
     10 cron[800]:
      8 systemd-logind[690]:
      5 kernel:
      3 dbus-daemon[620]:
      2 rsyslogd:
      1 snapd[900]:
```

> A saída mostra quais processos geram mais entradas de log. Isso é útil para identificar serviços ruidosos.

4. Converter para maiúsculas com `tr`

`student@vm01:~$ head -5 /tmp/practice.log | tr '[:lower:]' '[:upper:]'`

```bash
JAN 01 10:00:00 VM01 SYSTEMD[1]: STARTED NETWORK NAME RESOLUTION.
JAN 01 10:00:01 VM01 SYSTEMD[1]: STARTED OPENBSD SECURE SHELL SERVER.
JAN 01 10:00:01 VM01 SSHD[750]: SERVER LISTENING ON 0.0.0.0 PORT 22.
JAN 01 10:00:02 VM01 SSHD[750]: SERVER LISTENING ON :: PORT 22.
JAN 01 10:00:03 VM01 SYSTEMD[1]: REACHED TARGET MULTI-USER SYSTEM.
```

5. Usar `sed` para substituir o hostname por "REDACTED"

Primeiro, descubra seu hostname:

`student@vm01:~$ hostname`

```bash
vm01
```

Depois substitua:

`student@vm01:~$ sed 's/vm01/REDACTED/g' /tmp/practice.log > /tmp/redacted.log`

Verifique:

`student@vm01:~$ head -3 /tmp/redacted.log`

```bash
Jan 01 10:00:00 REDACTED systemd[1]: Started Network Name Resolution.
Jan 01 10:00:01 REDACTED systemd[1]: Started OpenBSD Secure Shell server.
Jan 01 10:00:01 REDACTED sshd[750]: Server listening on 0.0.0.0 port 22.
```

> Substitua `vm01` pelo hostname real da máquina do aluno.

6. Deletar linhas em branco com `sed`

`student@vm01:~$ sed '/^$/d' /tmp/practice.log`

> Isso remove todas as linhas vazias. A regex `^$` corresponde a linhas sem nada entre o início (`^`) e o fim (`$`). Para ver o efeito, você pode comparar a contagem de linhas:

```bash
wc -l /tmp/practice.log
sed '/^$/d' /tmp/practice.log | wc -l
```

7. Imprimir linhas com mais de 80 caracteres com `awk`

`student@vm01:~$ awk 'length > 80' /tmp/practice.log | head -10`

> Isso mostrará apenas as entradas de log mais longas. Linhas longas típicas incluem descrições de serviços, mensagens de autenticação SSH ou mensagens do kernel.

8. Somar uma coluna numérica com `awk`

`student@vm01:~$ echo -e "apples 5\nbananas 12\noranges 3\ngrapes 8" > /tmp/fruits.txt`

`student@vm01:~$ awk '{sum += $2} END {print "Total:", sum}' /tmp/fruits.txt`

```bash
Total: 28
```

> O programa `awk` adiciona a coluna 2 (`$2`) a uma variável `sum` acumuladora para cada linha, e depois imprime o total após processar todas as linhas (bloco `END`). Esse padrão é extremamente útil para somar valores em relatórios, logs ou arquivos CSV.

9. Encontrar endereços IP únicos no log

`student@vm01:~$ grep -oE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' /tmp/practice.log | sort -u`

```bash
0.0.0.0
10.0.0.4
127.0.0.1
127.0.0.53
168.63.129.16
```

> O flag `-o` exibe apenas a parte correspondente (não a linha inteira), e `-E` habilita regex estendida. A regex `[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+` corresponde a padrões de endereços IPv4. `sort -u` remove duplicatas. Nota: esta regex é um padrão simples e pode corresponder a números de versão ou outros números separados por pontos — para uso em produção, você adicionaria validação de faixa.

10. Contar arquivos .conf em /etc

`student@vm01:~$ find /etc -name "*.conf" 2>/dev/null | wc -l`

```bash
87
```

> A contagem exata depende dos pacotes instalados. O `2>/dev/null` suprime erros de "Permissão negada" para diretórios que o aluno não pode ler. O `wc -l` conta o número de linhas (um arquivo por linha) da saída do `find`.
