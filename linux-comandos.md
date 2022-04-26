
    
# ESTRUTURA DO LINUX.

    • / Raiz do sistema operacional (análogo ao “C:” de um sistema Windows).
    • /boot Contém arquivos necessários para a inicialização do sistema.
    • /etc Arquivos de configuração do sistema e de serviços de rede (pacotes) instalados (por padrão).
    • /bin Contém os programas/comandos básicos do sistema para uso dos usuários.
    • /sbin Contém os programas/comandos acessíveis pelo super usuário (root) para administração do sistema.
    • /var Contém os logs do sistema e dados de spool de impressora e cache.
    • /root Diretório do usuário root, o administrador do sistema.
    • /home Diretório que contém os subdiretórios de cada usuário (análogo ao “Users” ou o antigo “Documents and Settings”).
    • /dev Permite acesso aos dispositivos do sistema.
    • /lib Bibliotecas compartilhadas pelos programas do sistema e módulos do kernel.
    • /proc Sistema de arquivos do kernel. Este diretório não existe em seu disco rígido, ele é criado pelo kernel e usado por
    diversos programas que fazem sua leitura. Através de seu conteúdo podemos verificar configurações do sistema ou
    modificar o funcionamento de dispositivos através de alterações em seus arquivos (como a função de roteamento).
    • /usr Contém arquivos e aplicativos de usuários do sistema, “documentações” do sistema, entre outros tipos de arquivo.
    
    
 -------------------------------------------------------------------   
    
    
    |Syntaxe linux|
    |comando |origem |destino|
    |mv /origemnome  /destino |

## COMANDOS BÁSICOS

**ls** - lah  visualizar lista completa
**cd** - mudar diretorio, navegar entre eles
**pwd** - saber onde você está
**mkdir** - cria pasta
**rm** - deleta arquivo
**rm -r** deleta pasta modo recursivo
**tree -** forma uma arvore bonitinha
**mv** - para mover
**cp** - para copiar
**find** - para procurar
**touch** - para criar 

## VISUALIZADORES

**more** - visualização
**less** - eu achei melhor que o more, pois conseguir ir e voltar.
**head** - para pesquisar as primeiras 10 linhas
**tail** -f - para pesquisar as ultimas 10 linhas

## Redirecionadores

> . legal para extrair relatorio exp ls -l / > nomedoarquivo.txt
>> se usar >> ele concatena ao arquivo
du -hs *  >> /root/ok.txt 2>> /root/erro.txt

## Concatenação de comando, conectores e operadores.

**ls -l /etc | less**
**;** conectores
**&&** operadores
**||** = boolean True ou false.

## Filtros de conteudo.

**grep** - Pesquisa em arquivos ou em sua entrada padrão por uma sequência de caracteres informada.
• grep <opções> [string_ou_regex_desejada] [arquivo ou caminho]
• Ex.: grep “root” /etc/passwd
• Ex.: cat /etc/passwd | grep “root”
• Os dois comandos acima apresentam o mesmo resultado (procura pela string “root” dentro do
arquivo “/etc/passwd”), porém, no primeiro exemplo especificamos o arquivo e no segundo exemplo
filtramos a sua entrada padrão.
• Com o comando “grep” (ou “egrep”), também podemos utilizar expressões regulares, caracteres
curinga e “meta caracteres” (expressões regulares), criando inúmeras possibilidades.
• Meta caracteres: São símbolos e caracteres literais com função específica (mais detalhes no slide
sobre expressão regular).

Vamos supor que desejamos listar apenas os subdiretórios de um determinado
diretório... O que fazer?
• Ex.: ls -l /lib | grep ^d
• No caso acima, utilizamos um meta caractere (o “^”, que representa o início da linha). Portanto, o
“grep” filtrou toda linha que começa com “d”.
• Ex.: ls -l /lib | grep d
• Já neste exemplo, o “grep” filtraria todas as linhas que contém a letra “d” em qualquer parte da linha,
ou seja, o objetivo não seria alcançado.
• Agora vamos supor que desejamos listar todo o conteúdo, exceto subdiretórios... Aí
está um grande recurso do **“grep”**:
• Ex.: ls -l /lib | grep -v ^d
• O parâmetro **“-v”** exibe o inverso do que foi solicitado, ou seja, vamos visualizar todo o conteúdo,
exceto diretórios.

