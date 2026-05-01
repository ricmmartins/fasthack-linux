# Hackathon - Linux FUNdamentals

## Introdução

Este é um recurso de aprendizado criado para ajudar pessoas interessadas a adquirir habilidades em Linux e compreender conceitos básicos de linha de comando usando o Azure para construir e aprender. Porém, não se restringe ao uso do Azure e você pode executar este hackathon em qualquer máquina virtual com Ubuntu Linux.

<img align="right" src="./Student/resources/images/linuxpenguin.png" width="250"/>

> Nota: Este Hackathon foi incorporado ao Microsoft What The Hack, como o 1º "Hackathon" de Linux pela Microsoft! Saiba mais em [http://aka.ms/wth](http://aka.ms/wth)

## História do Linux

Linux é uma família de sistemas operacionais livres e de código aberto baseados no kernel Linux. Sistemas operacionais baseados em Linux são conhecidos como distribuições Linux ou distros. Exemplos incluem Debian, Ubuntu, Fedora, CentOS, Gentoo, Arch Linux e muitos outros.

O kernel Linux está em desenvolvimento ativo desde 1991, e provou ser extremamente versátil e adaptável. Você pode encontrar computadores que executam Linux em uma grande variedade de contextos ao redor do mundo, desde servidores web até telefones celulares. Hoje, 90% de toda a infraestrutura em nuvem e 74% dos smartphones do mundo são alimentados pelo Linux.

Para ler mais sobre a História do Linux, Distribuições Linux e Kernel Linux, [clique aqui](./Student/resources/linux-history.md).

## Objetivos de Aprendizado

Neste hack você será desafiado com algumas tarefas comuns de um cenário real de administração Linux, como:

1. Criar uma Máquina Virtual Linux no Azure
2. Manipular arquivos e diretórios
3. Manipular conteúdos de arquivos
4. Trabalhar com permissões padrão do Linux
5. Coletar informações sobre processos Linux em seu ambiente
6. Gerenciamento de usuários e grupos
7. Scripts básicos em shell
8. Trabalhar com discos, partições e gerenciador de volumes lógicos
9. Gerenciamento de pacotes Linux
10. Implementar um servidor web básico

## Desafios

Com exceção do desafio 01, que tem como resultado uma Máquina Virtual Linux necessária para todos os outros desafios, cada desafio pode ser feito separadamente e eles não são interdependentes. O nível de complexidade aumenta de acordo com o número respectivo de cada um.

* Desafio 01: **[Criar uma Máquina Virtual Linux](Student/Challenge-01.md)** - Uma máquina virtual Linux é o pré-requisito para os desafios, então crie uma nova VM Ubuntu Linux
* Desafio 02: **[Manipulando Diretórios](Student/Challenge-02.md)** - Aprenda a realizar operações comuns com diretórios, como exibir seu diretório atual e listar o conteúdo de diretórios.
* Desafio 03: **[Manipulando Arquivos](Student/Challenge-03.md)** - Aprenda comandos básicos sobre manipulação de arquivos, como criar, renomear, encontrar e remover arquivos.
* Desafio 04: **[Conteúdo de Arquivos](Student/Challenge-04.md)** - Aprenda sobre manipulação de conteúdo de arquivos e descubra como contar linhas, exibir linhas específicas de um arquivo e mais.
* Desafio 05: **[Permissões Padrão de Arquivos](Student/Challenge-05.md)** - Aprenda sobre as permissões padrão de arquivos Linux e entenda como trabalhar com permissões em um ambiente Linux.
* Desafio 06: **[Gerenciamento de Processos](Student/Challenge-06.md)** - Seus objetivos envolverão gerenciamento básico de processos, como verificar processos em execução e identificar IDs de processos.
* Desafio 07: **[Gerenciamento de Grupos e Usuários](Student/Challenge-07.md)** - Neste desafio você aprenderá sobre a criação de usuários e grupos em um ambiente Linux.
* Desafio 08: **[Scripting](Student/Challenge-08.md)** - Aprenda conceitos básicos de scripts em shell e o uso de comandos como echo, cut, read e grep.
* Desafio 09: **[Discos, Partições e Sistemas de Arquivos](Student/Challenge-09.md)** - Você trabalhará com discos e partições e aprenderá sobre sistemas de arquivos Linux e comandos como fdisk, mkfs e mount.
* Desafio 10: **[Gerenciador de Volumes Lógicos](Student/Challenge-10.md)** - Descubra sobre o Gerenciador de Volumes Lógicos no Linux e como usar comandos como pvcreate, vgcreate, lvcreate e mais.
* Desafio 11: **[Gerenciamento de Pacotes](Student/Challenge-11.md)** - Aprenda sobre gerenciamento de pacotes e atividades comuns como atualizar listas de distribuição de pacotes, instalar e desinstalar pacotes.
* Desafio 12: **[Configurando um Servidor Web](Student/Challenge-12.md)** - Neste desafio vamos configurar um servidor web e implantar uma aplicação PHP simples. O uso de SSL pode ser um diferencial.
* Desafio 13: **[Protegendo um Servidor](Student/Challenge-13.md)** - Neste desafio vamos descobrir como usar o Fail2Ban para proteger serviços em um ambiente Linux.
* Desafio 14: **[Executando Containers](Student/Challenge-14.md)** - Seu objetivo neste desafio será implantar um container Nginx e acessá-lo. Se quiser ir mais a fundo, há outra opção para implantar uma aplicação PHP simples.

## Pré-requisitos

- Para executar este hackathon no Azure e utilizar o Azure Cloud Shell, você precisará de uma assinatura Azure com acesso de contribuidor para o Desafio 01 ou acesso de contribuidor a uma Máquina Virtual Azure pré-criada para todos os outros desafios. Para executar este hackathon em qualquer outro provedor de nuvem ou localmente, você só precisa de uma máquina virtual executando Ubuntu Linux.
- Acesso a um terminal. Os termos "terminal", "shell" e "interface de linha de comando" são frequentemente usados de forma intercambiável, mas existem diferenças sutis entre eles:
  * Um terminal é um ambiente de entrada e saída que apresenta uma janela somente texto executando um shell.
  * Um shell é um programa que expõe o sistema operacional do computador a um usuário ou programa. Em sistemas Linux, o shell apresentado em um terminal é um interpretador de linha de comando.
  * Uma interface de linha de comando é uma interface de usuário (gerenciada por um programa interpretador de linha de comando) que processa comandos para um programa de computador e exibe os resultados.

  Quando alguém se refere a um desses três termos no contexto do Linux, geralmente significa um ambiente de terminal onde você pode executar comandos e ver os resultados impressos no terminal.

  Tornar-se um especialista em Linux requer que você esteja confortável usando um terminal. Qualquer tarefa administrativa, incluindo manipulação de arquivos, instalação de pacotes e gerenciamento de usuários, pode ser realizada através do terminal. O terminal é interativo: você especifica comandos para executar e o terminal exibe os resultados desses comandos. Para executar qualquer comando, você digita no prompt e pressiona ENTER.

  Para nossas atividades, é recomendado usar o [Azure Cloud Shell](http://shell.azure.com/).

- Existem alguns conceitos básicos que seria bom conhecer. Se quiser dar uma olhada, eles estão [listados aqui](./Student/resources/concepts.md).
- Conceitos sobre o Linux Filesystem Hierarchy Standard (FHS) são recomendados, então você pode obter mais detalhes [aqui](./Student/resources/fhs.md).
- Em relação aos comandos Linux, apenas como referência, [aqui está](./Student/resources/commands.md) um bom guia rápido.
- As páginas man do Linux são suas melhores amigas. Certifique-se de usá-las da melhor forma possível.

## Recursos de Aprendizado

* [Linux Journey](https://linuxjourney.com/)
* [Linux Upskill Challenge](https://linuxupskillchallenge.org/)
* [Guia para Iniciantes em Linux - Tecmint](https://www.tecmint.com/free-online-linux-learning-guide-for-beginners/)
* [Preparação para Linux Foundation Certified System Administrator](https://github.com/Bes0n/LFCS)
* [Notas do Linux Foundation Certified System Administrator (LFCS)](https://github.com/simonesavi/lfcs)
* [The Linux Documentation Project](https://tldp.org/)
* [Introdução ao Linux - do TLDP](https://tldp.org/LDP/intro-linux/intro-linux.pdf)
* [Notas de Comandos Linux para Profissionais](https://goalkicker.com/LinuxBook/LinuxNotesForProfessionals.pdf)
* [Introdução ao Linux - Curso gratuito da Linux Foundation](https://training.linuxfoundation.org/training/introduction-to-linux/)

## Guia do Coach

No diretório [coach](./Coach/) estão as diretrizes caso você esteja executando o Hackathon em um evento e seja um coach, bem como as soluções para os desafios propostos. Se você está fazendo o Hackathon como estudante, não se engane olhando as soluções durante o hack! Vá aprender algo. :)

## Contribuições

Contribuições na forma de correções de erros, solicitações de funcionalidades e PRs são sempre bem-vindas. Por favor, siga estes passos antes de enviar um PR:

* Crie uma issue descrevendo o erro ou solicitação de funcionalidade.
* Clone o repositório e crie uma branch de tópico.
* Faça as alterações, adicionando novos testes para novas funcionalidades.
* Envie um PR.

## Mostre seu apoio

Dê uma ⭐️ se este conteúdo te ajudou!