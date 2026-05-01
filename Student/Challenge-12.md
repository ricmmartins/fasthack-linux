# Desafio 12 - Configurando um servidor web

[< Desafio Anterior](./Challenge-11.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-13.md)

## Descrição

Neste desafio vamos configurar um servidor web e implantar uma aplicação PHP simples nele. Como um plus, você pode adicionar SSL para garantir requisitos de segurança.

- Baixe a aplicação de exemplo [daqui](./resources/simple-php-app.tar.gz?raw=true) para o seu diretório home
- Extraia o conteúdo do simple-php-app.tar.gz no seu diretório home
- Instale o nginx-core
- Instale o php7.4-fpm
- Configure o Nginx

## Critérios de Sucesso

1. Certifique-se de que o arquivo simple-php-app-tar.gz está dentro do seu `~`
2. Mostre o conteúdo do arquivo .tar.gz extraído no seu `~`
3. Certifique-se de que os pacotes nginx-core e php7.4-fpm estão instalados
4. Mostre o seu Nginx funcionando corretamente

## Dica

Se você instalar o Ubuntu 18.04 em vez do Ubuntu 20.04, a versão do php-fpm que será instalada será a 7.2 em vez da 7.4. Então certifique-se de configurar o arquivo de configuração do nginx corretamente.

## Recursos de Aprendizado

- [How to install PHP 7.4 With Nginx on Ubuntu 20.04](https://www.rosehosting.com/blog/how-to-install-php-7-4-with-nginx-on-ubuntu-20-04/)
- [How To Install Linux, Nginx, MySQL, PHP (LEMP stack) on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-20-04)

## Desafio Avançado
*Muito confortável? Quer fazer mais? Tente este desafio adicional!*

- Adicionar SSL

_Por favor, note que para este desafio avançado, você precisará acessar a máquina virtual usando um IP Público devido ao uso de um certificado SSL._