Uma opção muito utilizada é o **“-r”**, que nos permite realizar a busca de uma
determinada string de forma recursiva:
• Ex.: grep -r root /etc
• Lembre-se que podemos concatenar comandos, caso a saída seja extensa.
• Ex.: grep -r root /etc | more
• Ex.: grep -r root /etc | less
• Podemos verificar apenas os arquivos e diretórios que foram criados/modificados
em 2022:
• Ex.: ls -l /etc | grep 2022
• Agora desejamos visualizar apenas os arquivos criados/modificados em 2021:
• Ex.: ls -l /etc | grep -v ^d | grep 2021

Também é importante sabermos que além do **“grep”**, temos:
• **egrep** é o mesmo que “grep -E” (Interpreta o padrão de busca como uma expressão regular
extendida);
• **zgrep** Realiza a busca dentro de arquivos compactados com o padrão “gzip”;

## Filtros de comando WC

O comando **“wc”** (acrônimo de “word count”) realiza a contagem da quantidade de linhas, palavras ou caracteres de um determinado arquivo ou entrada padrão:
• Ex.: ls -l /etc | wc -l
• No exemplo acima, o “wc” tem como entrada padrão a listagem do diretório “/etc”. O parâmetro “-l”
realiza a contagem de linhas.
• Ex.: cat /etc/passwd | wc -l
• Ex.: wc -l /etc/passwd
• Ambos acima realizam a contagem de linhas do arquivo “/etc/passwd”.
• Vamos supor que desejamos saber a quantidade de subdiretórios contidos em
“/etc”
• Ex.: ls -l /etc | grep ^d | wc -l

Dentre as principais opções do comando “wc”, temos:
• “-l”  Contabiliza a quantidade de linhas;
• “-w”  Contabiliza a da quantidade de palavras;
• “-m”  Contabiliza a quantidade de caracteres;
• “-c”  Contabiliza a quantidade de bytes;
• Para contabilizar em apenas um comando a quantidade de linhas, palavras e
caracteres, utilizamos o “wc” sem parâmetros:
• Ex.: wc /etc/passwd

## Filtros comando tr

O comando “tr” traduz e/ou deleta caracteres da entrada padrão e exibe o
resultado como saída:
• Ex.: cat /etc/passwd | tr : ;
• No exemplo acima, o “tr” irá “traduzir” (converter) todos os caracteres “:” para “;”.

Ex.: ls -l /etc | tr -s “ ”
• O “tr” também “comprime” (squeeze) caracteres repetidos. No exemplo acima, todos os locais que
houver mais de um espaço são removidos (execute em sua VM para testar)

## Filtros comando diff
diff Compara o conteúdo de dois arquivos e exibe as diferenças:
• diff <opções> [arquivo1] [arquivo2]
• Ex.: diff /etc/yp.conf /etc/yp.conf-bkp

• Comando muito útil para compararmos as modificações realizadas em um arquivo
de configuração com o arquivo original ou backup, caso o serviço apresente
problemas após as modificações.

## Filtros comando sort

O comando “sort” ordena alfabeticamente um determinado arquivo ou entrada
padrão:
• Ex.: cat /etc/passwd | sort
• Ex.: sort /etc/passwd
• Ambos acima enviam para a saída padrão (tela) o conteúdo do arquivo “/etc/passwd” em ordem
alfabética.
• Caso seja feita uma auditoria no setor de TI, solicitando uma lista com todos os
usuários que possuem “shell válido” no Linux...
• Ex.: cat /etc/passwd | grep “/bin/bash” | cut -d ‘:’ -f 1 | sort
• Ex.: sort /etc/passwd | grep “/bin/bash” | cut -d ‘:’ -f 1
• Ambos acima enviam para a saída padrão (tela), apenas o “login” dos usuários que possuem “shell
válido”.

## O famigerado AWK

O comando “awk” possui função semelhante ao “cut”, porém, com muitas
possibilidades adicionais:
• Ex.: awk -F: ‘{ print $1 }’ /etc/passwd
• O comando acima separa os dados contidos no arquivo “/etc/passwd”, utilizando como delimitador de
cada campo de informação, o caractere ‘:’ e exibe o primeiro campo de cada linha “$1”.
• Ex.: ls -lh /var/log/ | awk -F “ ” ‘{ print “Nome do arquivo: ” $9 “ - Tamanho: ” $5 }’
• O comando acima lista o conteúdo do diretório “/var” e envia a saída para o “awk” filtrar e exibir de
forma customizada, somente o nome e o tamanho do arquivo.

