# Desafio 05 - Permissões padrão de arquivos

[< Desafio Anterior](./Challenge-04.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-06.md)

## Descrição

Neste desafio você aprenderá sobre as permissões padrão de arquivos do Linux e entenderá como trabalhar com permissões de arquivos em um ambiente Linux

- Como usuário regular (student), crie um diretório `~/permissions`
- Crie um arquivo chamado `myfile.txt` sob `~permissions`
- Liste as propriedades do arquivo `/var/log/waagent.log`. Em seguida, copie este arquivo para o seu diretório permissions
- Como root, crie um arquivo chamado rootfile.txt no diretório `/home/student/permissions`
- Como usuário regular (student), veja quem é o dono deste arquivo criado pelo root
- Altere a propriedade de todos os arquivos em `/home/student/permissions` para você mesmo (student)
- Certifique-se de que você (student) tem todos os direitos sobre os arquivos dentro de `~`, e que outros podem apenas ler

## Critérios de Sucesso

1. Verifique se o diretório foi criado com sucesso
2. Confirme o arquivo criado sob `~permissions`
3. Verifique o arquivo dentro do seu diretório permissions. Quem é o novo dono deste arquivo agora?
4. Certifique-se de que criou o arquivo como o usuário root no diretório `/home/student/permissions`
5. Garanta que você está logado como usuário regular (student), então verifique o dono do arquivo criado pelo usuário root
6. Valide que você conseguiu alterar a propriedade de todos os arquivos em `/home/student/permissions` para o usuário student
7. Confirme seus direitos dentro de `~`, e certifique-se de que outros usuários podem apenas ler


## Recursos de Aprendizado

- [File Permissions](https://linuxjourney.com/lesson/file-permissions)
- [Understanding Linux File Permissions](https://www.linuxfoundation.org/blog/classic-sysadmin-understanding-linux-file-permissions/)
- [Chmod Calculator](https://chmod-calculator.com/)
- [Linux File Permissions](https://linuxhandbook.com/linux-file-permissions/)
- [Suid, Sgid, and Sticky Bit](https://linuxhandbook.com/suid-sgid-sticky-bit/)