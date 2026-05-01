# Desafio 15 - Fundamentos de Rede - Guia do Coach
[< Solução Anterior](./Solution-14.md) - **[Início](./README.md)** - [Próxima Solução >](./Solution-16.md)

## Notas e Orientações

1. Listar todas as interfaces de rede e seus endereços IP

`student@vm01:~$ ip addr show`

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    link/ether 00:0d:3a:xx:xx:xx brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.4/24 metric 100 brd 10.0.0.255 scope global eth0
       valid_lft forever preferred_lft forever
    inet6 fe80::20d:3aff:fexx:xxxx/64 scope link
       valid_lft forever preferred_lft forever
```

> **Nota:** O nome da interface pode variar — VMs em nuvem normalmente usam `eth0`, enquanto instalações bare-metal ou desktop podem mostrar `ens33`, `enp0s3`, ou nomes similares seguindo a convenção de nomenclatura previsível de interfaces de rede.

2. Exibir apenas endereços IPv4

`student@vm01:~$ ip -4 addr show`

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
    inet 10.0.0.4/24 metric 100 brd 10.0.0.255 scope global eth0
       valid_lft forever preferred_lft forever
```

3. Mostrar o status da camada de enlace de todas as interfaces

`student@vm01:~$ ip link show`

```bash
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 00:0d:3a:xx:xx:xx brd ff:ff:ff:ff:ff:ff
```

> Procure por `state UP` ou `state DOWN` para determinar se uma interface está ativa.

4. Exibir a tabela de roteamento e identificar o gateway padrão

`student@vm01:~$ ip route show`

```bash
default via 10.0.0.1 dev eth0 proto dhcp src 10.0.0.4 metric 100
10.0.0.0/24 dev eth0 proto kernel scope link src 10.0.0.4 metric 100
168.63.129.16 via 10.0.0.1 dev eth0 proto dhcp src 10.0.0.4 metric 100
169.254.169.254 via 10.0.0.1 dev eth0 proto dhcp src 10.0.0.4 metric 100
```

> O gateway padrão é o endereço IP na linha que começa com `default via` — neste exemplo, `10.0.0.1`.

5. Verificar a configuração de DNS

`student@vm01:~$ resolvectl status`

```bash
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (eth0)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 168.63.129.16
       DNS Servers: 168.63.129.16
```

`student@vm01:~$ cat /etc/resolv.conf`

```bash
# This is /run/systemd/resolve/stub-resolv.conf managed by man:systemd-resolved(8).
nameserver 127.0.0.53
options edns0 trust-ad
search example.com
```

> O endereço `127.0.0.53` é o listener stub do systemd-resolved. Os servidores DNS upstream reais são mostrados pelo `resolvectl status` — neste caso `168.63.129.16`. Este é o comportamento normal no Ubuntu 24.04.

6. Instalar utilitários DNS e resolver um domínio

`student@vm01:~$ sudo apt install -y dnsutils`

`student@vm01:~$ dig google.com`

```bash
; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12345
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             300     IN      A       142.250.80.46

;; Query time: 5 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Mon Jan 01 12:00:00 UTC 2025
;; MSG SIZE  rcvd: 55
```

`student@vm01:~$ nslookup google.com`

```bash
Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
Name:   google.com
Address: 142.250.80.46
Name:   google.com
Address: 2607:f8b0:4004:800::200e
```

7. Instalar traceroute e rastrear a rota

`student@vm01:~$ sudo apt install -y traceroute`

`student@vm01:~$ traceroute google.com`

```bash
traceroute to google.com (142.250.80.46), 30 hops max, 60 byte packets
 1  10.0.0.1 (10.0.0.1)  0.548 ms  0.527 ms  0.516 ms
 2  * * *
 3  * * *
 4  108.170.245.65 (108.170.245.65)  1.234 ms  1.222 ms  1.211 ms
 5  142.250.80.46 (142.250.80.46)  1.456 ms  1.445 ms  1.434 ms
```

> Alguns saltos podem mostrar `* * *` — isso significa que esses roteadores estão configurados para não responder a sondas de traceroute. Isso é normal.

8. Testar conectividade com ping

`student@vm01:~$ ping -c 4 google.com`

```bash
PING google.com (142.250.80.46) 56(84) bytes of data.
64 bytes from lax17s62-in-f14.1e100.net (142.250.80.46): icmp_seq=1 ttl=118 time=1.23 ms
64 bytes from lax17s62-in-f14.1e100.net (142.250.80.46): icmp_seq=2 ttl=118 time=1.19 ms
64 bytes from lax17s62-in-f14.1e100.net (142.250.80.46): icmp_seq=3 ttl=118 time=1.21 ms
64 bytes from lax17s62-in-f14.1e100.net (142.250.80.46): icmp_seq=4 ttl=118 time=1.20 ms

--- google.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3004ms
rtt min/avg/max/mdev = 1.190/1.207/1.230/0.014 ms
```

9. Visualizar cabeçalhos de resposta HTTP com curl

`student@vm01:~$ curl -I https://google.com`

```bash
HTTP/2 301
location: https://www.google.com/
content-type: text/html; charset=UTF-8
content-security-policy-report-only: object-src 'none';base-uri 'self';script-src 'nonce-randomstring' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
date: Mon, 01 Jan 2025 12:00:00 GMT
expires: Wed, 31 Jan 2025 12:00:00 GMT
cache-control: public, max-age=2592000
server: gws
content-length: 220
x-xss-protection: 0
x-frame-options: SAMEORIGIN
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000
```

> A resposta `HTTP/2 301` é um redirecionamento de `google.com` para `www.google.com`. Este é o comportamento esperado.

10. Mostrar todas as portas TCP e UDP em escuta

`student@vm01:~$ sudo ss -tulnp`

```bash
Netid  State   Recv-Q  Send-Q   Local Address:Port   Peer Address:Port  Process
udp    UNCONN  0       0        127.0.0.53%lo:53     0.0.0.0:*          users:(("systemd-resolve",pid=610,fd=13))
tcp    LISTEN  0       4096     127.0.0.53%lo:53     0.0.0.0:*          users:(("systemd-resolve",pid=610,fd=14))
tcp    LISTEN  0       128            0.0.0.0:22     0.0.0.0:*          users:(("sshd",pid=750,fd=3))
tcp    LISTEN  0       128               [::]:22        [::]:*          users:(("sshd",pid=750,fd=4))
```

> O processo `sshd` está escutando na porta 22 (tanto IPv4 quanto IPv6). O processo `systemd-resolve` escuta na porta 53 para resolução DNS local. Os flags significam: `-t` TCP, `-u` UDP, `-l` em escuta, `-n` numérico (sem resolução de nomes), `-p` mostrar processo.