**- awk**
    awk [ -F separador] [ -v var=valor ] [ 'programa' | arquivo-com-programa] [ arquivo...] 
    1- diretamente pelo terminal. 
        awk 'BEGIN {print "Meu Primeiro Script AWK"}'


    2- No terminal, mas lendo arquivo separado.
        echo 'Meu Primeiro Script AWS' > primeiro.txt
        awk '{print}' primeiro.txt


    3- No terminal, mas lendo um arquivo separado e um programa separado.
        echo 'Meu Primeiro Script AWK' > primeiro.txt
        echo '{print}' > programa
        cat programa
        {print}
        awk -f programa primeiro.txt   
        
    4- Tudo num programa executável AWK
        echo -e '#!/user/bin/awk -f \nBEGIN {print "Meu Primeiro Script AWK"}' > programa.awk
        cat programa.awk
            #!/user/nin/awk -f
            ./programa.awk
            Meu primeiro Script AWK
                * obs: O -f na shebang ( O -f tem o f de file )

    As variáveis no AWK possuem diversos segmentos, o AWK classifica cada coluna
    como um número, sendo que o número zero é o proprio arquivo.
                Exemplos
        
        $1      $2      $3      $4          $5
       Cultivo  Produ   Fruto   Semente     Severidade

       Declarando variaveis em awk;
       awk 'BEGIN { nomedavariavel = "AWK é chato" ; print nomedavariavel }'

       - Variaveis Internas
            ARGV - Vetor contendo parametros passados para o programa
            FILENAME - Nome do arquivo de entrada atual
            FNR - Número do registro no arquivo atual
            FS - Separador de campos. Seu padrão é branco e TAB
            NR - Quantidade de registros do arquivo em processamento.
            OFMT - Formato de saida para números. Seu padrão é %6g
            OFS - Separador de campos na saida. Seu padrão é branco
            ORS - Separador dos registros de saida. Seu padrão é newline
            RS - Separador de registros de entrada. Seu padrão é newline.



            https://www.youtube.com/watch?v=j0Qm6CzbNbg

        awk '{print $3, $1}' tabela.txt  
        awk 'OFS = ' "> \t\t" {print $2, $1}' original-langs.txt  

## - sed
O editor sed é utilizado em quase 100% da sua utilização para efetuar substituição e/ou alteração
em um arquivo. Sua estrutura de utilização como comunmente ele é utilizado é:
    sed [opcao(s)] regras/comandos [arquivo] [...]

    sed - é o comando no terminal
    opção - parametro que pode ser passado pro sed, e podemos passar mais de uma opção ou parametro
    regras - Também podem ser chamados de comandos do sed, são ações realizadas no sed, exp substituição, imprimir, manipular de forma especifica etc....
    arquivo - Na maioria dos casos precisamos informar um arquivo pro Sed, para que ele o manipule, o arquivo só não precisa ser informado
              se o sed recebe os dados de saida de outro programa via canalizacao por pipe. E podemos passar mais de um arquivo pro Sed.

              Exemplos
              sed - n 'p' distros.txt

              Gentoo
              FreeBSD
              GNU/Hurd
              Slackware
              VoidExherbo
              Debian
              Ubuntu

              Lista Detalhada de todos os Comandos do Sed
               = - imprime o número da linha e depois a linha;
              
              -n = - com supressão, só os número das linhas, usando o -n;
               # - insere comentário (pode ser no prompt ou no arquivo);
              
              ! - inverte a lógica da regra (sed -n '1!p' distros.txt);
              
              ; - separa regras (sed -n '1p;2p' distros.txt);
              
              , - separa faixas de endereço (sed -n '4,6p' distros.txt);

               q - sai da Execução do comando (sed '/G/q' distros.txt);

              { } - inicia e finaliza bloco de regras (sed '/Void/{p;q;}' distros.txt);

               s - substitui um trecho de texto por outro (sed -n '/S/{p;q;}' ou sed -n ‘/Sl/{p;q}’ );

               y - traduz um caractere por outro ( sed 'y/Saoeb1/54038i/' distros.txt );

               d - apaga a linha que possui o conteúdo ( sed '/Gentoo/d' distros.txt );
              
              i - insere um texto ANTES da linha que deseja (sed '/Gentoo/i Mint' distros.txt);

              1i - insere na linha que deseja (sed '1i Mint' distros.txt ou sed ‘3i Mint’);

              c - substitui parte de um arquivo por um texto, troca tudo da linha entre a a linha que
              possui a palavra Gentoo até a linha que possui a palavra Slackware
              ( sed '/Gentoo/,/Slackware/c 4 distros estavam em 4 linhas' distros.txt ) ;

              As versões anteriores a 3.02a do GNU Sed, era necessário quebrar a linha ( \ ) pra que funcionasse essa regra c
              (também com a e i)

               a - insere um texto DEPOIS da linha que deseja (sed '/Gentoo/a Nova Distro' )
              (sed '3aNova Distro' , similar ao i só que N + 1 );
              
              l - mostra um $ no final do conteúdo que é da IMPRESSÃO NORMAL
              (sed l distros.txt);

               n - vai para próxima linha (sed -n '1{n;p}' distros.txt) , obs.: o N maiúsculo faz o mesmo, no
              entanto existe uma diferença, entenderemos melhor quando falarmos dos espaços padrão e reserva no
              próximo capítulo. Assim como o P MAIÚSCULO que também imprime igual ao p minúsculo, mas a segunda
              linha do ESPAÇO PADRÃO.;

