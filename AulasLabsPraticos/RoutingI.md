# Laboratório 2: Routing I

O Laboratório 2 tem como objetivo:
- Introduzir sistema de endereçamento e routing de pacotes IP

Pré-requisito: Três máquinas virtuais - Instalação de pelo menos uma máquina virtual do SEED Project (tal como indicado [aqui](https://github.com/pmrosa-classes/ComputerNetworksEI/blob/main/AulasLabsPraticos/AulasLabsPraticos.md)) e dois clones.

Os clones deverão ser realizados no VirtualBox. Para tal deverá escolher a opção `Clone`, nomear a máquina virtual e escolher a opção `MAC Adress Policy: Generate new MAC addresses for all network adapters`. No final escolher `Linked Clone` para poupar espaço de armazenamento. O outro tipo de clone duplica o espaço em disco gasto pela primeira máquina virtual; o Linked Clone apenas grava as diferenças em relação à máquina original.

Aconselha-se o uso de nomes como UE01, UE02 e UE03, ou algo do género, para as máquinas virtuais. Na documentação serão usados esses identificadores

## 0. Topologia a implementar

(desenho)

As primeiras placas de rede da UE01 e UE02 estão ligadas ao `switch01`; a segunda placa de rede do UE02 e a primeira placa de rede da UE03 estão ligadas ao `switch02`.

Para associar as placas de rede a esses switchs deve desligar as máquinas e escolher a opção `Attach to Internal Network` nas configurações da placa de rede
Atribuir o nomes `switch01` e `switch02` aos switchs, nas respetivas máquinas. Não esquecer de escolher a opção `Promiscuous Mode: Allow VMs`

## 1. Interligar UE01 com UE02

Para interligar estas duas máquinas virtuais, deve configurar os seguintes endereços em cada uma delas:

**UE01** - interface `enp0s3` - **192.168.1.1**

`$ sudo ifconfig enp0s3 192.168.1.1/24 up`

**UE02** - interface `enp0s3` - **192.168.1.2**

`$ sudo ifconfig enp0s3 192.168.1.2/24 up`

Para garantir que os novos endereços ficam ativos poderá reiniciar a componente de networking:

`$ sudo /etc/init.d/networking force-reload`

Deverá depois certificar-se que tudo está correto através dos seguintes comandos:

```
$ /sbin/ifconfig
$ /sbin/route
```

Para verificar se tem conectividade poderá utilizar o `ping`:

(a partir da UE01) `$ ping 192.168.1.2`

(a partir da UE02) `$ ping 192.168.1.1`

Deverá ter um output semelhante a este:
```
Ping reply ....
```








Finally, create a third Network adapter in VM2 that is nat-ed with your physical address. This interface will be used to access the Internet.

*Pedro Rosa - IADE/Universidade Europeia*
