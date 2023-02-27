## Estrutura do Linux

___

## História

Muitos eventos levaram à criação do primeiro kernel do Linux e, finalmente, do sistema operacional (SO) Linux, começando com o lançamento do sistema operacional Unix por Ken Thompson e Dennis Ritchie (que trabalhavam para a AT&T na época) em 1970. The Berkeley O Software Distribution (BSD) foi lançado em 1977, mas como continha o código Unix de propriedade da AT&T, um processo resultante limitou o desenvolvimento do BSD. Richard Stallman iniciou o projeto GNU em 1983. Seu objetivo era criar um sistema operacional gratuito semelhante ao Unix, e parte de seu trabalho resultou na criação da GNU General Public License (GPL). Projetos de outros ao longo dos anos falharam em resultar em um kernel livre e funcional que se tornaria amplamente adotado até a criação do kernel do Linux.

Inicialmente, o Linux foi um projeto pessoal iniciado em 1991 por um estudante finlandês chamado Linus Torvalds. Seu objetivo era criar um novo kernel de sistema operacional livre. Ao longo dos anos, o kernel do Linux passou de um pequeno número de arquivos escritos em C sob licenciamento que proibia a distribuição comercial para a versão mais recente com mais de 23 milhões de linhas de código-fonte (comentários excluídos), licenciado sob a GNU General Public License v2.

O Linux está disponível em mais de 600 distribuições (ou um sistema operacional baseado no kernel do Linux e software e bibliotecas de suporte). Alguns dos mais populares e conhecidos são Ubuntu, Debian, Fedora, OpenSUSE, elementar, Manjaro, Gentoo Linux, RedHat e Linux Mint.

O Linux é geralmente considerado mais seguro do que outros sistemas operacionais e, embora tenha tido muitas vulnerabilidades de kernel no passado, está se tornando cada vez menos frequente. É menos suscetível a malware do que os sistemas operacionais Windows e é atualizado com muita frequência. O Linux também é muito estável e geralmente oferece alto desempenho ao usuário final. No entanto, pode ser mais difícil para iniciantes e não possui tantos drivers de hardware quanto o Windows.

Como o Linux é gratuito e de código aberto, o código-fonte pode ser modificado e distribuído comercialmente ou não por qualquer pessoa. Os sistemas operacionais baseados em Linux são executados em servidores, mainframes, desktops, sistemas embarcados, como roteadores, televisões, consoles de videogame e muito mais. O sistema operacional Android geral que roda em smartphones e tablets é baseado no kernel do Linux e, por causa disso, o Linux é o sistema operacional mais amplamente instalado.

Linux é um sistema operacional como Windows, iOS, Android ou macOS. Um sistema operacional é um software que gerencia todos os recursos de hardware associados ao nosso computador. Isso significa que um sistema operacional gerencia toda a comunicação entre software e hardware. Além disso, existem muitas distribuições diferentes (distro). É como uma versão dos sistemas operacionais Windows.

Com as instâncias interativas, temos acesso ao Pwnbox, uma versão customizada do Parrot OS. Este será o sistema operacional principal com o qual trabalharemos por meio dos módulos. O Parrot OS é uma distribuição Linux baseada em Debian que se concentra em segurança, privacidade e desenvolvimento.

___

## Filosofia

O Linux segue cinco princípios fundamentais:

| **Princípio** | **Descrição** |
| --- | --- |
| `Everything is a file` | Todos os arquivos de configuração para os vários serviços em execução no sistema operacional Linux são armazenados em um ou mais arquivos de texto. |
| `Small, single-purpose programs` | O Linux oferece muitas ferramentas diferentes com as quais trabalharemos, que podem ser combinadas para trabalhar em conjunto. |
| `Ability to chain programs together to perform complex tasks` | A integração e combinação de diferentes ferramentas nos permite realizar muitas tarefas grandes e complexas, como processar ou filtrar resultados de dados específicos. |
| `Avoid captive user interfaces` | O Linux foi projetado para funcionar principalmente com o shell (ou terminal), o que dá ao usuário maior controle sobre o sistema operacional. |
| `Configuration data stored in a text file` | Um exemplo desse tipo de arquivo é o `/etc/passwd`arquivo, que armazena todos os usuários cadastrados no sistema. |

___

## Componentes

