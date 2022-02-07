# Laboratório 2: Routing I

O Laboratório 2 tem como objetivo:
- Introduzir sistema de endereçamento e routing de pacotes IP

Pré-requisito: Três máquinas virtuais - Instalação de pelo menos uma máquina virtual do SEED Project (tal como indicado [aqui](https://github.com/pmrosa-classes/ComputerNetworksEI/blob/main/AulasLabsPraticos/AulasLabsPraticos.md)) e dois clones.
Os clones deverão ser realizados no VirtualBox. Para tal deverá escolher a opção `Clone`, nomear a máquina virtual e escolher a opção "MAC Adress Policy: Generate new MAC addresses for all network adapters". No final escolher *Linked Clone* para poupar espaço de armazenamento. O outro tipo de clone duplica o espaço em disco gasto pela primeira máquina virtual; o Linked Clone apenas grava as diferenças em relação à máquina original.
Aconselha-se o uso de nomes como UE01, UE02 e UE03, ou algo do género, para as máquinas virtuais. Na documentação serão usados esses identificadores

## 0. Topologia a implementar

(desenho)

As primeiras placas de rede da UE01 e UE02 estão ligadas ao switch01; a segunda placa de rede do UE02 e a primeira placa de rede da UE03 estão ligadas ao switch02.

