# Laboratório 4: Routing II / Firewall

O Laboratório 4 tem como objetivo **Desenvolver o sistema de endereçamento IP, routing e mecanismos de firewall** através de configurações em máquinas virtuais Linux (Ubuntu).

***Pré-requisito: Três máquinas virtuais - Instalação de pelo menos uma máquina virtual do SEED Project e dois clones; Ter o Laboratório 3: Routing I efetuado***


## 1. Utilização de *iptables

Testar ICMP

Cortar ICMP

`$ sudo /sbin/iptables –A INPUT –p icmp –j DROP`

Testar ICMP

Apagar a regra colocada

`$ sudo /sbin/iptables –D INPUT –p icmp –j DROP`

## 2. Capturar tráfego com *tcpdump*

$ sudo tcpdump -i enp0s3
$ sudo tcpdump -i enp0s3
$ sudo tcpdump -i enp0s8
$ sudo tcpdump -i enp0s8

## 3. Testar serviço *ssh (acesso remoto)

Test SSH

Use tcpdump

Cut SSH

`sudo /sbin/iptables –A INPUT –p tcp –-dport 22 –j DROP`

Use tcpdump

## 4. Testar serviço *http (web)

Test Web

Use tcpdump

Cut Web

`sudo /sbin/iptables –A INPUT –p tcp –-dport 80 –j DROP`
`sudo /sbin/iptables –A INPUT –p tcp –-dport 443 –j DROP`
Use tcpdump
