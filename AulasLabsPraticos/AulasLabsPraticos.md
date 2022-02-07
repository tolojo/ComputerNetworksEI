# Aulas de Laboratórios Práticos (40%)


1. Trabalho de Routing I com máquinas virtuais (5%)
2. Análise de ficheiro pcap (captura de pacotes com Wireshark/tcpdump) (10%)
3. Trabalho de Routing II com NAT e acesso à Internet (5%)
4. Instalar o Nagius (5%)
5. Trabalho Cisco Packet Tracer com IoT (20%)

## 0. Instalação de Máquinas Virtuais (em equipamentos dos alunos)

***Pré-requisito: VirtualBox instalado em Windows, MacOS, Linux.***

Para as aulas práticas iremos utilizar os materiais do ***[SEED Labs Project](https://seedsecuritylabs.org/)***, mais precisamente a máquina virtual ***SEEDUbuntu16.04***.
Esta [página](https://seedsecuritylabs.org/labsetup.html) na secçãoo Ubuntu 16.04 estão vários links para download (pode fazer a partir [daqui](https://drive.google.com/file/d/12l8OO3PXHjUsf9vfjkAf7-I6bsixvMUa/view?usp=sharing)) da imagem e do [manual de instalação](https://seedsecuritylabs.org/Labs_16.04/Documents/SEEDVM_VirtualBoxManual.pdf) para o VirtualBox.

Instruções resumidas (podem não dispensar a consulta do manual referido anteriormente):

1. Efetuar o download da imagem da máquina virtual em Linux/Ubuntu 16.04
2. Descomprimir o ficheiro
3. Criar uma Máquina Linux no VirtualBox com o nome que pretender (poderá desejar acrescentar ...01 no final, uma vez que necessitará de várias máquinas)
4. Escolher preferivelmente a placa gráfica VBoxVGA
5. Iniciar a máquina virtual (credenciais - user:seed; password:dees)
6. Atualizar o sistema operativo: sudo apt update; sudo apt upgrade
7. Atualizar o teclado para português: setxkbmap pt

