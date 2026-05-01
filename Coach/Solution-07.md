# Desafio 07 - Gerenciamento de grupos e usuários - Guia do Coach 

[< Solução Anterior](./Solution-06.md) - **[Home](./README.md)** - [Próxima Solução >](./Solution-08.md)

## Notas e Orientações
1. Crie os grupos: marketing, finance, apps e production

`student@vm01:~$ for name in marketing finance apps production; do sudo groupadd ${name}; done`

2. Crie os usuários abaixo com as seguintes características:

    1. login: anna, grupo principal: marketing
  
    `student@vm01:~$ sudo useradd -c "Anna" -d /home/anna -m -s /bin/bash -g marketing anna`
  
    2. login: mary, grupo principal: finance
  
    `student@vm01:~$ sudo useradd -c "Mary" -d /home/mary -m -s /bin/bash -g finance mary`
  
    3. login: peter, grupo principal: apps
  
    `student@vm01:~$ sudo useradd -c "Peter" -d /home/peter -m -s /bin/bash -g apps peter`
  
    4. login: rick, grupo principal: production
  
    `student@vm01:~$ sudo useradd -c "Rick" -d /home/rick -m -s /bin/bash -g production rick`
  
    Outra forma de criar:
    ```bash
    student@vm01:~$ for usr in anna:marketing mary:finance peter:apps rick:prouction; do
    login=$(echo $usr | cut -d: -f1)
    group=$(echo $usr | cut -d: -f2)
    sudo useradd -c "$login" -d /home/$login -m -s /bin/bash -g $group $login
    done  
    ```
  
3. Crie senhas para todos os usuários

`student@vm01:~$ sudo passwd anna`

`student@vm01:~$ sudo passwd mary`

`student@vm01:~$ sudo passwd peter`

`student@vm01:~$ sudo passwd rick`