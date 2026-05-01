# Desafio 09 - Discos, Partições e Sistemas de Arquivos

[< Desafio Anterior](./Challenge-08.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-10.md)

## Pré-requisitos

- Crie um disco de dados com o tamanho de 5GB
- Adicione o disco à máquina virtual

## Descrição

Neste desafio você trabalhará com discos e partições. Será uma oportunidade para aprender sobre sistemas de arquivos Linux e comandos como `fdisk`, `mkfs` e `mount`.

- Identifique o novo disco adicionado à máquina
- Edite a tabela de partição do disco:
    - Adicione uma nova partição com 500MB
    - Liste e identifique no sistema operacional a partição criada
    - Apague a partição
    - Verifique no sistema operacional que a partição foi removida
    - Adicione duas novas partições com tipo Linux nativo (83), uma com 500MB e outra com 100MB
    - Verifique no sistema operacional que as partições foram criadas
- Crie um sistema de arquivos em cada uma das partições criadas
- Crie um diretório para cada uma das partições dentro do diretório `/mnt`
- Monte cada uma das partições no respectivo diretório
- Verifique se as partições estão montadas corretamente no sistema operacional
- Escreva arquivos dentro de uma das partições
- Desmonte as partições
- Remova as partições existentes

## Critérios de Sucesso

1. Verifique se o disco foi adicionado à máquina virtual
2. Certifique-se de que as partições foram criadas conforme esperado
3. Valide em ambas as partições o sistema de arquivos criado
4. Certifique-se de que os respectivos diretórios foram criados dentro do diretório `mnt`
5. Certifique-se de que as partições estão corretamente montadas
6. Garanta que você consegue criar arquivos nas partições
7. Certifique-se de que desmontou as partições e removeu ambas corretamente

## Recursos de Aprendizado

- [Filesystem Hierarchy](https://linuxjourney.com/lesson/filesystem-hierarchy)
- [Dev Directory](https://linuxjourney.com/lesson/dev-directory)
- [How to partition a disk in Linux](https://opensource.com/article/18/6/how-partition-disk-linux)
- [How To – Linux List Disk Partitions Command](https://www.cyberciti.biz/faq/linux-list-disk-partitions-command/)
- [How To List Disk Partitions In Linux](https://ostechnix.com/how-to-list-disk-partitions-in-linux/)