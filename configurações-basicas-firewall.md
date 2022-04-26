# CONFIGURAÇÕES BÁSICAS FIREWALL

## Tabelas IPTABLES

O iptables organiza suas regras em uma estrutura que contém tabelas e cadeias. As tabelas são um agrupamento de cadeias em um nível mais alto, e terminam a grosso modo o escopo das regras que serão criadas. O iptables possui três tabelas ou listas.

**filter** - Tabela padrão para manipular pacotes de rede, usada para configurar politicas para o tráfego que entra, atravessa ou sai do computador.

**NAT** Usada para alterar pacotes que criam uma nova conexão, e para redirecionar conexões para NAT.

**MANGLE** Isada ára tipos especificos de alteração de pacotes, como a modificação de opções de cabeçalho IP de um pacote.

**raw** Marca pacotes que não devem ser manipulados pelo sistema de rastreamento de conexões.


Uma tabela contém cadeias, e as cadeias contém regras, como podemos ver a seguir.


##Tabela 1

| Cadeia 1 |            
| -------- |
|- Regra 1 |
|- Regra 2 |
|- Regra 3 |
|- regra n |


| Cadeia 2 |
| -------- |
|- Regra 1 |
|- Regra 2 |
|- Regra 3 |
|- regra n |

## Divisões das cadeias em tabelas

**Tabela Filter**: <p>Cadeias INPUT, OUTPUT, FORWARD</p>
**Tabela NAT**: Cadeias PREROUTING, OUTPUT, POSTROUTING
**Tabela Mangle**: Cadeias PREROUTING, OUTPUT, POSTROUTING, INPUT, FORWARD.
**Tabela Raw**: Cadeias PREROUTING E OUTPUT
**Tabelas security**: Usada para regras de rede MAC(Mandatory Access Control)

## Cadeias

As regras são organizadas em grupos denominados cadeias **(chains)**, que por sua vez ficam contidas nas tabelas. Uma cadeia é então um conjunto de regras usadas para verificar a correspodencia de um pacote de forma sequencial. Um pacote é verificado junto ás regras na chain, e se não há correspondencia, a proxima regra na ordem é verificada. Quando um pacote corresponde a uma regra na cadeia, a ação associada a essa regra é executada ao pacote, a regra padrão **(policy)** será aplicada.

**INPUT** - Aplica regras aos pacotes de rede que chegam ao servidor.
**OUTPUT** - Aplica regras aos pacotes de rede originados e que partem do servidor.
**FORWARD** - Aplica regras aos pacotes de rede roteados através do servidor **(para outro servidor ou outra interface de rede no mesmo servidor)**
**PREROUNTING** - Altera pacotes de rede quando eles chegam e antes do roteamento. Usado para DNAT **(Destination NAT)**.
**POSTROUTING** Altera pacotes de rede após o roteamento, usado para SNAT **(Source NAT)**


## CAMADA OSI

| Camada osi |            
|  --------  |
|7 Aplicação |
|6 Apresentação|
|5 Sessão |
|4 transporte |
|3 Rede |
|2 Link de dados|
|1 Fisica|