https://linuxconfig.org/learning-linux-commands-sed

## Compactadores - ZIP.

**zip**  Permite compactar arquivos no formato “zip” (Padrão PKZIP e Winzip
    utilizado no Windows).
    • zip <opções> [caminho_do_arquivo.zip] [arquivos_a_ser_compactados]
    • Ex.: zip -r dados.zip /etc/
    • O comando acima realiza a compactação do diretório “/etc” e todo o seu conteúdo, dentro do novo
    arquivo de nome “dados.zip”.
    • O parâmetro “-r” permite compactar de forma recursiva.
    • unzip  Permite descompactar arquivos no formato “zip” ou apenas listar o
    conteúdo contido no arquivo compactado (parâmetro “-l”).
    • unzip <opções> [caminho_do_arquivo.zip] <opções> <destino>
    • Ex.: unzip dados.zip
    • Descompacta o conteúdo de “dados.zip” no diretório corrente.
    • Ex.: unzip dados.zip -d /root/bkp-etc/
    • Descompacta o conteúdo de “dados.zip” no diretório “/root/bkp-etc”.


## Compactadores - TAR.

tar - Permite dois tipos de tarefas:  
• Empacotar dados em um arquivo sem realizar compactação “efetivamente”;  
• Compactar/Descompactar arquivos utilizando o padrão “gzip”.
• O objetivo de empacotar é viabilizar a distribuição de pacotes de instalação de Softwares, publicando
apenas um arquivo ao invés dos diversos arquivos necessários para a instalação do Software.  
• Ao compactar/descompactar através do comando “tar”, podemos utilizar três tipos de
compactadores:  
• “gzip”  extensão “tar.gz” (mais utilizado e eficiente na compressão);  
• “bzip2”  extensão “tar.bz2”  
• “compress”  extensão “tar.Z”  

**tar Sintaxe:**
• tar <opções> [arquivo] <opções || caminho_a_ser_compactado>
• No próximo slide teremos exemplos de sintaxe. Portanto, vamos conhecer as principais opções e
possibilidades de uso:  
• c - Compacta ou empacota dados em um novo arquivo;  
• x - Extrai o conteúdo de um arquivo compactado;  
• t - Lista o conteúdo de um arquivo compactado;  
• v - Exibe na tela o que está sendo compactado ou descompactado;  
• p - Preserva as permissões do arquivo de origem;  
• r - Acrescenta arquivos dentro do pacote “tar”;  
**• z - Modo de operação com o comando compactador “gzip”;**   
**• Z - Modo de operação com o comando compactador “compress”;** 
**• j - Modo de operação com o comando compactador “bzip2”.**  
**• f - Modo de operação com arquivos.**

**tar** - Sintaxe para compactar (com o compactador “gzip”):
• Ex.: tar czf arquivo.tar.gz /etc/
• Compacta o diretório “/etc” e seu conteúdo, utilizando o compactador GZIP, dentro de um novo
arquivo (arquivo.tar.gz).
• tar  Sintaxe para compactar (com o compactador “bzip2”):
• Ex.: tar cjf arquivo.tar.bz2 /etc/
• Compacta o diretório “/etc” e seu conteúdo, utilizando o compactador BZIP2, dentro de um novo
arquivo (arquivo.tar.bz2).

