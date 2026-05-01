# Desafio 15 - Fundamentos de Rede

[< Desafio Anterior](./Challenge-14.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-16.md)

## Descrição

Redes são a espinha dorsal da infraestrutura moderna. Entender como o Linux gerencia interfaces de rede, roteamento e DNS é essencial para solução de problemas e gerenciamento de servidores. Este desafio apresenta as ferramentas essenciais de rede disponíveis em todo sistema Linux.

## Tarefas

1. Liste todas as interfaces de rede e seus endereços IP usando `ip addr show`
2. Exiba apenas os endereços IPv4 usando `ip -4 addr show`
3. Mostre o status da camada de enlace de todas as interfaces usando `ip link show`
4. Exiba a tabela de roteamento usando `ip route show`. Identifique o gateway padrão.
5. Verifique a configuração DNS usando `resolvectl status`. Também visualize `/etc/resolv.conf` e observe que pode mostrar um resolvedor stub (127.0.0.53) — os servidores DNS reais são gerenciados pelo systemd-resolved.
6. Instale utilitários DNS: `sudo apt install -y dnsutils` — depois resolva um domínio usando `dig google.com` e `nslookup google.com`
7. Instale o traceroute: `sudo apt install -y traceroute` — depois trace a rota até google.com
8. Teste a conectividade com google.com usando `ping -c 4 google.com`
9. Use `curl -I https://google.com` para visualizar os cabeçalhos de resposta HTTP
10. Mostre todas as portas TCP e UDP em escuta com `sudo ss -tulnp`. Identifique qual processo está usando a porta 22.

## Critérios de Sucesso

1. Você consegue exibir endereços IP de todas as interfaces de rede
2. Você consegue identificar o gateway padrão
3. A resolução DNS funciona com dig e nslookup
4. Você consegue rastrear rotas de rede
5. Você consegue identificar todas as portas em escuta e seus processos associados

## Recursos de Aprendizado

- [Folha de referência do comando ip](https://access.redhat.com/sites/default/files/attachments/rh_ip_command_cheatsheet_1214_jcs_print.pdf)
- [Comandos de rede Linux](https://www.redhat.com/en/blog/linux-network-commands)
- [Documentação de rede do Ubuntu](https://ubuntu.com/server/docs/about-networking)
- [systemd-resolved](https://www.freedesktop.org/software/systemd/man/latest/systemd-resolved.service.html)

## Ponte para o Kubernetes

No Kubernetes, redes são fundamentais — Pods se comunicam através de redes virtuais, Services fornecem endpoints estáveis e o CoreDNS gerencia a resolução DNS do cluster. Dominar as ferramentas de rede do Linux ajuda você a depurar problemas de rede do Kubernetes com `kubectl exec` dentro dos pods.