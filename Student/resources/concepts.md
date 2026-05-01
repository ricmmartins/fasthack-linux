
# Conceitos básicos do Linux

## Todos os arquivos são sensíveis a maiúsculas e minúsculas

Arquivos no Linux são sensíveis a maiúsculas e minúsculas. Isso significa que MYLOG.txt é diferente de mylog.txt.

Este exemplo mostra a diferença entre dois arquivos, um com S maiúsculo, o outro com s minúsculo.

```bash
student@vm1:~/Linux$ ls summer.txt  Summer.txt
student@vm1:~/Linux$ cat summer.txt It is hot.
student@vm1:~/Linux$ cat Summer.txt It is very hot!
```

## Tudo é um arquivo

No Linux, tudo é considerado um arquivo. Isso inclui dispositivos de hardware, processos, diretórios, arquivos regulares, sockets, links e assim por diante. Além disso, o sistema de arquivos é geralmente dividido em blocos de dados e inodes. Com isso em mente, você pode pensar nos inodes como a base do sistema de arquivos do Linux. Para explicar de forma mais clara, um Inode é uma estrutura de dados que armazena metadados sobre cada arquivo no seu sistema. É uma estrutura de dados de arquivo que armazena informações sobre qualquer arquivo Linux, exceto seu nome e dados.

Informações contidas em um Inode:

* Tamanho do arquivo;
* Dispositivo no qual o arquivo está armazenado;
* IDs de usuário e grupo associados ao arquivo;
* Permissões necessárias para acessar o arquivo;
* Carimbos de data/hora de criação, leitura e escrita;
* Localização dos dados (mas não o caminho do arquivo).

Além disso, os Inodes também são independentes dos nomes de arquivo. Isso significa que você pode copiar um único arquivo, renomeá-lo e ainda assim tê-lo apontando para o mesmo Inode que o original.

## Descritores de arquivo, pipes e redirecionamentos

Esta seção explica como funcionam os recursos de direcionamento de entrada e saída do sistema GNU/Linux. 

Um comando sempre gera uma saída que pode ser incorporada por outro comando, que gera outra saída que pode ser incorporada por outro comando, e assim por diante até que a saída dos comandos apareça em um local específico (na tela ou dentro de um arquivo).


### Descritores de Arquivo

Abstração de uma identificação para acessar um arquivo. Quando um processo deseja manipular um arquivo, ele usará um número que é um descritor de arquivo que indica onde esse arquivo está e como acessá-lo.

Existem 3 descritores de arquivo que mostram como os arquivos podem ser acessados, são eles:

* **Entrada Padrão (stdin)**: A Entrada Padrão é um fluxo para entrada de texto, vinculado ao teclado. É chamado de **Descritor de Arquivo 0**.

* **Saída Padrão (stdout)**: A Saída Padrão é um fluxo para a saída normal de programas. Quando um programa é executado com sucesso, ele gera uma saída que é a Saída Padrão, que está vinculada ao terminal ou a uma janela de terminal. Toda saída gerada pelos comandos é escrita na Saída Padrão, que é chamada de **Descritor de Arquivo 1**.

* **Erro Padrão (stderr)**: O Erro Padrão também é um fluxo de saída de texto, mas usado para exibir mensagens de erro.
Quando seu comando falha, ele gera um erro que é exibido pela saída de Erro Padrão, vinculada ao terminal e é chamada de **Descritor de Arquivo 2**.

### Pipes 

O Pipe permite unir dois ou mais comandos executados em sequência.

Exemplo:

```bash
ls -l /etc | less 
```

Se mais de dois comandos são usados com redirecionamento, chamamos a operação resultante de **Pipeline**.

```bash
ls -l /etc | sort -r | less
```

### Redirecionamentos

O operador de redirecionamento `>` pode enviar a saída de um comando para um arquivo, ou ler de um arquivo.

* **Redirecionamento de Saída Padrão**

```bash
ls -i > inodes.txt
```
Saídas que são redirecionadas para um arquivo não são exibidas na saída padrão (tela ou terminal), precisamente porque foram redirecionadas para o arquivo, exceto erros padrão.

```bash
> = criar arquivos
>> = adicionar ao final do arquivo
```

* **Redirecionamento de Entrada Padrão**

O comando em vez de ler informações do teclado, lê de um arquivo. 

Redirecionar o arquivo para um comando

`cat < /etc/group > groups.txt` = O operador com sinal de menor `<` é um operador de redirecionamento de entrada, ou seja, o conteúdo do arquivo `/etc/groups/` será lido pelo comando `cat` e então será enviado através do operador de redirecionamento de saída `>` para o arquivo "groups.txt"

* **Redirecionamento de Erro Padrão**

Para redirecionar a mensagem de erro de um comando para um arquivo, é necessário informar o Descritor de Arquivo 2 antes do operador de redirecionamento `>`

Exemplo:

`ls -zz 2> error.txt`

### O comando tee

O comando "tee" permite enviar a saída de um comando para um arquivo e para a tela ao mesmo tempo.

Sintaxe:

```bash
tee [options] files
```

Opções:

```bash
-a = Adicionar ao arquivo em vez de sobrescrevê-lo
```

Exemplo:

```bash
ls -l | tee result.txt
```

Exemplo 2:

```bash
ls -i | tee result2.txt | less
```