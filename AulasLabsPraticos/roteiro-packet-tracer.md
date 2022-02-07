
# Aulas Práticas com Cisco Packet Tracer
VLANs/Routing/NAT/IPv4/DHCPv4/IPv6/DHCPv6
Pedro Rosa (pedro.rosa@universidadeeuropeia.pt)

Diagrama e sintaxe do exercício a realizar durante as aulas práticas com o software Cisco Packet Tracer
Nota: a forma exata de implementação pode variar devido a alterações realizadas durante as aulas.

## Diagrama da Rede a configurar nas Aulas Práticas
![alt text](roteiro-imagem.png)


## Configurações iniciais

Entrar em modo privilegiado
enable

Entrar em modo de configuração
`config terminal`

Atribuir nome ao equipamento

`hostname Router1 `

Atribuir domínio ao equipamento

`ip domain-name universidadeeuropeia.pt`

Password de enable
enable secret “password”

Gravação de configurações
copy running-config startup-config
