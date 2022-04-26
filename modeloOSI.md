## MODELO OSI

| Camada osi |            
|  --------  |
|7 Aplicação |
|6 Apresentação|
|5 Sessão |
|4 transporte |
|3 Rede |
|2 Link de dados|
|1 Fisica|



**Camada -1 fisica**

Relaciona-se com o hardware da rede, define questoes ligadas a voltagem e a velocidade de transmissão. além de tratar da construção dos equipamentos de rede.  

**Camada -2 enlace**

Quebra as mensagens em quadros de dados, sempre que um receptor recebe um desses quadros, emite de volta uma mensagem de confirmação e o transmissor então envia o próximo.  

Além de controlarem a velocidade da transmissão de dados de um dispositivo rápido para outro mais lento.  

**camada -3 de rede**

Controla o direcionamento do fluxo de dados na condução da informação pela rede. Possibilita que os dados passem por vários pontos até serem entregues no destino.  

Controla rotas e escolhe os melhores caminhos. Leva em consideração a distancia mais curta, congestionamentos ou falhas ocasionadas pelo desaparecimento de um ponto de passagem na rota.  

Esta camada possibilita a comunicação entre sub-redes.  


**Camada -4 transporte**

Tem a função de redecer dados da camada de rede e fracioná-los em pedaços menores, se isso for necessário.  

Organiza os pacotes e os entrega na sequencia correta, livres de erros, uma vez que durante a transmissão podem seguir caminhos diferentes, se perderem e ainda chegarem fora de ordem ao destino.  


**Camada -5 sessão**

Administra a sessão, estabelece quando a comunicação se inicia e quando termina. Controla o diálogo entre a comunicação dos dispositivos.  

**Camada -6 apresentação**

Realiza a tradução de formado de dados entre máquinas que utilizam formatos diferentes.

Ex: A codificação de caracteres do padrão ASCII, ABCDIC.  
Essa codificação é realizada e convertida em várias interpretações para que a informação recebida seja a identica á que foi transmitida.  

**Camada -7 aplicação**

São protocolos de alto nível que possibilitam que softwares do mesmo tipo troquem informações.

Este nível da rede é responsável pelo formato do conteúdo dos pacotes que estão sendo transmitidos.  

É constituido de softwares que interagem com o usuário, pois entrega o recurso ao cliente do serviço, se seguirmos o conceito de tshoot da cisco TOP-DOWN é a primeira camada a ser tratada, porém como cliente do serviço, está no fim da rede.  
