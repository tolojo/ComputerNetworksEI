# Aulas de Laboratórios Práticos (40%)


1. Trabalho de Routing I com máquinas virtuais (5%)
2. Análise de ficheiro pcap (captura de pacotes com Wireshark/tcpdump) (10%)
3. Trabalho de Routing II com NAT e acesso à Internet (5%)
4. Instalar o Nagius (5%)
5. Trabalho Cisco Packet Tracer com IoT (20%)

## Instalação de Máquinas Virtuais (em equipamentos dos alunos)

Para as aulas práticas iremos utilizar os materiais do ***[SEED Labs Project](https://seedsecuritylabs.org/)***, mais precisamente a máquina virtual ***SEEDUbuntu16.04***.

In this document we will provide two ways of running this VM:
(a) Locally on your machine, or
(b) using the virtualization system provided by RNL (labs in Alameda).

We strongly suggest the former.

1. Install SEED Locally on your machine

Download the Pre-built Virtual Machine Images (Ubuntu) from SEED Labs Project. We suggest the one built in June 2019.
Unzip the file.
Files will be included in folder SEEDUbuntu-16.04-32bit.
Follow the instructions.
Step2: You can give whatever name you want to your machine (and a folder with that name will be created)
Step4: To keep your disk organized, you may move the files from the folder created in 2.1 to the folder that was just created prior to performing Step4.
Step5: It is important that you select Graphics Controller: VBoxVGA otherwise you might have a small resolution.
Start the VM. user:pass/seed:dees,
Recommended: Change the user password.
Recommended: Update the system. sudo apt update; sudo apt upgrade
Optional: Change keymap to PT. setxkbmap pt
Troubleshooting

If you have problems with the Guest Additions (screen resolution, unable to copy host to guest, etc) you might want to have a look in here.
