# What The Hack - Fundamentos do Linux - Guia do Coach

## Introdução
Bem-vindo ao guia do coach para o Hackathon de Fundamentos do Linux. Aqui você encontrará links para orientações específicas para coaches em cada um dos desafios.

> **NOTA:** Se você é um participante do Hackathon, este é o guia de respostas. Não trapaceie olhando estas respostas durante o hack! Vá aprender algo. :)

## Guias do Coach

| # | Solução | Descrição |
|---|---------|-----------|
| 01 | **[Criar uma Máquina Virtual Linux](Solution-01.md)** | Configurar um ambiente Ubuntu Linux — VM na nuvem, VM local ou WSL2 |
| 02 | **[Manipulando Diretórios](Solution-02.md)** | Operações comuns com diretórios |
| 03 | **[Manipulando Arquivos](Solution-03.md)** | Manipulação de arquivos: criar, renomear, encontrar e remover |
| 04 | **[Conteúdo de Arquivos](Solution-04.md)** | Manipulação de conteúdo de arquivos |
| 05 | **[Permissões Padrão de Arquivos](Solution-05.md)** | Permissões de arquivos Linux e propriedade |
| 06 | **[Gerenciamento de Processos](Solution-06.md)** | Verificar processos em execução e identificar PIDs |
| 07 | **[Gerenciamento de Grupos e Usuários](Solution-07.md)** | Criação de usuários e grupos |
| 08 | **[Scripting](Solution-08.md)** | Scripts básicos em shell |
| 09 | **[Discos, Partições e Sistemas de Arquivos](Solution-09.md)** | fdisk, mkfs e mount |
| 10 | **[Gerenciador de Volumes Lógicos](Solution-10.md)** | pvcreate, vgcreate, lvcreate |
| 11 | **[Gerenciamento de Pacotes](Solution-11.md)** | Instalação e gerenciamento de pacotes |
| 12 | **[Configurando um Servidor Web](Solution-12.md)** | Implantação de aplicação web com Nginx + PHP-FPM |
| 13 | **[Protegendo um Servidor](Solution-13.md)** | Fail2Ban e hardening de SSH |
| 14 | **[Executando Contêineres](Solution-14.md)** | Containers Docker e construção de imagens |
| 15 | **[Fundamentos de Rede](Solution-15.md)** | IP, DNS, roteamento, portas, conectividade |
| 16 | **[systemd e Gerenciamento de Serviços](Solution-16.md)** | systemctl, journalctl, units personalizadas |
| 17 | **[Processamento de Texto](Solution-17.md)** | sed, awk, pipes, pipelines de texto |
| 18 | **[Agendamento de Tarefas](Solution-18.md)** | Cron jobs e agendamento com at |
| 19 | **[Configuração de Firewall](Solution-19.md)** | Regras UFW e limitação de taxa |
| 20 | **[Troubleshooting Linux](Solution-20.md)** | Cenários capstone de troubleshooting |

## Pré-requisitos do Coach

Este hack possui pré-requisitos que o coach é responsável por entender e/ou configurar ANTES de sediar um evento.

O guia cobre os passos comuns de preparação que um coach precisa realizar antes do evento.

### Recursos do Estudante

Antes do hack, é responsabilidade do Coach garantir que os estudantes possam acessar o conteúdo da pasta `./Student/Resources`.

## Requisitos do Ambiente

Os estudantes precisam de acesso a um ambiente Linux. As seguintes opções são suportadas:

- **VM na Nuvem**: Azure, AWS, GCP ou qualquer provedor de nuvem — crie uma VM Ubuntu 24.04 LTS
- **VM Local**: VirtualBox, UTM, Hyper-V ou VMware com Ubuntu 24.04 LTS
- **WSL2**: Windows Subsystem for Linux (Ubuntu)
- **Servidor existente**: Qualquer sistema Linux baseado em Ubuntu/Debian

Para os Desafios 09 e 10 (Discos/LVM), os estudantes precisarão da capacidade de anexar um disco adicional à sua VM. Isso é simples em provedores de nuvem e ferramentas de VM local, mas não é suportado no WSL2.

Para o desafio avançado opcional do Desafio 12 (SSL), os estudantes precisarão:
- Um IP público associado à máquina virtual
- Acesso ao IP público pela internet
- Um nome de domínio com acesso ao gerenciamento de DNS (opcional, para SSL adequado)

## Tempo Estimado

| Desafio | Tempo |
|---------|-------|
| 01 - Criar uma VM Linux | 15-30 min |
| 02 - Manipulando Diretórios | 15-20 min |
| 03 - Manipulando Arquivos | 20-30 min |
| 04 - Conteúdo de Arquivos | 15-20 min |
| 05 - Permissões Padrão de Arquivos | 20-30 min |
| 06 - Gerenciamento de Processos | 15-20 min |
| 07 - Gerenciamento de Grupos e Usuários | 20-30 min |
| 08 - Scripting | 30-45 min |
| 09 - Discos, Partições e Sistemas de Arquivos | 30-45 min |
| 10 - Gerenciador de Volumes Lógicos | 30-45 min |
| 11 - Gerenciamento de Pacotes | 15-20 min |
| 12 - Configurando um Servidor Web | 30-45 min |
| 13 - Protegendo um Servidor | 30-45 min |
| 14 - Executando Contêineres | 30-45 min |
| 15 - Fundamentos de Rede | 25-35 min |
| 16 - systemd e Gerenciamento de Serviços | 25-35 min |
| 17 - Processamento de Texto | 20-30 min |
| 18 - Agendamento de Tarefas | 20-30 min |
| 19 - Configuração de Firewall | 25-35 min |
| 20 - Troubleshooting Linux (Capstone) | 35-45 min |
| **Total** | **~8-11 horas** |

## Conteúdo do Repositório

- `./Coach` — Guia do coach e arquivos de solução
- `./Student` — Guia de desafios do estudante
- `./Student/resources` — Arquivos de recursos, código de exemplo e materiais de referência

