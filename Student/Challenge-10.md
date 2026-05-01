# Desafio 10 - Logical Volume Manager

[< Desafio Anterior](./Challenge-09.md) - **[Início](../README.md)** - [Próximo Desafio >](./Challenge-11.md)

## Pré-requisitos

- Crie um disco de dados de 5GB
- Adicione à Máquina Virtual

## Descrição

Este desafio lhe dará um entendimento sobre o Logical Volume Manager no Linux, e conhecimento usando os comandos pvcreate, vgcreate, lvrcreate, e mais

- Crie um Physical Volume (`PV`) com o disco adicionado
- Verifique se o ```PV``` foi criado
- Crie um Volume Group (```VG```) usando o PV criado
- Verifique se o VG foi criado
- Crie um Logical Volume (```LV```) usando metade do disco (2.5GB)
- Crie um ```LV``` usando 10% do disco (500MB)
- Verifique se os ```LV```s foram criados
- Formate ambos os ```LV```s como ```ext4```
- Monte os ```LV```s nos diretórios criados anteriormente em ```/mnt```
- Redimensione o menor ```LV``` para ocupar mais 20% do disco (1GB)
- Verifique:
    - Se o ```LV``` foi redimensionado
    - Se houve reflexo no sistema de arquivos
- Redimensione o sistema de arquivos

## Critérios de Sucesso

1. Valide a criação do Physical Volume
2. Valide a criação do Volume Group
3. Valide a criação do Logical Volume
4. Certifique-se de que ambos os volumes lógicos foram criados com os tamanhos esperados
5. Certifique-se de que ambos os volumes lógicos foram formatados como sistema de arquivos ext4
6. Confirme que ambos os volumes lógicos foram corretamente montados em `/mnt`
7. Mostre o volume lógico e o sistema de arquivos redimensionados


## Recursos de Aprendizado

- [LVM (Logical Volume Manager)](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/5/html/deployment_guide/ch-lvm)
- [LVM Guide](https://linuxhandbook.com/lvm-guide/)
- [What is LVM (Logical Volume Management), and what are its Benefits?](https://linuxhint.com/whatis_logical_volume_management/)
- [Linux Logical Volume Manager (LVM) tutorial](https://linuxconfig.org/linux-lvm-logical-volume-manager)
- [A Beginner's Guide To LVM](https://www.howtoforge.com/linux_lvm)