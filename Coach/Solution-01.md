# Desafio 01 - Criar uma Máquina Virtual Linux - Guia do Coach 

**[Home](./README.md)** - [Próxima Solução >](./Solution-02.md)

## Notas e Orientações
 
Para realizar a criação da Máquina Virtual Linux Ubuntu 20.04, você pode seguir os passos abaixo usando o Azure CLI a partir do cloud shell:

- Criar o resource group:

```bash
az group create --name rg-linux-fundamentals --location eastus
```

- Criar a Máquina Virtual

```bash
az vm create \
  --resource-group rg-linux-fundamentals \
  --name myVM \
  --image Canonical:0001-com-ubuntu-server-focal:20_04-lts:latest \
  --admin-username student \
  --generate-ssh-keys
```

- Conectar à máquina virtual

```bash
ssh student@[public-ip]
```