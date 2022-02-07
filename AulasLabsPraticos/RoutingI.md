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

## 1. Interligar Máquinas Virtuais

## 1.1 Interligar UE01 com UE02

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

## 1.2 Interligar UE01 com UE03

Para interligar estas duas máquinas virtuais, deve configurar os seguintes endereços em cada uma delas:

**UE01** - interface `enp0s8` - **192.168.2.1**

`$ sudo ifconfig enp0s3 192.168.1.1/24 up`

**UE03** - interface `enp0s3` - **192.168.2.2**

`$ sudo ifconfig enp0s3 192.168.1.2/24 up`

Para garantir que os novos endereços ficam ativos poderá reiniciar a componente de networking:

`$ sudo /etc/init.d/networking force-reload`

Deverá depois certificar-se que tudo está correto através dos seguintes comandos:

```
$ /sbin/ifconfig
$ /sbin/route
```

Para verificar se tem conectividade poderá utilizar o `ping`:

(a partir da UE01) `$ ping 192.168.2.2`

(a partir da UE03) `$ ping 192.168.2.1`

## Preparar a UE01 para fazer routing de pacotes e configurar o default gateway da UE02 e UE03

### Configurar UE01


Defining a default gateway means that whenever a machine does not have a specific route for a given network, those packets are sent to its default gateway. Since VM2 will be the default gateway for VM1, IP forwarding must be enabled in VM2. This will allow VM1 to communicate with machines outside its subnet 192.168.0.X.

Activate IP forwarding with:

$ sudo sysctl net.ipv4.ip_forward=1   # on VM2
Confirm that the flag value was updated to 1:

$ /sbin/sysctl net.ipv4.conf.all.forwarding

### Configurar UE02 e UE03

Now set VM2 as the default gateway for VM1 by doing this:

$ sudo ip route add default via 192.168.0.10   # on VM1
Try again to ping VM3 from VM1.

$ ping 192.168.1.1       # on VM1
Does it work? Can you identify where the problem is? Run the commands below and see if you understand what is happening

$ sudo tcpdump -i enp0s3   # on VM1
$ sudo tcpdump -i enp0s3   # on VM2
$ sudo tcpdump -i enp0s8   # on VM2
$ sudo tcpdump -i enp0s8   # on VM3
What happens now when you ping VM1 from VM3? Why is the answer different?

Add now VM2 also as the default gateway for VM3. This would allow VM3 to talk to machines outside its subnet 192.168.1.X.

$ sudo ip route add default via 192.168.1.254    # on VM3
Can you now ping VM3 from VM1? Why?
And can you ping VM1 from VM3? Why?

## Configurar NAT (Network Address Translation)

2.4 Configure NAT (Network Address Translation)

Try to ping google.com from the 3 machines? Why can't you do it from VM1 nor VM3?

The issue is that VM2 is acting as the gateway to the internet for both VM1 and VM3 but is not NATing the packets. If you run

$ ping 8.8.8.8                    # on VM1
$ sudo tcpdump -i enp0s9 -p icmp    # on VM2 (interface to the internet)
you can observe that the packets go out to google.com but do not come back. Why? Because google.com does not know where 192.168.0.100 is and so cannot send the packets back. You can use the iptables command (man iptables) in VM2 to correct this behaviour. NAT will do the source and destination mapping.

$ sudo iptables -P FORWARD ACCEPT    # Defines default policy for FORWARD
$ sudo iptables -F FORWARD           # Flushes all the rules from chain FORWARD
$ sudo iptables -t nat -F            # Flushes all the rules from table NAT
$ sudo iptables -t nat -A POSTROUTING  -o enp0s9 -j MASQUERADE    # Creates a source NAT on interface enp0s9
Test again

$ ping 8.8.8.8                    # on VM1
$ sudo tcpdump -i enp0s9 -p icmp    # on VM2 (interface to the internet)
What do you observe? Why does it work now?
What is the source address of the packet now? Compare this source address to the previous case.
Lets now go back to 2.3 to the scenario where VM2 is the default gateway for VM1 but where VM3 has no default gateway.

To remove the default gateway run in VM3

$ sudo route del default    # on VM3
As seen before you cannot ping VM3 from VM1. Could you solve this issue with a NAT (in interface enp0s8 of VM2) instead of adding VM2 as the default gateway for VM3? Why?
And can you ping VM1 from VM3? Why?


## Garantir que as configurações ficam permanentes

Making these changes permanent

The changes you made before will be lost once you perform a reboot of your machine. In order to make them permanent you have to edit the corresponding /etc/network/interfaces

```
## On VM1
auto enp0s3
iface enp0s3 inet static
    address 192.168.0.100
    netmask 255.255.255.0
    gateway 192.168.0.10
    dns-nameservers 8.8.8.8 8.8.4.4
### On VM2
auto enp0s3
iface enp0s3 inet static
    address 192.168.0.10
    netmask 255.255.255.0
    dns-nameservers 8.8.8.8 8.8.4.4

auto enp0s8
iface enp0s8 inet static
    address 192.168.1.254
    netmask 255.255.255.0
    dns-nameservers 8.8.8.8 8.8.4.4

auto enp0s9
iface enp0s9 inet dhcp
### On VM3
auto enp0s3
iface enp0s3 inet static
    address 192.168.1.1
    netmask 255.255.255.0
    gateway 192.168.1.254
    dns-nameservers 8.8.8.8 8.8.4.4
```

You should also enable IP forwarding permanently on VM2. For that you need to edit /etc/sysctl.conf and uncomment the following line

net.ipv4.ip_forward=1



Gracefully turn off the virtual machines (for rnl-virt only)

To gracefully close the virtual machines which you deployed using the rnl-virt command, execute the following on VM1, VM2 and VM3:

$ sudo /sbin/poweroff







Finally, create a third Network adapter in VM2 that is nat-ed with your physical address. This interface will be used to access the Internet.

*Pedro Rosa - IADE/Universidade Europeia*
