# Desafio 18 - Agendamento de Tarefas com Cron

[< Desafio Anterior](./Challenge-17.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-19.md)

## Descrição

Automatizar tarefas repetitivas é uma habilidade essencial para qualquer administrador de sistemas. O Linux oferece o cron, um agendador de tarefas baseado em tempo que executa comandos em intervalos especificados. De limpeza de logs a backups de banco de dados e verificações de saúde, o cron é o motor da automação Linux.

## Tarefas

1. Verifique se o cron está em execução: `systemctl status cron`
2. Visualize o crontab do usuário atual: `crontab -l` (deve mostrar "no crontab for student" se estiver vazio)
3. Entenda a sintaxe do cron — os cinco campos: `minuto hora dia-do-mês mês dia-da-semana`
   Exemplo: `30 2 * * *` = "Todo dia às 2:30 AM"
4. Crie uma tarefa agendada simples usando uma abordagem baseada em arquivo:

```bash
echo '*/5 * * * * echo "Cron is alive at $(date)" >> /tmp/cron-test.log' > /tmp/mycron
crontab /tmp/mycron
crontab -l
```

5. Aguarde 5 minutos e verifique se o cron job foi executado: `cat /tmp/cron-test.log`
6. Crie um script de limpeza e agende-o:

```bash
cat > /tmp/cleanup.sh << 'EOF'
#!/bin/bash
find /tmp -name "*.log" -mtime +7 -delete 2>/dev/null
echo "Cleanup ran at $(date)" >> /var/log/cleanup.log
EOF
chmod +x /tmp/cleanup.sh
```

Depois adicione-o ao cron para executar diariamente à meia-noite:

```bash
echo '0 0 * * * /tmp/cleanup.sh' >> /tmp/mycron
crontab /tmp/mycron
```

7. Visualize os cron jobs do sistema: `ls -la /etc/cron.d/ /etc/cron.daily/ /etc/cron.hourly/`
8. Instale e use `at` para uma tarefa única:

```bash
sudo apt install -y at
echo "echo 'One-time task ran at $(date)' >> /tmp/at-test.log" | at now + 1 minute
atq
```

9. Após o job `at` executar, verifique: `cat /tmp/at-test.log`
10. Limpe — remova seu crontab: `crontab -r`

## Critérios de Sucesso

1. Você consegue criar, listar e remover cron jobs
2. Sua tarefa agendada executa no intervalo esperado
3. Você entende a sintaxe de cinco campos do cron
4. Você consegue agendar tarefas únicas com `at`
5. Você sabe onde os cron jobs do sistema ficam armazenados

## Recursos de Aprendizado

- [Página man do crontab](https://man7.org/linux/man-pages/man5/crontab.5.html)
- [Crontab Guru — editor de expressões cron](https://crontab.guru/)
- [Guia de cron do Ubuntu](https://help.ubuntu.com/community/CronHowto)
- [Comando at](https://man7.org/linux/man-pages/man1/at.1.html)

## Ponte para o Kubernetes

O Kubernetes possui um recurso CronJob que funciona como o cron do Linux — mesma sintaxe de agendamento de cinco campos. Se você consegue escrever uma entrada no crontab, você consegue escrever uma especificação de CronJob do Kubernetes. A diferença principal é que CronJobs do Kubernetes executam em Pods em vez de diretamente no host.