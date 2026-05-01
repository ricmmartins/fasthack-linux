# What The Hack - Fundamentos do Linux - Guia do Coach

## Introdução
Bem-vindo ao guia do coach para o Hackathon de Fundamentos do Linux. Aqui você encontrará links para orientações específicas para coaches em cada um dos desafios.

> **NOTA:** Se você é um participante do Hackathon, este é o guia de respostas. Não trapaceie olhando estas respostas durante o hack! Vá aprender algo. :)

## Guias do Coach
* Desafio 01: **[Criar uma Máquina Virtual Linux](../Coach/Solution-01.md)**
 - Uma máquina virtual Linux é o pré-requisito para os desafios, então crie uma nova VM Ubuntu Linux
* Desafio 02: **[Manipulando Diretórios](../Coach/Solution-02.md)**
 - Aprenda como realizar operações comuns com diretórios, como exibir seu diretório atual e listar o conteúdo de diretórios.
* Desafio 03: **[Manipulando Arquivos](../Coach/Solution-03.md)**
 - Aprenda comandos básicos sobre manipulação de arquivos, como criar, renomear, localizar e remover arquivos.
* Desafio 04: **[Conteúdo de Arquivos](../Coach/Solution-04.md)**
 - Aprenda sobre manipulação de conteúdo de arquivos e descubra como contar linhas de um arquivo, exibir linhas específicas de um arquivo e muito mais.
* Desafio 05: **[Permissões Padrão de Arquivos](../Coach/Solution-05.md)**
 - Aprenda sobre as permissões padrão de arquivos no Linux e entenda como trabalhar com permissionamento de arquivos em um ambiente Linux.
* Desafio 06: **[Gerenciamento de Processos](../Coach/Solution-06.md)**
 - Seus objetivos envolverão o gerenciamento básico de processos, como verificar processos em execução e identificar IDs de processos.
* Desafio 07: **[Gerenciamento de Grupos e Usuários](../Coach/Solution-07.md)**
 - Neste desafio você aprenderá sobre a criação de usuários e grupos em um ambiente Linux.
* Desafio 08: **[Scripting](../Coach/Solution-08.md)**
 - Aprenda noções básicas sobre shell scripting e o uso de alguns comandos como echo, cut, read e grep.
* Desafio 09: **[Discos, Partições e Sistemas de Arquivos](../Coach/Solution-09.md)**
 - Você trabalhará com discos e partições e aprenderá sobre sistemas de arquivos Linux e comandos como fdisk, mkfs e mount.
* Desafio 10: **[Gerenciador de Volumes Lógicos](../Coach/Solution-10.md)**
 - Descubra sobre o Gerenciador de Volumes Lógicos no Linux e como usar comandos como pvcreate, vgcreate, lvrcreate e muito mais.
* Desafio 11: **[Gerenciamento de Pacotes](../Coach/Solution-11.md)**
 - Aprenda sobre gerenciamento de pacotes e atividades comuns como atualizar listas de distribuição de pacotes, instalar e desinstalar pacotes.
* Desafio 12: **[Configurando um Servidor Web](../Coach/Solution-12.md)**
 - Neste desafio vamos configurar um servidor web e implantar uma aplicação PHP simples nele. O uso de SSL seria um diferencial.
* Desafio 13: **[Protegendo um Servidor](../Coach/Solution-13.md)**
- Neste desafio vamos descobrir como usar o Fail2Ban para proteger serviços em um ambiente Linux.
* Desafio 14: **[Executando Contêineres](../Coach/Solution-14.md)**
- Seu objetivo neste desafio será criar uma imagem de contêiner a partir de uma aplicação de exemplo e fazê-la funcionar usando Docker.

## Pré-requisitos do Coach

Este hack possui pré-requisitos que o coach é responsável por entender e/ou configurar ANTES de sediar um evento.

O guia cobre os passos comuns de preparação que um coach precisa realizar antes do evento.

### Recursos do Estudante

Antes do hack, é responsabilidade do Coach garantir que os estudantes possam acessar o conteúdo da pasta `./Student/Resources`.

## Requisitos do Azure

Este hack requer que os estudantes tenham acesso a uma assinatura do Azure onde possam criar e consumir recursos do Azure. Estes requisitos do Azure devem ser compartilhados com uma parte interessada na organização que fornecerá a(s) assinatura(s) do Azure que serão utilizadas pelos estudantes.

- Para o Desafio 01, será necessária uma assinatura do Azure com acesso de contribuidor.
- Para todos os outros desafios, será necessário pelo menos acesso de contribuidor a uma máquina virtual Ubuntu Linux 20.04 pré-criada.
- Para o desafio avançado opcional do Desafio 12, estes são os requisitos:
- Um IP público associado à máquina virtual
- Acesso ao IP público da máquina virtual
- Acesso ao Domínio do Azure App Service para obter um domínio ou acesso ao gerenciamento de DNS de um domínio existente

## Conteúdo do Repositório

- `./Coach`
  - Guia do Coach e arquivos relacionados
- `./Coach/Solutions`
  - Arquivos de solução com exemplos completos de respostas para cada desafio
- `./Student`
  - Guia de Desafios do Estudante
- `./Student/Resources`
  - Arquivos de recursos, código de exemplo, scripts, etc. destinados a serem fornecidos aos estudantes. (Devem ser empacotados pelo coach e fornecidos aos estudantes no início do evento)

