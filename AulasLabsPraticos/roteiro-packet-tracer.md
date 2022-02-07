
# Aulas Práticas com Cisco Packet Tracer
**VLANs/Routing/NAT/IPv4/DHCPv4/IPv6/DHCPv6**

Diagrama e sintaxe do exercício a realizar durante as aulas práticas com o software Cisco Packet Tracer

*Nota: a forma exata de implementação pode variar devido a alterações realizadas durante as aulas.|*

## Diagrama da Rede a configurar nas Aulas Práticas
![alt text](roteiro-imagem.png)


## Configurações iniciais

Entrar em modo privilegiado: `enable`

Entrar em modo de configuração: `config terminal`

Atribuir nome ao equipamento: `hostname Router1 `

Atribuir domínio ao equipamento: `ip domain-name universidadeeuropeia.pt`

Password de enable: `enable secret *password*`

Gravação de configurações: `copy running-config startup-config` or `wr`

## Configurar Switching

Após implementar o diagrama deve efetuar as ligações entre os equipamentos nas portas indicadas no diagrama.

As ligações entre equipamentos deverão ser em trunk (onde aplicável, isto é, onde passam várias VLANs) e as portas dos switchs devem ser colocadas nas VLANs adequadas. 
Na aula faz-se esta configuração na gestão gráfica dos equipamentos. Estas são as únicas configurações de equipamentos de rede feitas desta forma (e apenas titulo de exemplo para utilizar a ferramenta de simulação, existe obviamente sintaxe para que possam ser feitas em linha de comando nos equipamentos).

## Configurar IPv4

### Criação dos interfaces das redes de postos de trabalho no router:

```
interface gigabitethernet 0/0.100       *Sub-interface/vlan dentro do interface fisio gi 0/0*
encapsulation dot1Q 100                 *Colocação do interface na vlan 100*
ip address 192.168.100.1 255.255.255.0  *Indicação do ip address deste sub- interface*

interface gigabitethernet 0/0.101
encapsulation dot1Q 101
ip address 192.168.101.1 255.255.255.0

interface gigabitethernet 0/0.102\n
encapsulation dot1Q 102<br>
ip address 192.168.102.1 255.255.255.0`
```

### Criação do interface da rede de servidores no router:
```
interface gigabitethernet 0/0.200
encapsulation dot1Q 200
ip address 192.168.200.1 255.255.255.0`
```
### Ativar administrativamente o interface físico Gigabitethernet 0/0
```
interface gigabitethernet 0
no shutdown	Interfaces nos routers estão em “shutdown” por omissão, por isso têm que ser ativados manualmente
```
### Deverá ser configurado o serviço DHCP no servidor com as várias pools de endereços IPv4 necessárias

#### Configuração do relay de DHCP em cada um dos interfaces que necessite de DHCP (redes de postos de trabalho).
O IP do servidor é fixo: 192.168.200.10
```
interface gigabitethernet 0/0.100
ip helper-address 192.168.200.10		Indicação do servidor de DHCP para esta VLAN

interface gigabitethernet 0/0.101
ip helper-address 192.168.200.10

interface gigabitethernet 0/0.102
ip helper-address 192.168.200.10
```
### Configuração do NAT no router interno

#### Criação das listas de endereços para a realização de NAT:
```
access-list 1 permit 192.168.100.0 0.0.0.255
access-list 2 permit 192.168.101.0 0.0.0.255
access-list 3 permit 192.168.102.0 0.0.0.255
access-list 4 permit 192.168.200.0 0.0.0.255
```
#### Nos interfaces com ip privado colocar “ip nat inside” 
```
interface gigabitEthernet 0/0.100
ip nat inside					Indicação de que se trata de um interface interno
exit						sobre o qual será realizado NAT
interface gigabitEthernet 0/0.101
ip nat inside
exit
interface gigabitEthernet 0/0.102
ip nat inside
exit
interface gigabitEthernet 0/0.200
ip nat inside
exit
```

#### interface com ip publico colocar “ip nat outside” 
```
interface gigabitEthernet 0/1
ip nat outside
```

