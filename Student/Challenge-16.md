# Desafio 16 - systemd e Gerenciamento de Serviços

[< Desafio Anterior](./Challenge-15.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-17.md)

## Descrição

systemd é o sistema de inicialização e gerenciador de serviços para distribuições Linux modernas. Ele controla como os serviços iniciam, param e são gerenciados ao longo do ciclo de vida do sistema. Entender o systemd é crucial para qualquer administrador Linux — é assim que você gerencia tudo, desde servidores web até bancos de dados e aplicações personalizadas.

## Tarefas

1. Liste todos os serviços ativos: `systemctl list-units --type=service --state=active`
2. Verifique o status do serviço SSH: `systemctl status ssh`
3. Verifique se o nginx está instalado e em execução: `systemctl status nginx`. Se não estiver instalado, instale-o primeiro com `sudo apt install -y nginx`
4. Pare o serviço nginx: `sudo systemctl stop nginx` — depois verifique se ele parou
5. Inicie o nginx novamente: `sudo systemctl start nginx` — verifique se está em execução
6. Reinicie o nginx (parar+iniciar em um comando): `sudo systemctl restart nginx`
7. Desabilite o nginx de iniciar na inicialização: `sudo systemctl disable nginx` — verifique com `systemctl is-enabled nginx`
8. Reabilite o nginx na inicialização: `sudo systemctl enable nginx`
9. Visualize as últimas 20 linhas dos logs do nginx: `journalctl -u nginx --no-pager -n 20`
10. Visualize todos os logs da última hora: `journalctl --since "1 hour ago" --no-pager | tail -30`
11. Crie um serviço systemd personalizado: Crie um arquivo `/etc/systemd/system/hello.service` com este conteúdo:

```
[Unit]
Description=Hello World Service
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/echo "Hello from systemd!"
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

Depois recarregue o systemd com `sudo systemctl daemon-reload`, inicie o serviço e verifique seu status e logs.

## Critérios de Sucesso

1. Você consegue listar, iniciar, parar, reiniciar, habilitar e desabilitar serviços
2. Você consegue verificar o status e os logs de qualquer serviço
3. Você consegue filtrar logs do journal por serviço e tempo
4. Seu serviço personalizado hello.service executa com sucesso

## Recursos de Aprendizado

- [Documentação do systemd](https://www.freedesktop.org/software/systemd/man/latest/systemd.service.html)
- [Guia de serviços systemd do Ubuntu](https://ubuntu.com/server/docs/managing-services-with-systemd)
- [Manual do journalctl](https://www.freedesktop.org/software/systemd/man/latest/journalctl.html)
- [Como criar um serviço systemd](https://linuxhandbook.com/create-systemd-services/)

## Ponte para o Kubernetes

Componentes do Kubernetes como kubelet e containerd executam como serviços systemd. Ao solucionar problemas em um nó Kubernetes, `systemctl status kubelet` e `journalctl -u kubelet` são suas primeiras ferramentas de diagnóstico.