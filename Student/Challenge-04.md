# Desafio 04 - Conteúdo de arquivos

[< Desafio Anterior](./Challenge-03.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-05.md)

## Descrição

Neste desafio vamos aprender sobre manipulação de conteúdo de arquivos e descobrir como contar linhas de arquivos, exibir linhas específicas de um arquivo e mais.

- Exiba as primeiras 10 linhas de `/etc/resolv.conf`
- Exiba as últimas 5 linhas de `/etc/crontab`
- Crie um arquivo chamado `count.log` com este conteúdo:

    One<br>
    Two<br>
    Three<br>
    Four<br>
    Five

- Use `cp` para fazer um backup deste arquivo para `count.bkp`
- Use `cat` para fazer um backup deste arquivo, salvando como `cat-count.log`
- Exiba o conteúdo de `cat-count.log`, com todas as linhas em ordem reversa
- Use `more` para exibir `/etc/selinux/semanage.conf`
- Use `ls` para encontrar o maior arquivo em `/var/log`

## Critérios de Sucesso

1. Mostre o conteúdo das primeiras 10 linhas de `/etc/resolv.conf`
2. Mostre as últimas 5 linhas de `/etc/crontab`
3. Valide se o conteúdo do arquivo `count.log` foi criado como esperado
4. Verifique se o arquivo `count.bkp` foi criado 
5. Verifique se o arquivo `cat-count.log` foi criado
6. Confirme se você consegue ver o conteúdo do arquivo `cat-count.log` em ordem reversa
7. Valide se você conseguiu ver o conteúdo do arquivo `/etc/selinux/semanage.conf` paginado
8. Verifique se você consegue ver o maior arquivo em `/var/log` no topo da lista

## Recursos de Aprendizado

- [The Shell](https://linuxjourney.com/lesson/the-shell)