#### Configuração do tipo de NAT a relizar (um para muitos - overload):
```
ip nat inside source list 1 interface GigabitEthernet0/1 overload
ip nat inside source list 2 interface GigabitEthernet0/1 overload
ip nat inside source list 3 interface GigabitEthernet0/1 overload
ip nat inside source list 4 interface GigabitEthernet0/1 overload
```

### Colocação de novo router “ISP” e fazer a ligação entre redes com uma rede /30 ao router interno (rede 199.199.199.0/30)

#### Router interno: 
```
interface gigabitethernet 0/1
ip address 199.199.199.2 255.255.255.252
no shutdown
```

#### Router ISP: 
```
interface gigabitethernet 0/1
ip address 199.199.199.1 255.255.255.252
no shutdown
```

### Configuração do interface da rede de servidores no ISP

#### Router ISP: 
```
interface gigabitethernet 0/0
ip address 201.1.1.1 255.255.255.0
```

### Configuração do routing na rede interna (default gateway para mandar todos os pacotes desconhecidos para o ISP)

#### Router interno:
```
ip route 0.0.0.0 0.0.0.0 199.199.199.1
```

## Configurar IPv6 na rede interna

### Router interno:
Ligar routing de IPv6:
```
ipv6 unicast-routing 
```

Configurar interfaces ipv6:
```
interface gi 0/1.100
ipv6 address 2001:1111:2222:100:1/64
interface gi 0/1.101
ipv6 address 2001:1111:2222:101:1/64
interface gi 0/1.102
ipv6 address 2001:1111:2222:102:1/64
interface gi 0/1.200
ipv6 address 2001:1111:2222:200:1/64
```
Neste momento o Router já deverá enviar RA para a rede e os hosts devem conseguir obter um endereço IPv6 na configuração automática.

### Configuração de IPv6 DHCP Server no Router
```
Router(config)#ipv6 dhcp pool ipv6-pool-100
Router(config-dhcpv6)#domain-name europeia.internal
Router(config-dhcpv6)#dns-server 2001:1111:2222:100::10
Router(config-dhcpv6)#prefix-delegation pool client-prefix-100 lifetime 800 600
Router(config-dhcpv6)#exit
Router(config)#ipv6 local pool client-prefix-100 2001:1111:2222:100::/48 64
(prefix de rede 64 bits, dando endereços de 64 bits)
```
```
Router(config)#interface gigabitEthernet 0/0.100
Router(config-subif)# ipv6 dhcp server ipv6-pool-100 
(ativar a configuração de IPv6 por DHCP no interface)
Router(config-subif)# ipv6 nd other-config-flag
(para passar outras configs, como gateway, para os clientes)
```
Confirmar que aparece o servidor de DNS em Auto-Config/DHCP

Repetir para os outros interfaces 101 e 102. Rede 200 deverá ter um IP estátio.


### Configurar IPv6 na rede ISP (e routing com rede interna)

Configurar IPv6 na rede de interligação entre Router interno e Router ISP com a rede 2001:9999:9999:9999::/126 (...::1 no lado do ISP e ...::2 no lado da rede interna)
Configurar IPv6 no interface com a rede 2001:1:1:0::/64  (0 = default VLAN).
Configurar postos de trabalho com endereços 2001:1:1:0::10 e 2001:1:1:0::11.

Router ISP:

Ligar routing de IPv6:
```
ipv6 unicast-routing 
```

Configurar interfaces ipv6:
```
interface gi 0/0
ipv6 address 2001:1:1:0::1/64
interface gi 0/1
ipv6 address 2001:9999:9999:9999::1/126
```

Router interno:

```
Configurar interface ipv6:
interface gi 0/1
ipv6 address 2001:9999:9999:9999::2/126
```

Nota: configurar IPv6 nos dois servidores internos com a mesma terminação dos endereços IPv4, para testar conectividade: 2001:1:1:0::10/64 e 2001:1:1:0::11/64

Configurar routing de IPv6 para permitir conectividade entre redes:

Routing:
```
ipv6 route 2001:1111:2222::/48 2001:9999:199:199::2
```

Router interno:
```
ipv6 route ::/0 2001:9999:9999:9999::1
```
