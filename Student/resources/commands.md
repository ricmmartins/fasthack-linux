# Guia de Referência de Comandos Linux 

O terminal de linha de comando no Linux é o componente mais poderoso do sistema operacional. No entanto, devido à grande quantidade de comandos disponíveis, pode ser intimidador para iniciantes. Mesmo usuários experientes podem esquecer um comando de vez em quando e é por isso que criamos este guia de referência de comandos Linux.

Nesta página, apresentaremos uma lista selecionada dos comandos Linux mais úteis. 

_Observe que esses comandos são para Linux em geral, tanto para distribuições baseadas em RedHat quanto em Debian. Existem alguns comandos na sessão de gerenciamento de pacotes que podem ser específicos para distribuições baseadas em Redhat, como yum e rpm, que não funcionam no Ubuntu (baseado em Debian)._


## Comandos de Arquivo

| Comando | Descrição |
|--------------|--------------|
|`ls` | Listar arquivos no diretório|
| `ls -a` | Listar todos os arquivos (mostra arquivos ocultos)|
| `locate [name]` | Encontrar todos os arquivos e diretórios relacionados a um nome específico: |
| `pwd` | Mostrar o diretório em que você está trabalhando atualmente |
| `mkdir [directory]` | Criar um novo diretório |
| `rm [file_name]` | Remover um arquivo |
| `rm -r [directory_name]`| Remover um diretório recursivamente|
|`rm -rf [directory_name]`|Remover recursivamente um diretório sem exigir confirmação|
|`cp [file_name1] [file_name2]`|Copiar o conteúdo de um arquivo para outro arquivo|
|`cp -r [directory_name1] [directory_name2]`|Copiar recursivamente o conteúdo de um arquivo para um segundo arquivo|
|`mv [file_name1] [file_name2]`|Renomear [file_name1] para [file_name2] com o comando|
|`ln -s /path/to/[file_name] [link_name]`|Criar um link simbólico para um arquivo|
| `touch [file_name]` | Criar um novo arquivo usando touch |
| `more [file_name]` | Mostrar o conteúdo de um arquivo | 
| `cat [file_name]`  | ou usar o comando cat |
| `cat [file_name1] >> [file_name2]` | Adicionar o conteúdo de um arquivo a outro arquivo | 
| `head [file_name]` | Exibir as primeiras 10 linhas de um arquivo com o comando head | 
| `tail [file_name]` | Mostrar as últimas 10 linhas de um arquivo | 
| `wc` | Mostrar o número de palavras, linhas e bytes em um arquivo usando wc | 
| `ls \| xargs wc` | Listar o número de linhas/palavras/caracteres em cada arquivo de um diretório com o comando xargs | 
| `cut -d[delimiter] [filename]` | Recortar uma seção de um arquivo e imprimir o resultado na saída padrão | 
| `[data] \| cut -d[delimiter]` | Recortar uma seção de dados canalizados e imprimir o resultado na saída padrão | 
| `awk '[pattern] {print $0}' [filename]` | Imprimir todas as linhas que correspondem a um padrão em um arquivo |
| `diff [file1] [file2]` | Comparar dois arquivos e exibir as diferenças| 
| `source [filename]` | Ler e executar o conteúdo do arquivo no shell atual| 
| `[command] \| tee [filename] >/dev/null` | Armazenar a saída do comando em um arquivo e pular a saída do terminal | 

## Pesquisa

| Comando | Descrição |
|--------------|--------------|
| `grep [pattern] [file_name]` | Pesquisar um padrão específico em um arquivo com grep |
| `grep -r [pattern] [directory_name]` | Pesquisar recursivamente um padrão em um diretório:|
| `locate [name]` | Encontrar todos os arquivos e diretórios relacionados a um nome específico: |
| `find [/folder/location] -name [a]` | Listar nomes que começam com um caractere especificado [a] em um local especificado [/folder/location] usando o comando find: |
| `find [/folder/location] -size [+100M]` | Ver arquivos maiores que um tamanho especificado [+100M] em uma pasta: |

## Navegação de Diretórios

| Comando | Descrição |
|--------------|--------------|
|`tar cf [compressed_file.tar] [file_name]`|Arquivar um arquivo existente|
|`tar xf [compressed_file.tar]`|Extrair um arquivo arquivado|
|`tar czf [compressed_file.tar.gz]`|Criar um arquivo tar compactado com gzip executando|
|`gzip [file_name]`  | Compactar um arquivo com a extensão .gz | 


## Transferência de Arquivos

| Comando | Descrição |
|--------------|--------------|
|`scp [file_name.txt] [server/tmp]`|Copiar um arquivo para um diretório do servidor de forma segura usando o comando scp do Linux|
|`rsync -a [/your/directory] [/backup/] `|Sincronizar o conteúdo de um diretório com um diretório de backup usando o comando rsync|

## Usuários e Grupos

