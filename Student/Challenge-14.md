# Desafio 14 - Executando Containers

[< Desafio Anterior](./Challenge-13.md) - **[Início](./README.md)**

## Descrição

Containers são unidades executáveis de software nas quais o código da aplicação é empacotado, junto com suas bibliotecas e dependências, de maneiras comuns para que possa ser executado em qualquer lugar, seja em desktop, TI tradicional ou na nuvem.

Para isso, os containers aproveitam uma forma de virtualização do sistema operacional (SO) na qual recursos do SO (no caso do kernel Linux, especificamente os namespaces e primitivas de cgroups) são utilizados tanto para isolar processos quanto para controlar a quantidade de CPU, memória e disco que esses processos podem acessar.

Containers são pequenos, rápidos e portáteis porque, diferentemente de uma máquina virtual, os containers não precisam incluir um SO convidado em cada instância e podem, em vez disso, simplesmente aproveitar os recursos e funcionalidades do SO hospedeiro.

Containers apareceram pela primeira vez décadas atrás com versões como FreeBSD Jails e AIX Workload Partitions, mas a maioria dos desenvolvedores modernos lembra de 2013 como o início da era moderna dos containers com a introdução do [Docker](https://www.docker.com/).

Docker é uma plataforma para desenvolver, distribuir e executar aplicações. Vamos detalhar essa afirmação. O Docker permite que os usuários construam novas imagens de container, enviem essas imagens para o Docker Hub, e também baixem essas imagens do Docker Hub. O Docker Hub funciona como uma biblioteca de imagens de container, e hospeda imagens de container que os usuários constroem. Existem também algumas novas alternativas ao Docker como o [Podman](https://podman.io/).

Podman é um engine de container sem daemon para desenvolver, gerenciar e executar OCI Containers (Open Containers Initiative) no seu sistema Linux. Ao contrário do Docker, o Podman não requer um processo daemon para iniciar e gerenciar containers. Esta é uma diferença importante entre os dois projetos.

O Podman busca melhorar algumas das desvantagens do Docker. Por exemplo, o Podman não requer um daemon rodando como root. Na verdade, containers do Podman rodam com as mesmas permissões do usuário que os iniciou. Isso resolve uma preocupação significativa de segurança, embora você ainda possa executar containers com permissões de root se realmente quiser.

O Podman busca ser um substituto direto do Docker no que diz respeito à CLI. Os desenvolvedores afirmam que a maioria dos usuários pode simplesmente usar alias docker=podman e continuar executando os mesmos comandos familiares. O formato de imagem de container também é totalmente compatível entre Docker e Podman, então containers existentes construídos em Dockerfiles funcionarão com o Podman.

Outra diferença chave é que, diferentemente do Docker, o Podman não é capaz de construir imagens de container (a ferramenta [Buildah](https://buildah.io/) é usada para isso). Isso mostra que o Podman não foi construído para ser monolítico.

Ele lida com a execução de containers (entre outras coisas), mas não com a construção deles. O objetivo aqui é ter um conjunto de padrões de container que qualquer aplicação possa ser desenvolvida para suportar, em vez de depender de uma única aplicação monolítica como o Docker para realizar todas as tarefas.

Este desafio permitirá que você tenha seu primeiro contato com containers. Você irá:

- Instalar o runtime do Docker
- Executar um container Nginx
- Acessar o website padrão na sua máquina virtual

Se você quiser ir além com um desafio avançado, tente este:

- Baixe esta aplicação de exemplo [daqui](/Student/resources/simple-php-app.tar.gz) para o seu diretório home
- Crie um Dockerfile para instalar o Nginx, PHP, e executar esta aplicação PHP.
- Construa a imagem
- Teste a execução do container
- Publique a imagem no Docker Hub

## Critérios de Sucesso

1. Certifique-se de que o runtime do Docker foi instalado com sucesso
2. Garanta que seu container Nginx está rodando corretamente
3. Acesse o website padrão do Nginx através do IP público da sua máquina virtual

Se você decidiu aceitar o desafio avançado:

1. Garanta que a aplicação de exemplo foi baixada na máquina virtual
6. Tenha a aplicação rodando via container e acessível pelo navegador
7. Valide que a imagem do container foi publicada no Docker Hub

## Recursos de Aprendizado

- [What is a container?](https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-a-container/)
- [Introduction to Containers and Docker](https://learn.microsoft.com/en-us/dotnet/architecture/microservices/container-docker-introduction)
- [A beginner's guide to Docker — how to create your first Docker application](https://www.freecodecamp.org/news/a-beginners-guide-to-docker-how-to-create-your-first-docker-application-cc03de9b639f/)