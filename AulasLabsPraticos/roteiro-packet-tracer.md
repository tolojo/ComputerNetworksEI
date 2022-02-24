
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

Após implementar o diagrama deve efetuar as ligações entre os equipamentos nas portas indicadas no diagrama, ou seja, computadores pessoais nas portas *FastEthernet* 1 a 6 (da direita para a esquerda, portanto a comecar pelos computadores da rede **192.168.100.x**). O servidor deve ser ligado às porta 24 (ultima porta *FastEthernet*).

No switch é necessário efetuar as configurações adequadas destas portas. Na aula faz-se esta configuração na gestão gráfica dos equipamentos. Estas são as únicas configurações de equipamentos de rede feitas desta forma (e apenas titulo de exemplo para utilizar a ferramenta de simulação, existe obviamente sintaxe para que possam ser feitas em linha de comando nos equipamentos).

Sendo assim, nas portas onde foram ligados computadores pessoais e o servidor, devem ser colocadas as VLANs adequadas:
- PCs da rede **192.168.100.x** na VLAN 100;
- PCs da rede **192.168.101.x** na VLAN 101;
- PCs da rede **192.168.102.x** na VLAN 102;
- o servidor que está na rede **192.168.200.x** deve ser colocado na VLAN 200. Antes devem-se criar as VLANs no menu adequado. 
Nota: Estas portas são colocadas em *Access* mode no menu de alterar as VLANs. 

Apenas as ligações entre equipamentos deverão ser em configuradas em *Trunk* por passarem várias VLANs. Isso só vai acontecer, tipicamente, na ligação entre routers e switchs ou entre switchs.

Acessoriamente, para poder fazer testes nas próximas configurações, poderá desejar configurar os IPs apresentados no diagrama de rede (rede do lado esquerdo) nos PCs e servidor. Para tal deverá abrir as configurações dos PCs e colocar o IP correspondente e a máscara de rede (255.255.255.0) nas configurações do endereço IP. Colocar sempre em *Manual* o endereço IP, nesta altura.

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

### Testar configurações

Se efetuou a configuração manual dos endereços IP anteriromente, já pode testar efetuar um `ping` a partir de um PC a outro PC e ao endereço do *router*.
Para fazer isto deverá usar uma *Command Prompt* (idêntica ao Windows) no menu *Desktop* dentro de um PC ou servidor. Após abrir a *Command Prompt* poderá testar a conectividade, por exemplo a partir do PC com o IP 192.168.100.11:
```
C:\>ping 192.168.100.1

Pinging 192.168.100.1 with 32 bytes of data:

Reply from 192.168.100.1: bytes=32 time=43ms TTL=255
Reply from 192.168.100.1: bytes=32 time<1ms TTL=255
Reply from 192.168.100.1: bytes=32 time<1ms TTL=255
Reply from 192.168.100.1: bytes=32 time=26ms TTL=255

Ping statistics for 192.168.100.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 43ms, Average = 17ms
```
Neste caso o comando `ping` testa a conectividade entre o PC e o router. Caso todos o output seja diferente (*Request timed out*) alguma configuiração anterior está errada.

Poderá ainda testar a conectividade ao outro PC da mesma VLAN:
```
C:\>ping 192.168.100.12

Pinging 192.168.100.12 with 32 bytes of data:

Reply from 192.168.100.12: bytes=32 time<1ms TTL=128
Reply from 192.168.100.12: bytes=32 time<1ms TTL=128
Reply from 192.168.100.12: bytes=32 time<1ms TTL=128
Reply from 192.168.100.12: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.100.12:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
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

#### Router ISP:

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

#### Router interno:

```
Configurar interface ipv6:
interface gi 0/1
ipv6 address 2001:9999:9999:9999::2/126
```

Nota: configurar IPv6 nos dois servidores internos com a mesma terminação dos endereços IPv4, para testar conectividade: 2001:1:1:0::10/64 e 2001:1:1:0::11/64

#### Configurar routing de IPv6 para permitir conectividade entre redes:

Routing:
```
ipv6 route 2001:1111:2222::/48 2001:9999:199:199::2
```

Router interno:
```
ipv6 route ::/0 2001:9999:9999:9999::1
```
