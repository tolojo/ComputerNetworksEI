# Laboratório 5: Captura de Tráfego de Rede

O Laboratório 5 tem como objetivo:
- Introduzir os alunos à Captura de Tráfego de Rede
- 




Monitor network traffic

To monitor the network traffic, we may use VM2 (or another machine, e.g. a VM4, also connected to the network) to run tcpdump and capture all network traffic. Make sure you can detect ICMP packets originating at VM3 and with destination VM1 (using ping). Use tcpdump with options -X and -XX and identify the IP addresses, MAC addresses and protocol in a given packet. While still running /usr/sbin/tcpdump, open a telnet connection between VM1 and VM2 using user seed and password dees. Verify that you can capture both the username and password with tcpdump.

You have successfully eavesdropped communications… But what is the difference between executing telnet from VM1 to VM3 with and without NAT (in interface enp0s8 of VM2)? Use tcpdump to analyse the output and compare the differences.

You might want to run

$ sudo tcpdump -i enp0s3   # on VM1
$ sudo tcpdump -i enp0s3   # on VM2
$ sudo tcpdump -i enp0s8   # on VM2
$ sudo tcpdump -i enp0s8   # on VM3