| Comando | Descrição |
|--------------|--------------|
|`id`|Ver detalhes sobre os usuários ativos|
|`last`|Mostrar últimos logins do sistema|
|`who`|Exibir quem está atualmente logado no sistema com o comando who|
|`w`  | Mostrar quais usuários estão logados e suas atividades | 
| `groupadd [group_name]` | Adicionar um novo grupo digitando |
| `adduser [user_name]` | Adicionar um novo usuário|
| `usermod -aG [group_name] [user_name]` | Adicionar um usuário a um grupo |
| `sudo [command_to_be_executed_as_superuser]`| Elevar temporariamente os privilégios do usuário para superusuário ou root usando o comando sudo | 
| `userdel [user_name] ` | Excluir um usuário | 
| `usermod`| Modificar informações do usuário com |
| `chgrp [group-name] [directory-name]` | Alterar o grupo do diretório|

## Instalação de Pacotes

| Comando | Descrição |
|--------------|--------------|
|`yum list installed`|Listar todos os pacotes instalados com yum|
|`yum search [keyword]`|Encontrar um pacote por uma palavra-chave relacionada|
|`yum info [package_name]`|Mostrar informações e resumo do pacote|
|`yum install [package_name.rpm]`|Instalar um pacote usando o gerenciador de pacotes YUM|
|`dnf install [package_name.rpm]`|Instalar um pacote usando o gerenciador de pacotes DNF|
|`apt install [package_name]`|Instalar um pacote usando o gerenciador de pacotes APT|
|`rpm -i  [package_name.rpm]`|Instalar um pacote .rpm de um arquivo local|
|`rpm -e [package_name.rpm]`|Remover um pacote .rpm|
|`dpkg -i [package_name.deb]`|Instalar um pacote .deb de um arquivo local|
|`dpkg -r [package_name.deb]`|Remover um pacote .deb|
|`tar zxvf [source_code.tar.gz] && cd [source_code] && ./configure && make && make install`|Instalar software a partir do código-fonte|

## Gerenciamento de Processos

| Comando | Descrição |
|--------------|--------------|
|`ps` | Ver um snapshot dos processos ativos|
|`pstree`|Mostrar processos em um diagrama em forma de árvore|
|`pmap`|Exibir um mapa de uso de memória dos processos|
|`top`|Ver todos os processos em execução|
|`kill [process_id]` |Encerrar um processo Linux com um ID específico |
|`pkill [proc_name]` | Encerrar um processo com um nome específico|
|`killall [proc_name`|Encerrar todos os processos rotulados como "proc"|
|`bg`|Listar e retomar trabalhos parados em segundo plano|
|`fg`|Trazer o trabalho suspenso mais recentemente para o primeiro plano|
|`fg [job]`|Trazer um trabalho específico para o primeiro plano|
|`lsof`|Listar arquivos abertos por processos em execução|
|`trap "[commands-to-execute-on-trapping]" [signal]`|Capturar um sinal de erro do sistema em um script shell|
|`wait`|Pausar o terminal ou um script Bash até que um processo em execução seja concluído|
|`nohup [command] &`|Executar um processo Linux em segundo plano|

## Gerenciamento e Informações do Sistema

| Comando | Descrição |
|--------------|--------------|
|`uname -r` | Mostrar informações do sistema|
|`uname -a`|Ver informações sobre a versão do kernel|
|`uptime `|Exibir há quanto tempo o sistema está em execução, incluindo a média de carga|
|`hostname`|Ver o nome do host do sistema|
|`hostname -i`|Mostrar o endereço IP do sistema|
|`last reboot`|Listar o histórico de reinicializações do sistema|
|`date`|Ver a hora e data atuais|
|`timedatectl `|Consultar e alterar o relógio do sistema com|
|`cal`|Mostrar o calendário atual (mês e dia)|
|`whoami`|Ver qual usuário você está usando|
|`finger [username]`|Mostrar informações sobre um usuário específico|
|`ulimit [flags] [limit]`|Visualizar ou limitar a quantidade de recursos do sistema|
|`shutdown [hh:mm]`|Agendar o desligamento do sistema|
|`shutdown now` |Desligar o sistema imediatamente|

## Uso de Disco

| Comando | Descrição |
|--------------|--------------|
|`df -h`|Ver espaço livre e usado em sistemas montados|
|`df -i`|Mostrar inodes livres em sistemas de arquivos montados|
|`fdisk -l`|Exibir partições de disco, tamanhos e tipos com o comando|
|`du -ah`|Ver o uso de disco de todos os arquivos e diretórios|
|`du -sh`|Mostrar o uso de disco do diretório em que você está atualmente|
|`findmnt`|Exibir o ponto de montagem de destino para todos os sistemas de arquivos|
|`mount [device_path] [mount_point]` | Montar um dispositivo|


## Login SSH

| Comando | Descrição |
|--------------|--------------|
|`ssh user@host`|Conectar ao host como usuário|
|`ssh host` | Conectar de forma segura ao host via SSH na porta padrão 22| 
| `ssh -p [port] user@host` |Conectar ao host usando uma porta específica|

