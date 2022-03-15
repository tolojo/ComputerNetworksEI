# Laboratório 4: Routing II / Firewall

O Laboratório 4 tem como objetivo **Desenvolver o sistema de endereçamento IP, routing e mecanismos de firewall** através de configurações em máquinas virtuais Linux (Ubuntu).

***Pré-requisito: Três máquinas virtuais - Instalação de pelo menos uma máquina virtual do SEED Project e dois clones; Ter o Laboratório 3: Routing I efetuado***

## 0. Notas Prévias

Para gerir regras de firewall em Linux utiliza-se o comando `iptables`.

Alguns comandos uteis:

Para apagar todas as regras de firewall:

`sudo /sbin/iptables –F`

Para apagar todas as regras de nat:

`sudo /sbin/iptables -t nat –F`

## 1. Exemplo de utilização de *iptables* 

### 1.1 Testar ICMP (pings)

Em primeiro lugar deve-se testar que se consegue realizar um ping a partir do **UE02** para a **UE01**:

```
$ ping 192.168.1.1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
64 bytes from 192.168.1.1: icmp_seq=1 ttl=64 time=0.566 ms
64 bytes from 192.168.1.1: icmp_seq=2 ttl=64 time=0.526 ms
64 bytes from 192.168.1.1: icmp_seq=3 ttl=64 time=0.669 ms
64 bytes from 192.168.1.1: icmp_seq=4 ttl=64 time=0.658 ms
```
O comando `ping` utiliza o protocolo ICMP, como verificado nas aulas teóricas. Para impedir que um *host* responda a *pings* deve-se cortar o protocolo ICMP. Vamos testar esse corte no **UE01**:

`$ sudo /sbin/iptables –A INPUT –p icmp –j DROP`

Após isso deve-se efetuar novamente o `ping` ao mesmo *host*. É interessante colocar `-O` no comando para devolver uma resposta negativa (quando não consegue realizar o ping):

```
$ ping -O 192.168.1.1
PING 192.168.1.1 (192.168.1.1) 56(84) bytes of data.
no answer yet for icmp_seq=1
no answer yet for icmp_seq=2
no answer yet for icmp_seq=3
no answer yet for icmp_seq=4
```

Após o teste deve apagar a regra para impedir futuros problemas com testes de conectividade.

`$ sudo /sbin/iptables –D INPUT –p icmp –j DROP`

## 2. Utilização de *tcpdump* para capturar tráfego

Em **UE01**:

`$ sudo tcpdump -i enp0s3`

`$ sudo tcpdump -i enp0s8`

`$ sudo tcpdump -i enp0s9`

Em **UE02**:

`$ sudo tcpdump -i enp0s3`

Em **UE03**:

`$ sudo tcpdump -i enp0s3`

## 3. Testar serviço *ssh* (acesso remoto)

Test SSH

Use tcpdump

Cut SSH

`sudo /sbin/iptables –A INPUT –p tcp –-dport 22 –j DROP`

Use tcpdump

## 4. Testar serviço *http* (web)

Test Web

Use tcpdump

Cut Web

`sudo /sbin/iptables –A INPUT –p tcp –-dport 80 –j DROP`

`sudo /sbin/iptables –A INPUT –p tcp –-dport 443 –j DROP`

Use tcpdump

## 5. Redirecionar tráfego

`$ sudo /sbin/iptables -t nat -A PREROUTING -–dst 192.168.2.1 -p tcp --dport 22 –j DNAT  --to-destination 192.168.1.1`
