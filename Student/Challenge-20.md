# Desafio 20 - Solução de Problemas Linux (Projeto Final)

[< Desafio Anterior](./Challenge-19.md) - **[Início](../README.md)**

## Descrição

Este desafio final combina tudo o que você aprendeu. Você trabalhará em três cenários realistas de solução de problemas que testam sua capacidade de diagnosticar e corrigir problemas usando as ferramentas de todos os desafios anteriores. Cada cenário começa com um sintoma — seu trabalho é investigar, identificar a causa raiz e corrigi-la.

## Cenário A — "O Servidor Web Está Fora do Ar"

Sua equipe reporta que o servidor web está inacessível. Diagnostique e corrija o problema.

**Preparação** (execute estes comandos para criar o estado com problema):

```bash
sudo systemctl stop nginx
sudo ufw deny 80/tcp 2>/dev/null
```

**Tarefas:**

1. Verifique o sintoma: `curl -s -o /dev/null -w "%{http_code}" http://localhost:80` (deve falhar ou não retornar nada)
2. Verifique se o nginx está em execução: `systemctl status nginx`
3. Verifique se a porta 80 está em escuta: `sudo ss -tulnp | grep :80`
4. Inicie o nginx: `sudo systemctl start nginx`
5. Teste novamente — ainda bloqueado? Verifique o firewall: `sudo ufw status`
6. Permita a porta 80: `sudo ufw allow 80/tcp`
7. Verifique a correção: `curl -s -o /dev/null -w "%{http_code}" http://localhost:80` (deve retornar 200)

## Cenário B — "Alerta de Espaço em Disco"

O monitoramento reporta que a partição /tmp está enchendo. Investigue e faça a limpeza.

**Preparação:**

```bash
dd if=/dev/zero of=/tmp/bigfile bs=1M count=100 2>/dev/null
mkdir -p /tmp/oldlogs
for i in $(seq 1 50); do dd if=/dev/zero of=/tmp/oldlogs/app-$i.log bs=1M count=1 2>/dev/null; done
```

**Tarefas:**

1. Verifique o uso de disco: `df -h`
2. Descubra o que está consumindo espaço em /tmp: `du -sh /tmp/* 2>/dev/null | sort -rh | head -10`
3. Encontre arquivos maiores que 10MB em /tmp: `find /tmp -size +10M -exec ls -lh {} \; 2>/dev/null`
4. Encontre arquivos de log antigos (criados durante a preparação): `find /tmp/oldlogs -name "*.log" -type f | wc -l`
5. Faça a limpeza: Remova o arquivo grande e os logs antigos:

```bash
rm /tmp/bigfile
rm -rf /tmp/oldlogs
```

6. Verifique se o espaço em disco foi recuperado: `df -h`

## Cenário C — "Mistério do Alto Uso de CPU"

Um processo está consumindo CPU excessivamente. Encontre e pare-o.

**Preparação:**

```bash
nohup bash -c 'while true; do echo "busy" > /dev/null; done' &
```

**Tarefas:**

1. Verifique a carga do sistema: `uptime`
2. Identifique os maiores consumidores de CPU: `top -b -n 1 | head -20` ou `ps aux --sort=-%cpu | head -10`
3. Encontre o processo bash descontrolado e seu PID
4. Verifique o que o processo está fazendo: `cat /proc/<PID>/cmdline | tr '\0' ' '`
5. Encerre o processo: `kill <PID>`
6. Se não parar: `kill -9 <PID>`
7. Verifique se o uso de CPU voltou ao normal: `uptime` (a carga deve começar a diminuir)
8. Verifique também o uso de memória: `free -h`

## Critérios de Sucesso

1. **Cenário A:** O servidor web está em execução e acessível na porta 80
2. **Cenário B:** Identificou e removeu os arquivos grandes; espaço em disco recuperado
3. **Cenário C:** Encontrou e encerrou o processo descontrolado; carga de CPU está diminuindo

## Instruções de Reset

Se você precisar repetir qualquer cenário, reexecute os comandos de preparação correspondentes acima.

## Recursos de Aprendizado

- [Guia de solução de problemas Linux](https://www.brendangregg.com/linuxperf.html)
- [Documentação do systemctl](https://www.freedesktop.org/software/systemd/man/latest/systemctl.html)
- [Como encontrar arquivos grandes](https://linuxhandbook.com/find-large-files-linux/)
- [Gerenciamento de processos Linux](https://tldp.org/LDP/tlk/kernel/processes.html)

## Ponte para o Kubernetes

No Kubernetes, a solução de problemas segue padrões similares: `kubectl describe pod` é como `systemctl status`, `kubectl logs` é como `journalctl`, `kubectl top pod` é como `top`, e `kubectl exec` permite executar essas mesmas ferramentas Linux dentro dos contêineres. A mentalidade de diagnóstico é idêntica.