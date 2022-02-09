# Aulas de Laboratórios Práticos


1. Laboratório 1: Cisco Packet Tracer I 
2. Laboratório 2: Cisco Packet Tracer II
3. Laboratório 3: Routing I (com máquinas virtuais) 
5. Laboratório 4: Routing II (com NAT e acesso à Internet)
6. Laboratório 5: Captura de Tráfego numa Rede  
7. Laboratório 6: Cisco Packet Tracer III

## 0. Preparação dos Laboratórios / Pré-Requisitos

### 0.1 Instalação do Cisco Packet Tracer (Labs 1,3 e 6)

***Pré-requisito: Ter uma conta na [Cisco NetAcad](https://www.netacad.com)***

Para criar conta: Escolher Login, introduzir o endereço de mail e prosseguir. Quando for detetado que o mail não está registado aparece uma opção `Create New Account`. Esta conta será a mesma que deve ser utilizada no inicio do programa, depois de instalado.
Após criação da conta pode efetuar o download [aqui](https://www.netacad.com/portal/resources/packet-tracer)

Em Fev/2022 os requisitos e versões disponiveis eram as seguintes:

```
To successfully install and run Cisco Packet Tracer 8.1, the following system requirements must be met:

Cisco Packet Tracer 8.1 (64 bit):
Computer with one of the following operating systems: Microsoft Windows 8.1, 10, 11 (64bit), Ubuntu 20.04 LTS (64bit) or macOS 10.14 or newer.
amd64(x86-64) CPU
4GB of free RAM
1.4 GB of free disk space

 
Cisco Packet Tracer 8.1 (32 bit):    
Computer with one of the following operating systems: Microsoft Windows 8.1, 10, 11 (32bit)
x86 compatible CPU
2GB of free RAM
1.4 GB of free disk space
```

Existem versões para os seguintes sistemas operativos:
```
Windows Desktop Version 8.1.1 English
64 Bit Download
32 Bit Download
 
Ubuntu Desktop Version 8.1.1 English
64 Bit Download

macOS Version 8.1.1 English
64 bit Download
``` 

### 0.2 Instalação de Máquinas Virtuais em equipamentos dos alunos (Labs 2,4 e 5)

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

*Nota: É possível correr as máquinas dos SEED LABS na Cloud. [Neste repositório](https://github.com/seed-labs/seed-labs/blob/master/manuals/cloud/seedvm-cloud.md) da SEED Labs poderá verificar como o fazer. Não haverá suporte do Docente para esta configuração*

# Laboratórios
Para a calendarização prevista dos seguintes laboratórios, por favor ver as [datas](https://github.com/pmrosa-classes/ComputerNetworksEI#planeamento) no Planeamento Previsto 

## 1. Laboratório 1: Cisco Packet Tracer I 

- Apresentação do interface da ferramenta Cisco Packet Tracer
- Primeiras configurações do [Roteiro do Packet Tracer para as aulas Práticas](https://github.com/pmrosa-classes/ComputerNetworksEI/blob/main/AulasLabsPraticos/roteiro-packet-tracer.md)

## 2. Laboratório 2: Cisco Packet Tracer II 

Continuação das configurações do [Roteiro do Packet Tracer para as aulas Práticas](https://github.com/pmrosa-classes/ComputerNetworksEI/blob/main/AulasLabsPraticos/roteiro-packet-tracer.md)

## 3. Laboratório 3: Routing I 

Seguir os [seguintes](https://github.com/pmrosa-classes/ComputerNetworksEI/blob/main/AulasLabsPraticos/RoutingI.md) passos para a realização do laboratório.

## 4. Laboratório 4: Routing II

Seguir os [seguintes](https://github.com/pmrosa-classes/ComputerNetworksEI/blob/main/AulasLabsPraticos/RoutingII.md) passos para a realização do laboratório.

## 5. Laboratório 5: Captura de Tráfego numa Rede 

Seguir os [seguintes](https://github.com/pmrosa-classes/ComputerNetworksEI/blob/main/AulasLabsPraticos/CapturaTrafegoRede.md) passos para a realização do laboratório.

## 6. Laboratório 6: Cisco Packet Tracer III

- Utilização de dispositivos IoT na ferramenta Cisco Packet Tracer
- Configurações básicas de Servidor de IoT e equipamentos exemplo segundo o Roteiro do Packet Tracer para IoT
- Disponível brevemente