| **Componente** | **Descrição** |
| --- | --- |
| `Bootloader` | Um pedaço de código que é executado para guiar o processo de inicialização para iniciar o sistema operacional. O Parrot Linux usa o gerenciador de inicialização GRUB. |
| `OS Kernel` | O kernel é o principal componente de um sistema operacional. Ele gerencia os recursos dos dispositivos de E/S do sistema no nível do hardware. |
| `Daemons` | Os serviços de segundo plano são chamados de "daemons" no Linux. Sua finalidade é garantir que as principais funções, como agendamento, impressão e multimídia, estejam funcionando corretamente. Esses pequenos programas são carregados depois que inicializamos ou efetuamos login no computador. |
| `OS Shell` | O shell do sistema operacional ou o interpretador de linguagem de comando (também conhecido como linha de comando) é a interface entre o sistema operacional e o usuário. Essa interface permite que o usuário diga ao sistema operacional o que fazer. Os shells mais usados são Bash, Tcsh/Csh, Ksh, Zsh e Fish. |
| `Graphics server` | Isso fornece um subsistema gráfico (servidor) chamado "X" ou "X-server" que permite que programas gráficos sejam executados local ou remotamente no sistema X-window. |
| `Window Manager` | Também conhecida como interface gráfica do usuário (GUI). Existem muitas opções, incluindo GNOME, KDE, MATE, Unity e Cinnamon. Um ambiente de área de trabalho geralmente possui vários aplicativos, incluindo arquivos e navegadores da web. Eles permitem que o usuário acesse e gerencie os recursos e serviços essenciais e acessados com frequência de um sistema operacional. |
| `Utilities` | Aplicativos ou utilitários são programas que executam funções específicas para o usuário ou outro programa. |

___

## Arquitetura Linux

O sistema operacional Linux pode ser dividido em camadas:

| **Camada** | **Descrição** |
| --- | --- |
| `Hardware` | Dispositivos periféricos como RAM do sistema, disco rígido, CPU e outros. |
| `Kernel` | O núcleo do sistema operacional Linux cuja função é virtualizar e controlar recursos comuns de hardware do computador, como CPU, memória alocada, dados acessados e outros. O kernel fornece a cada processo seus próprios recursos virtuais e evita/atenua conflitos entre diferentes processos. |
| `Shell` | Uma interface de linha de comando ( **CLI** ), também conhecida como shell na qual um usuário pode inserir comandos para executar as funções do kernel. |
| `System Utility` | Disponibiliza ao usuário todas as funcionalidades do sistema operacional. |

___

## Hierarquia do sistema de arquivos

O sistema operacional Linux é estruturado em uma hierarquia semelhante a uma árvore e está documentado no [Filesystem Hierarchy](http://www.pathname.com/fhs/) Standard (FHS). O Linux é estruturado com os seguintes diretórios padrão de nível superior:

![imagem](https://academy.hackthebox.com/storage/modules/18/NEW_filesystem.png)

| **Caminho** | **Descrição** |
| --- | --- |
| `/` | O diretório de nível superior é o sistema de arquivos raiz e contém todos os arquivos necessários para inicializar o sistema operacional antes que outros sistemas de arquivos sejam montados, bem como os arquivos necessários para inicializar os outros sistemas de arquivos. Após a inicialização, todos os outros sistemas de arquivos são montados em pontos de montagem padrão como subdiretórios da raiz. |
| `/bin` | Contém binários de comando essenciais. |
| `/boot` | Consiste no carregador de inicialização estático, executável do kernel e arquivos necessários para inicializar o sistema operacional Linux. |
| `/dev` | Contém arquivos de dispositivo para facilitar o acesso a todos os dispositivos de hardware conectados ao sistema. |
| `/etc` | Arquivos de configuração do sistema local. Arquivos de configuração para aplicativos instalados também podem ser salvos aqui. |
| `/home` | Cada usuário no sistema tem um subdiretório aqui para armazenamento. |
| `/lib` | Arquivos de biblioteca compartilhada necessários para a inicialização do sistema. |
| `/media` | Dispositivos externos de mídia removível, como drives USB, são montados aqui. |
| `/mnt` | Ponto de montagem temporário para sistemas de arquivos regulares. |
| `/opt` | Arquivos opcionais, como ferramentas de terceiros, podem ser salvos aqui. |
| `/root` | O diretório inicial do usuário raiz. |
| `/sbin` | Este diretório contém executáveis usados para administração do sistema (arquivos binários do sistema). |
| `/tmp` | O sistema operacional e muitos programas usam esse diretório para armazenar arquivos temporários. Esse diretório geralmente é limpo na inicialização do sistema e pode ser excluído em outras ocasiões sem qualquer aviso. |
| `/usr` | Contém executáveis, bibliotecas, arquivos man, etc. |
| `/var` | Este diretório contém arquivos de dados variáveis, como arquivos de log, caixas de entrada de e-mail, arquivos relacionados a aplicativos da web, arquivos cron e muito mais. |