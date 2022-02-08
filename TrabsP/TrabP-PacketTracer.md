# Trabalho Prático - Packet Tracert Networking/IoT (20%)

*Este trabalho prático deve ser realizado no simulador Cisco Packet Tracer utilizado nas aulas práticas*

**Enunciado temporário. Pode sofrer alterações**

## Implementação de todas as componentes de uma rede de suporte a uma Empresa, incluindo equipamentos IoT.

**Descrição genérica do trabalho:**
1.	O objetivo principal é concretizar uma rede de uma empresa sediada em Lisboa e composta por três edifícios (edifício A, edifício B e fábrica C);
2.	São dois edifícios de 3 andares que alojam um total de 200 funcionários, estando previsto a duplicação do número de funcionários nos próximos 5 anos, caso a evolução da empresa se mantenha nos atuais níveis;
3.	Tendo os edifícios uma largura de cerca de 100m, o backbone dos edifícios é duplo, ou seja, dois bastidores por piso (devidamente espaçados), interligados a um lugar central no piso 1 do mesmo edifício. 
4.	O Datacenter fica localizado num quarto pequeno edificio, construído para o efetio, onde estão também centralizadas as comunicações.
5.	A infraestrutura central de rede e o acesso à Internet estão dentro do Datacenter.
6.	Os edifícios têm ainda a infraestrutura necessária para interligar diversas componentes de IoT para suporte à gestão inteligente do campus e dos edifícios.
7.	Todos os pisos têm disponíveis 4 pontos de acesso sem fios por piso.

**Objetivos a concretizar:**
1.	Elaborar um relatório de acordo com o template aqui disponibilizado.
2.	Deve escolher um negócio imaginário e caracterizar a empresa de forma adequada e justificada (máximo de duas páginas A4).
3.	O objetivo principal do trabalho é planear, instalar e configurar a rede necessária para servidores, postos de trabalho, portáteis/telemoveis e equipamentos IoT.
4.	Os mapas de rede deverão ser claros e organizados, eventualmente utilizando anotações necessárias para explicações necessárias.
5.	Deverão quantificar o número de switchs a colocar nos pisos dos edifícios, tendo em conta o número de funcionários da empresa e uma margem que considerem interessante para crescimento imediato. Os funcionários estão espalhados de forma muito semelhante pelos pisos 2 e 3. Os pisos 1 dos edifícios têm cerca de 50% dos funcionários dos restantes pisos em ambos os edifícios.
6.	Deverão escolher os equipamentos mais adequados a colocar nos pontos centrais dos edifícios e no Datacenter, sabendo que apenas existe routing no Datacenter.
7.	Os equipamentos devem ter as portas necessárias configuradas e com respetivas descrições.
8.	A escolha dos modelos dos equipamentos e sua respetiva configuração a nível de hardware é da responsabilidade dos grupos, que devem ser capazes de justificar as suas escolhas.
9.	Devem ser usadas, pelo menos, as seguintes VLANs, dependendo muito do negócio escolhido a necessidade de existirem mais:
9.1.	VLAN 10 – 10.10.10.0/24 – 2001:1:1:10::/64 – servidores (DHCP, DNS)
b.	VLAN 11 – 10.10.11.0/24 – 2001:1:1:11::/64 – servidores (Web, Mail, IoT)
c.	VLAN 20 – 10.10.20.0/24 – 2001:1:1:20::/64 – IoT
d.	VLAN 30 – 10.10.30.0/24 – 2001:1:1:30::/64 – Apoio Administrativo
e.	VLAN 31 – 10.10.31.0/24 – 2001:1:1:31::/64 – Financeira
f.	VLAN 32 – 10.10.32.0/24 – 2001:1:1:32::/64 – Recursos Humanos
g.	VLAN 33 – 10.10.33.0/24 – 2001:1:1:33::/64 – Marketing
h.	VLAN 34 – 10.10.34.0/24 – 2001:1:1:34::/64 – Direção
i.	VLAN 35 – 10.10.35.0/24 – 2001:1:1.35::/64 – Equipamentos portáteis / rede sem fios
j.	VLAN 40 – 10.10.40.0/24 – 2001:1:1:40::/64 – Laboratórios (ou algo adequado ao negócio)
k.	VLAN 41 – 10.10.41.0/24 – 2001:1:1:41::/64 – Investigação (ou algo adequado ao negócio)
