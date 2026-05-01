# Desafio 17 - Processamento de Texto com sed, awk e Pipes

[< Desafio Anterior](./Challenge-16.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-18.md)

## Descrição

O Linux se destaca no processamento de texto. A capacidade de encadear comandos com pipes e usar ferramentas poderosas como sed e awk é o que torna a administração Linux eficiente. Essas habilidades são essenciais para analisar logs, transformar arquivos de configuração e automatizar a extração de dados.

## Tarefas

1. Crie um arquivo de log de exemplo para os exercícios:

```bash
sudo cp /var/log/syslog /tmp/practice.log 2>/dev/null || sudo journalctl --no-pager -n 200 > /tmp/practice.log
```

2. Use `cut` para extrair os três primeiros campos (data/hora/hostname) de cada linha: `cut -d' ' -f1-3 /tmp/practice.log | head -10`
3. Use `sort` e `uniq -c` para encontrar as 10 palavras mais frequentes na coluna 5 do log: `awk '{print $5}' /tmp/practice.log | sort | uniq -c | sort -rn | head -10`
4. Use `tr` para converter as primeiras 5 linhas do log para maiúsculas: `head -5 /tmp/practice.log | tr '[:lower:]' '[:upper:]'`
5. Use `sed` para substituir todas as ocorrências do seu hostname por "REDACTED" no log e salve a saída: `sed 's/yourhostname/REDACTED/g' /tmp/practice.log > /tmp/redacted.log`
6. Use `sed` para deletar todas as linhas em branco de um arquivo: `sed '/^$/d' /tmp/practice.log`
7. Use `awk` para imprimir apenas linhas com mais de 80 caracteres: `awk 'length > 80' /tmp/practice.log | head -10`
8. Use `awk` para somar uma coluna numérica. Primeiro crie um arquivo de teste:

```bash
echo -e "apples 5\nbananas 12\noranges 3\ngrapes 8" > /tmp/fruits.txt
awk '{sum += $2} END {print "Total:", sum}' /tmp/fruits.txt
```

9. Construa um pipeline para encontrar endereços IP únicos em um arquivo de log (se existirem): `grep -oE '[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+' /tmp/practice.log | sort -u`
10. Conte quantos arquivos .conf existem em /etc: `find /etc -name "*.conf" 2>/dev/null | wc -l`

## Critérios de Sucesso

1. Você consegue extrair colunas específicas de texto estruturado
2. Você consegue encontrar os itens mais frequentes em um conjunto de dados
3. Você consegue realizar operações de busca e substituição com sed
4. Você consegue filtrar e agregar dados com awk
5. Você consegue construir pipelines de múltiplos estágios combinando várias ferramentas

## Recursos de Aprendizado

- [Manual do GNU sed](https://www.gnu.org/software/sed/manual/sed.html)
- [Manual do GNU awk](https://www.gnu.org/software/gawk/manual/gawk.html)
- [Comandos de processamento de texto Linux](https://tldp.org/LDP/abs/html/textproc.html)
- [Tutorial de pipe e redirecionamento](https://ryanstutorials.net/linuxtutorial/piping.php)

## Ponte para o Kubernetes

No Kubernetes, você frequentemente encadeará a saída do kubectl através de ferramentas de processamento de texto — por exemplo, `kubectl get pods | awk '{print $1, $3}'` para extrair nomes e status dos pods, ou `kubectl logs <pod> | grep ERROR` para filtrar logs de aplicações.