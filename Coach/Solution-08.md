# Desafio 08 - Scripting - Guia do Coach 

[< Solução Anterior](./Solution-07.md) - **[Início](./README.md)** - [Próxima Solução >](./Solution-09.md)

## Notas e Orientações
1. Crie um script que procure o nome da distribuição atual no arquivo `/etc/os-release` e imprima na tela

`student@vm01:~$ vim distribution.sh`

```bash
#!/bin/bash
distribution=`grep ^NAME /etc/os-release | cut -d= -f2`
echo "The current distribution is: $distribution"
```
`student@vm01:~$ chmod a+x distribution.sh`

`student@vm01:~$ ./distribution.sh`

```bash
The current distribution is: "Ubuntu"
```

2. Crie um script que leia os nomes de usuário do `/etc/passwd` e imprima aqueles com shell terminando em sh

`student@vm01:~$ vim users.sh`

```bash
#!/bin/bash
users=`grep sh$ /etc/passwd | cut -d: -f1`
echo "Users with login shell:"
echo $users
```
`student@vm01:~$ chmod a+x users.sh`

`student@vm01:~$ ./users.sh`

```bash
Users with login shell:
root student omsagent nxautomation anna mary peter rick"
```

3. Crie um script que some dois inteiros solicitados ao usuário e imprima o resultado

`student@vm01:~$ vim sum.sh`

```bash
#!/bin/bash
echo "Enter two numbers: "
read N1 N2
sum=$(( N1 + N2 ))
echo "The sum of $N1 and $N2 is $sum"
```
`student@vm01:~$ chmod a+x sum.sh`

`student@vm01:~$ ./sum.sh`

```bash
Enter two numbers:
2 3
The sum of 2 and 3 is 5
```