tar - Sintaxe para empacotar:
• Ex.: tar cf empacotado.tar /etc/
• “Agrupa”/”Empacota” o diretório “/etc” e seu conteúdo dentro de um novo arquivo (empacotado.tar),
sem comprimir os dados.
• tar - Sintaxe para descompactar (com o compactador “gzip”):
• Ex.: tar xzf arquivo.tar.gz
• Descompacta o conteúdo do “arquivo.tar.gz” no diretório corrente.
• tar  Sintaxe para descompactar especificando o diretório:
• Ex.: tar xzf arquivo.tar.gz -C /diretorio/destino/desejado/
• Descompacta o conteúdo do “arquivo.tar.gz” no diretório especificado.

## Informações de sistema e software.

• **uname** - Exibe informações sobre o sistema instalado, incluindo a versão do
Kernel:
• Ex.: uname -a

**uptime** - Exibe um resumo de informações sobre o sistema como:
• Hora atual;
• Tempo que o sistema está em execução (“up”, “no ar”);
• Quantidade de usuários logados;
• “Load Average”, que mostra quantos processos em média estão aguardando (na fila) para serem
executados, sendo que as separações por “vírgula” representam os intervalos de tempo de 1, 5
e 15 minutos.

**free** - Exibe informações sobre a utilização da memória RAM e SWAP.
• Ex.: free -m
• O parâmetro “-m” exibe a utilização em MB, da mesma forma que “-g” ou “-k” podem ser utilizados
para exibição em GB e KB respectivamente.
• OBS.: A coluna “shared” não deve ser considerada.
• Podemos executar o “free -s 10”, para atualizar o status do consumo de memória a cada 10
segundos.
• Para obter mais informações sobre o uso da memória, podemos acessar o arquivo “/proc/meminfo”.
Ex.: cat /proc/meminfo

• **df** - Exibe informações sobre o espaço livre/utilizado em disco:
• Ex.: df -h
• O parâmetro “-h” exibe de forma “inteligível” (humam readable)

**file** - Exibe o tipo de um determinado arquivo (se o mesmo é texto, imagem,
    arquivo compactado, entre outros).
    • Ex.: file <nome_do_arquivo>

**w**- Exibe a saída do comando “uptime” e informações sobre os usuários
conectados, como tempo ocioso e processo que este usuário está executando

**who** - Exibe quais usuários estão logados no sistema, qual o “terminal” este
usuário está conectado, data e hora do Logon, e por fim, o IP de origem desta
conexão (caso seja uma conexão remota).

**whoami**- Exibe qual o nome do usuário logado no terminal atual:

## Configuração e comandos de redes

Para solicitar um IP via DHCP, temos os comandos “ifdown” + ”ifup” ou o “dhclient”:
• Ex.: ifdown <interface> (para desabilitar) + ifup <interface> (para habilitar).
• Ex.: dhclient ou dhclient <interface>
• Para identificar as suas interfaces de rede, execute “ifconfig” ou “ip addr”.

**ifconfig** - Permite verificar o IP atual ou configurar um IP para um determinado
adaptador de rede:
• Ex.: ifconfig <interface>
• O comando acima apenas verifica o IP de uma determinada interface;

Ex.: ifconfig <interface> [X.X.X.X] netmask [Y.Y.Y.Y]
• O comando acima atribui um IP a uma determinada interface;

**route** - Permite visualizar ou modificar rotas ou o “Default Gateway”:
• Ex.: route add default gw [X.X.X.X]
• Define o “Default Gateway”;

Ex.: route -n
• Apenas exibe as rotas existentes;

O comando “ip” possui diversas opções (chamadas de objetos), que permite ver e
alterar configurações de rede, roteamento e tunelamento.
• Apenas para se ter uma ideia da quantidade de opções, segue um print do manual
do comando “ip” (resultado do “man ip”) com os objetos e opções disponíveis:

A principal utilidade do comando é definir um endereço IP. Segue exemplo:
• Listando as interfaces. Ex.: ip address ou ip addr list ou ip addr

Definindo endereço IP na interface “enp0s3”. Ex.: ip address add x.x.x.x/mask dev <interface>

Listando somente a interface “enp0s3” e seu IP. Ex.: ip address list enp0s3 ou ip addr list enp0s3

A remoção de um endereço IP possui sintaxe similar, tendo duas possibilidades:
• Remover todos os endereços de uma interface (caso tenha mais de um IP):
• Ex.: ip address flush dev enp0s3