## Permissões de Arquivo

| Comando | Descrição |
|--------------|--------------|
|`chmod 777 [file_name]`|Atribuir permissão de leitura, escrita e execução para todos|
|`chmod 755 [file_name]`|Dar permissão de leitura, escrita e execução ao proprietário, e permissão de leitura e execução ao grupo e outros|
|`chmod 766 [file_name]` | Atribuir permissão total ao proprietário, e permissão de leitura e escrita ao grupo e outros| 
|`chown [user] [file_name]`| Alterar a propriedade de um arquivo|
|`chown [user]:[group] [file_name]`|Alterar o proprietário e o grupo de um arquivo|

## Rede

| Comando | Descrição |
|--------------|--------------|
|`ip addr show` | Listar endereços IP e interfaces de rede|
|`ip address add [IP_address]`| Atribuir um endereço IP à interface eth0|
|`ifconfig` | Exibir endereços IP de todas as interfaces de rede com|
|`netstat -pnltu` | Ver portas ativas (em escuta) com o comando netstat|
| `netstat -nutlp` | Mostrar portas tcp e udp e seus programas|
| `whois [domain]` | Exibir mais informações sobre um domínio|
| `dig [domain] ` | Mostrar informações DNS sobre um domínio usando o comando dig|
| `dig -x host` | Fazer uma consulta reversa em um domínio|
| `dig -x [ip_address]` | Fazer consulta reversa de um endereço IP|
| `host [domain]` | Realizar uma consulta de IP para um domínio|
| `hostname -I` | Mostrar o endereço IP local|
| `wget [file_name]` | Baixar um arquivo de um domínio usando o comando wget|
| `nslookup [domain-name]` | Receber informações sobre um domínio da internet|
| `curl -O [file-url]` | Salvar um arquivo remoto no seu sistema usando o nome de arquivo que corresponde ao nome no servidor|

## Variáveis

| Comando | Descrição |
|--------------|--------------|
| `let "[variable]=[value]"`|Atribuir um valor inteiro a uma variável|
| `export [variable-name]` | Exportar uma variável Bash| 
| `declare [variable-name]= "[value]"` | Declarar uma variável Bash|
| `set` | Listar os nomes de todas as variáveis e funções do shell|
| `echo $[variable-name]` | Exibir o valor de uma variável|

## Gerenciamento de Comandos Shell

| Comando | Descrição |
|--------------|--------------|
| `alias [alias-name]='[command]'` | Criar um alias para um comando|
| `watch -n [interval-in-seconds] [command]` | Definir um intervalo personalizado para executar um comando definido pelo usuário|
| `sleep [time-interval] && [command]` | Adiar a execução de um comando|
| `at [hh:mm]` | Criar uma tarefa a ser executada em um horário específico (Ctrl+D para sair do prompt após digitar o comando)|
| `man [command]` | Exibir o manual integrado de um comando |
| `history` | Imprimir o histórico dos comandos que você usou no terminal|

## Atalhos de Teclado do Linux

| Comando | Descrição |
|--------------|--------------|
| `Ctrl + C` | Encerrar processo em execução no terminal|
| `Ctrl + Z` | Parar o processo atual - O processo pode ser retomado em primeiro plano com `fg` ou em segundo plano com `bg`|
| `Ctrl + W` | Recortar uma palavra antes do cursor e adicioná-la à área de transferência|
| `Ctrl + U` | Recortar parte da linha antes do cursor e adicioná-la à área de transferência |
| `Ctrl + K` | Recortar parte da linha após o cursor e adicioná-la à área de transferência |
| `Ctrl + Y` | Colar da área de transferência |
| `Ctrl + R` | Recuperar o último comando que corresponde aos caracteres fornecidos|
| `Ctrl + O` | Executar o comando recuperado anteriormente|
| `Ctrl + G` | Sair do histórico de comandos sem executar um comando|
| `!!` | Executar o último comando novamente |
| `Ctrl + D | Fazer logout da sessão atual|

## Informações de Hardware

| Comando | Descrição |
|--------------|--------------|
|`dmesg` | Mostrar mensagens de inicialização |
| `cat /proc/cpuinfo` | Ver informações da CPU|
| `free -h` | Exibir memória livre e usada |
| `lshw` | Listar informações de configuração de hardware |
| `lsblk` | Ver informações sobre dispositivos de bloco |
| `lspci -tv`| Mostrar dispositivos PCI em um diagrama em forma de árvore | 
| `dmidecode` |Mostrar informações de hardware do BIOS |
| `hdparm -i /dev/disk` | Exibir informações de dados do disco |
| `hdparm -tT /dev/[device]` | Realizar um teste de velocidade de leitura no dispositivo/disco |
| `fsck [disk-or-partition-location]`| Executar uma verificação de disco em um disco ou partição não montada | 