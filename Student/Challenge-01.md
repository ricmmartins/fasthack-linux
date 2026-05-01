# Desafio 01 - Criar uma Máquina Virtual Linux

**[Início](../README.md)** - [Próximo Desafio >](./Challenge-02.md)

## Pré-requisitos 

- Uma assinatura Azure ativa.

## Descrição

Para acompanhar, você precisará de acesso a um servidor executando um sistema operacional baseado em Linux. Note que este hackathon foi validado usando um servidor Linux executando Ubuntu 20.04 ([LTS](https://ubuntu.com/about/release-cycle)), mas os exemplos dados devem funcionar em qualquer distribuição Linux. Veja abaixo os passos a seguir para criar sua Máquina Virtual Linux no Azure e escolha aquele com o qual você está mais familiarizado.

Durante o processo de criação da VM, garanta o uso de **student** para o nome de usuário com privilégios de root sobre a máquina virtual, apenas para facilitar durante os desafios. 

### Aviso

Abrir a porta 22 para a internet pública é uma má prática. Recomendamos fortemente o uso do Azure Bastion ou a criação de uma regra NSG que limite o acesso ao endereço IP residencial do estudante (ou instância do Azure Cloud Shell).

## Critérios de Sucesso

* Valide que você conseguiu criar com sucesso sua Máquina Virtual Linux **Ubuntu 20.04**
* Confirme que você consegue acessar via SSH

## Recursos de Aprendizado

* [Criar uma máquina virtual Linux no portal do Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-portal)
* [Criar uma máquina virtual Linux com o Azure CLI](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-cli)
* [Criar uma máquina virtual Linux no Azure com PowerShell](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/quick-create-powershell)
* [Conectar a uma VM Linux](https://docs.microsoft.com/en-us/azure/virtual-machines/linux-vm-connect?tabs=Linux)