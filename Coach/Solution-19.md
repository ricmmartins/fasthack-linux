# Desafio 19 - Configuração de Firewall com UFW - Guia do Coach
[< Solução Anterior](./Solution-18.md) - **[Início](./README.md)** - [Próxima Solução >](./Solution-20.md)

## Notas e Orientações

> **Nota de recuperação:** Se um aluno ficar trancado fora da VM após habilitar o UFW sem permitir SSH, ele deve acessar a VM via console em nuvem (console serial na maioria dos provedores de nuvem) ou display local e executar `sudo ufw disable` para restaurar o acesso.

1. Verificar o status atual do firewall

`student@vm01:~$ sudo ufw status verbose`

```bash
Status: inactive
```

> Por padrão, o UFW está instalado mas não habilitado no Ubuntu 24.04.

2. Permitir acesso SSH antes de habilitar o firewall

`student@vm01:~$ sudo ufw allow 22/tcp`

```bash
Rules updated
Rules updated (v6)
```

> **CRÍTICO:** Isso deve ser feito antes do passo 3. Se o aluno alterou a porta SSH no Desafio 13 (por exemplo, para 2222), ele deve usar `sudo ufw allow 2222/tcp` em vez disso.

3. Habilitar o firewall

`student@vm01:~$ sudo ufw enable`

```bash
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
```

4. Verificar o status após habilitar

`student@vm01:~$ sudo ufw status verbose`

```bash
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
```

> A política padrão é `deny (incoming)` — todo tráfego de entrada é bloqueado a menos que seja explicitamente permitido. O tráfego de saída é permitido por padrão.

5. Permitir HTTP e HTTPS

`student@vm01:~$ sudo ufw allow 80/tcp`

```bash
Rule added
Rule added (v6)
```

`student@vm01:~$ sudo ufw allow 443/tcp`

```bash
Rule added
Rule added (v6)
```

6. Permitir acesso de uma sub-rede específica

`student@vm01:~$ sudo ufw allow from 10.0.0.0/8 to any port 3306`

```bash
Rule added
```

> Isso permite conexões MySQL (porta 3306) apenas da rede privada 10.0.0.0/8. Note que esta regra cria apenas uma regra IPv4 (não v6) porque a origem é um bloco CIDR IPv4.

7. Negar uma porta específica

`student@vm01:~$ sudo ufw deny 8080/tcp`

```bash
Rule added
Rule added (v6)
```

8. Habilitar limitação de taxa no SSH

`student@vm01:~$ sudo ufw delete allow 22/tcp`

```bash
Rule deleted
Rule deleted (v6)
```

`student@vm01:~$ sudo ufw limit 22/tcp`

```bash
Rule added
Rule added (v6)
```

> A regra `limit` permite conexões mas bloqueia um endereço IP que tenta mais de 6 conexões em 30 segundos. Isso protege contra ataques de força bruta no SSH.

`student@vm01:~$ sudo ufw status verbose`

```bash
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
80/tcp                     ALLOW IN    Anywhere
443/tcp                    ALLOW IN    Anywhere
3306                       ALLOW IN    10.0.0.0/8
8080/tcp                   DENY IN     Anywhere
22/tcp                     LIMIT IN    Anywhere
80/tcp (v6)                ALLOW IN    Anywhere (v6)
443/tcp (v6)               ALLOW IN    Anywhere (v6)
8080/tcp (v6)              DENY IN     Anywhere (v6)
22/tcp (v6)                LIMIT IN    Anywhere (v6)
```

9. Visualizar todas as regras com números

`student@vm01:~$ sudo ufw status numbered`

```bash
Status: active

     To                         Action      From
     --                         ------      ----
[ 1] 80/tcp                     ALLOW IN    Anywhere
[ 2] 443/tcp                    ALLOW IN    Anywhere
[ 3] 3306                       ALLOW IN    10.0.0.0/8
[ 4] 8080/tcp                   DENY IN     Anywhere
[ 5] 22/tcp                     LIMIT IN    Anywhere
[ 6] 80/tcp (v6)                ALLOW IN    Anywhere (v6)
[ 7] 443/tcp (v6)               ALLOW IN    Anywhere (v6)
[ 8] 8080/tcp (v6)              DENY IN     Anywhere (v6)
[ 9] 22/tcp (v6)                LIMIT IN    Anywhere (v6)
```

10. Deletar uma regra por número

Para deletar a regra de negação da porta 8080 (regra número 4 no exemplo acima):

`student@vm01:~$ sudo ufw delete 4`

```bash
Deleting:
 deny 8080/tcp
Proceed with operation (y|n)? y
Rule deleted
```

> **Importante:** Após deletar uma regra, as regras restantes são renumeradas. Se você precisar deletar a regra IPv6 correspondente também, execute `sudo ufw status numbered` novamente para encontrar seu novo número, e então delete-a.

`student@vm01:~$ sudo ufw status numbered`

```bash
Status: active

     To                         Action      From
     --                         ------      ----
[ 1] 80/tcp                     ALLOW IN    Anywhere
[ 2] 443/tcp                    ALLOW IN    Anywhere
[ 3] 3306                       ALLOW IN    10.0.0.0/8
[ 4] 22/tcp                     LIMIT IN    Anywhere
[ 5] 80/tcp (v6)                ALLOW IN    Anywhere (v6)
[ 6] 443/tcp (v6)               ALLOW IN    Anywhere (v6)
[ 7] 8080/tcp (v6)              DENY IN     Anywhere (v6)
[ 8] 22/tcp (v6)                LIMIT IN    Anywhere (v6)
```

Agora delete a regra IPv6 da porta 8080 (agora regra 7):

`student@vm01:~$ sudo ufw delete 7`

```bash
Deleting:
 deny 8080/tcp
Proceed with operation (y|n)? y
Rule deleted (v6)
```

11. Habilitar e visualizar logs do UFW

`student@vm01:~$ sudo ufw logging on`

```bash
Logging enabled
```

`student@vm01:~$ grep -i ufw /var/log/syslog | tail -10`

```bash
Jan  1 12:30:00 vm01 kernel: [UFW BLOCK] IN=eth0 OUT= MAC=... SRC=192.168.1.100 DST=10.0.0.4 LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=12345 DF PROTO=TCP SPT=54321 DPT=8080 WINDOW=64240 RES=0x00 SYN URGP=0
```

> Se `/var/log/syslog` não existir (rsyslog não instalado), use `journalctl` em vez disso:

`student@vm01:~$ sudo journalctl --no-pager | grep -i ufw | tail -10`

> As entradas de log do UFW mostram `[UFW BLOCK]` ou `[UFW ALLOW]` junto com IP de origem/destino, porta e protocolo. Esses logs são inestimáveis para solução de problemas de conectividade.