* Informações de rede Comando ip route

ip route
• Apenas exibe as rotas existentes;


## Informações sobre Hardware

**dmesg** exibe todo o Hardware reconhecido/carregado pelo kernel durante a
inicialização.

**lspci** - exibe informações do chipset e dispositivos PCI:

Para instalar/desinstalar dispositivos que o sistema não reconheça
automaticamente, devemos realizar o download do módulo (driver) do dispositivo a
ser instalado e utilizar os comandos abaixo:
• **lsmod** - exibe os módulos (drivers) carregados no sistema:
• Ex.: lsmod
• **insmod** - Instala/carrega um novo módulo no Kernel.
• Ex.: insmod [arquivo] <opções>
• rmmod  Remove um módulo (devemos ter cautela na realização do mesmo,
tendo em vista que ao remover um módulo, “desativamos” o hardware associado ao
módulo);
• Ex.: rmmod <nome_do_modulo>

**proc**
O diretório “/proc” é um diretório virtual do sistema Linux com algumas
características importantes:
• É um diretório utilizado exclusivamente pelo kernel para gerenciamento do sistema e seus
recursos;
• Existe apenas enquanto o computador está ligado;
• Possui diversos arquivos com o tamanho de 0 bytes, porém, podemos encontrar conteúdos
nestes arquivos;
• O maior arquivo deste diretório se chama “kcore”, que possui tamanho próximo ao disponível na
memória RAM;
• Não podemos gravar ou criar arquivos neste diretório.

Através do diretório “/proc”, podemos:
• Obter informações do processador  Ex.: cat /proc/cpuinfo
Listar os dispositivos IDE conectados  Ex.: ls -l /proc/ide

Para informações sobre armazenamento
fdisk -l

## - top.

Este utilitário exibe informações sobre os processos que estão sendo executados.

    Algumas opções do comando
    -c : mostra a linha de comando ao invés do nome do programa.
    -d num : atualiza a tela após num segundos (o padrão é 5 segundos).
    -h : exibe as opções do utilitário.
    -p pid : mostra apenas o processo com o PID especificado
    -v : mostra informações sobre o utilitário.
    Teclas do aplicativo
    espaço : atualiza imediatamente a tela.
    h : ajuda.
    k : encerra um processo (comando kill). Será solicitado o PID do processo e o sinal a ser enviado ao processo. O sinal 15 provoca o término normal do processo, enquanto o sinal 9 provoca o término forçado do processo. O padrão é o sinal 15 (SIGTERM).
    M : ordena processos de acordo com o uso da memória.
    n ou # : altera a quantidade de processos a serem apresentados na tela. É solicitada a entrada de um número. O valor padrão é zero que corresponde ao número de processos que a tela pode suportar.
    P : ordena processos de acordo com o uso de CPU.
    q : encerra o aplicativo.
    r : altera a prioridade de um processo (comando renice). Será solicitado o PID do processo e o valor da nova prioridade a ser usada pelo processo (o valor padrão é 10). O usuário comum só pode informar um valor positivo maior que a prioridade atual. O root pode informar qualquer valor entre -20 (maior prioridade) e 19 (menor prioridade).
    s : altera o tempo entre as atualizações de tela. É solicitada a entrada do tempo de espera em segundos. O valor zero corresponde a atualização contínua. O padrão é 5 segundos.
    T : ordena processos de acordo com o tempo de execução.
    u : exibe os processos de um determinado usuário. É solicitada a entrada do nome (login) do usuário. O padrão é branco (todos os usuários).
    Exemplos
    O comando
    top -d 10

    inicializa o aplicativo top e atualiza as informações apresentadas a cada 10 segundos.



    Para ver apenas as informações do processo 1 (init), digite
    top -p 1



    Observações
    Os comandos ps e pstree também exibem informações sobre os processos.
    O aplicativo htop é similar ao top, mas oferece paginação dos processos (permite ver todos os processos do sistema) e diversas outras melhorias.

## - htop

O Htop é uma ferramenta visual e interativa (ela recebe interação até pelo mouse) para visualizar os processos e os recursos consumidos por eles. Na versão 2.0 o Htop se tornou multiplataforma, sendo suportado por Linux, FreeBSD, OpenBSD e MacOS.
    https://www.treinaweb.com.br/blog/monitorando-processos-com-o-htop


## - atop

