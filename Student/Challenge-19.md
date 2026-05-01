# Desafio 19 - Configuração de Firewall com UFW

[< Desafio Anterior](./Challenge-18.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-20.md)

## Descrição

Um firewall é sua primeira linha de defesa para qualquer servidor exposto a uma rede. O Ubuntu inclui o UFW (Uncomplicated Firewall), uma interface amigável para gerenciar regras do iptables. Este desafio ensina como controlar o acesso à rede do seu servidor.

**NOTA IMPORTANTE DE SEGURANÇA:** Antes de habilitar o firewall, SEMPRE permita o acesso SSH primeiro para evitar que você fique trancado para fora. Se você alterou a porta SSH no Desafio 13, use essa porta (ex.: 2222) em vez da porta padrão 22.

Observe também: Se você está executando em um ambiente de nuvem, o firewall do provedor de nuvem (Security Groups, NSGs, etc.) opera independentemente do UFW. Ambos devem permitir o tráfego para que ele chegue ao seu servidor. O UFW gerencia apenas o firewall no nível do host.

Se você completou o Desafio 14 (Docker), esteja ciente de que o Docker modifica as regras do iptables diretamente e pode contornar o UFW para portas publicadas por contêineres. Para este desafio, teste o UFW contra serviços do host (como nginx) em vez de contêineres Docker.

## Tarefas

1. Verifique o status atual do firewall: `sudo ufw status verbose`
2. Antes de habilitar, permita o acesso SSH (CRÍTICO — faça isso primeiro!):
   - Se estiver usando a porta SSH padrão: `sudo ufw allow 22/tcp`
   - Se você alterou a porta SSH no Desafio 13: `sudo ufw allow 2222/tcp`
3. Habilite o firewall: `sudo ufw enable`
4. Verifique o status novamente: `sudo ufw status verbose` — você deve ver o SSH permitido
5. Permita HTTP e HTTPS: `sudo ufw allow 80/tcp` e `sudo ufw allow 443/tcp`
6. Permita acesso de uma sub-rede específica (use sua rede local): `sudo ufw allow from 10.0.0.0/8 to any port 3306` (exemplo: MySQL apenas da rede interna)
7. Negue uma porta específica: `sudo ufw deny 8080/tcp`
8. Habilite limitação de taxa no SSH para proteger contra força bruta: Primeiro exclua a regra SSH existente e adicione uma com limite:

```bash
sudo ufw delete allow 22/tcp
sudo ufw limit 22/tcp
```

(Use a porta 2222 se essa for sua porta SSH)

9. Visualize todas as regras com números: `sudo ufw status numbered`
10. Exclua uma regra por número: `sudo ufw delete <número>` (exclua a regra de negação da porta 8080)
11. Visualize os logs do UFW: `sudo ufw logging on` depois verifique `sudo journalctl -u ufw --no-pager | tail -20` ou `grep -i ufw /var/log/syslog | tail -10`

## Critérios de Sucesso

1. O firewall está ativo e o acesso SSH está preservado
2. As portas HTTP e HTTPS estão abertas
3. Você consegue permitir acesso de sub-redes específicas
4. A limitação de taxa SSH está configurada
5. Você consegue adicionar e remover regras por número

## Recursos de Aprendizado

- [Documentação do UFW do Ubuntu](https://ubuntu.com/server/docs/firewalls)
- [Página man do UFW](https://manpages.ubuntu.com/manpages/noble/man8/ufw.8.html)
- [Fundamentos do UFW](https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands)

## Ponte para o Kubernetes

No Kubernetes, NetworkPolicies controlam o tráfego pod-a-pod, funcionando como um firewall no nível do cluster. Os conceitos são similares — regras de permissão/negação baseadas em portas e origem/destino — mas aplicadas a Pods e Namespaces em vez de endereços IP.