We’re all familiar with top, a real-time system monitor. Some prefer htop and previously, I mentioned iotop for use with storage read/write monitoring. Let’s looks at another popular tool for Linux server performance analysis: atop.
    Advantages of atop
    Atop is an ASCII full-screen performance monitor which can log and report the activity of all server processes. One feature I really like is that atop will stay active in the background for long-term server analysis (up to 28 days by default). Other advantages include:

    Shows resource usage of ALL processes, even those that are closed/completed.
    Monitors threads within processes & ignores unused processes.
    Accumulates resource usage for all processes and users with the same name.
    Highlights critical resources using colors (red).
    Will add or remove columns as the size of the display window changes.
    Includes disk I/O and network utilization.
    Uses netatop kernel module to monitor TCP & UDP and network bandwidth.
    Once atop is launched, by default, it will show system activity for CPU, memory, swap, disks, and network in 10-second intervals. In addition, for each process and thread, you can analyze CPU utilization, memory consumption, disk I/O, priority, username, state, and even exit codes.
    https://haydenjames.io/use-atop-linux-server-performance-analysis/

        sing atop – system & process monitor
    A good place to start would be to read the man pages:

    man atop
    Other useful commands:

    Launch with average-per-second total values:

    atop -1
    Launch with active processes only:

    atop -a
    Launch with command line per process

    atop -c
    Launch with disk info

    Datadog
    atop -d
    Launch with memory info

    atop -m
    Launch with network info

    atop -n
    Launch with scheduling info

    atop -s
    Launch with various info (ppid, user, time)

    atop -v
    Launch with individual threads

    atop -y
    Once atop is running, press the following shortcut keys to sort processes:

    a – sort in order of most active resource.
    c – revert to sorting by CPU consumption (default).
    d – sort in order of disk activity.
    m – sort in order of memory usage
    n – sort in order of network activity
    

    Guide to reading atop reports/logs
    By default after install the atop daemon writes snapshots to a compressed log file (eg. /var/log/atop/atop_20140813). These log files can be read using:

    atop -r /full/path/to/atop/log/file
    Once you open a log file (e.g., atop -r /var/log/atop/atop_20140813), use t to go forward in 10-minute intervals and T to go back. You can analyze specific times by pressing b then entering the time. The above shortcut keys also work in this mode… a, c, d, m,n.

    You can use shortcuts with atopsar. For example, using the flag “-c 30 5” with atopsar will generate a report for current CPU utilization for 5 minutes (ten times with intervals of 30 seconds):

    atopsar -c 30 5
    Using the flag -A with return all available reports.

    atopsar -A
    But you can limit this to a specific time window using beginning “-b” and end “-e” flags:

    atopsar -A -b 11:00 -e 11:15
    As you can see, it’s easy to use atop for Linux server performance analysis effectively.



## - lsof

Este aplicativo lista os arquivos abertos (em uso) pelos processos. O termo lsof significa list open files.

    Algumas opções do comando
    −−help : mostra as opções do aplicativo.
    -i [endereço] [tipo] : mostra a lista dos arquivos abertos que estão associados ao endereço de Internet especificado. Se nenhum endereço é especificado, o comando fornece a lista todos os arquivos abertos associados aos endereços de internet. Pode-se também definir um tipo de comunicação como porta,  protocolos IPv4 e IPv6 e tipo de socket.
    -s : mostra o tamanho do arquivo.
    -p PID : mostra os arquivos abertos do processo com o PID informado.
    -u usuário : mostra apenas informações de um determinado usuário.
    -U : lista os sockets Unix.
    Exemplos
    Para ver a lista de todos os arquivos abertos pelos processos em execução no sistema, entre com
    lsof

    Para ver apenas os processos do usuário aluno, digite
    lsof -u aluno

    Se você quiser ver apenas a quantidade de aquivos abertos do usuário aluno, use o comando wc para contar a quantidade de linhas na resposta (subtrai 1 da resposta para ignorar o cabeçalho).

    lsof -u aluno | wc -l

    Para ver os arquivos abertos pelo processo com PID 3761, basta digitar
    lsof -p 3761

    Para listar os processos relacionados com a porta 80, entre com
    lsof -i :80

    Para obter a lista dos arquivos associados com o protocolo IPv4, entre com
    lsof -i 4

    Para listar os processos com socket UNIX, digite
    lsof -i -U

    Observações
    O comando fuser identifica os processos que estão usando um determinado arquivo.
    O comando stat fornece informações sobre arquivos.