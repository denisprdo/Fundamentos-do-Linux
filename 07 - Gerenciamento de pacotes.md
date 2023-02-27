## Gerenciamento de pacotes

___

Seja trabalhando como administrador de sistema, mantendo nossas próprias máquinas Linux em casa ou construindo/atualizando/mantendo nossa distribuição de teste de penetração preferida, é crucial ter um domínio firme dos gerenciadores de pacotes Linux disponíveis e as várias maneiras de utilizá-los para instalar, atualizar ou remover pacotes. Pacotes são arquivos que contêm binários de software, arquivos de configuração, informações sobre dependências e acompanham atualizações e upgrades. Os recursos que a maioria dos sistemas de gerenciamento de pacotes oferece são:

-   Download de pacotes
-   Resolução de dependência
-   Um formato de pacote binário padrão
-   Locais comuns de instalação e configuração
-   Configuração e funcionalidade adicionais relacionadas ao sistema
-   Controle de qualidade

Podemos usar muitos sistemas de gerenciamento de pacotes diferentes que cobrem diferentes tipos de arquivos como ".deb", ".rpm" e outros. O requisito de gerenciamento de pacotes é que o software a ser instalado esteja disponível como um pacote correspondente. Normalmente, isso é criado, oferecido e mantido centralmente nas distribuições do Linux. Desta forma, o software é integrado diretamente ao sistema, e seus diversos diretórios são distribuídos por todo o sistema. As alterações do software de gerenciamento de pacotes no sistema para instalar o pacote são retiradas do pacote e implementadas pelo software de gerenciamento de pacotes. Se o software de gerenciamento de pacotes reconhecer que são necessários pacotes adicionais para o bom funcionamento do pacote que ainda não foi instalado, uma dependência é incluída e avisa o administrador ou tenta recarregar o software ausente de um repositório, por exemplo, e instalar com antecedência.

Se um software instalado foi excluído, o sistema de gerenciamento de pacotes retoma as informações do pacote, modifica-o com base em sua configuração e exclui os arquivos. Existem diferentes programas de gerenciamento de pacotes que podemos usar para isso. Aqui está uma lista de exemplos de tais programas:

| **Comando** | **Descrição** |
| --- | --- |
| `dpkg` | o `dpkg`é uma ferramenta para instalar, compilar, remover e gerenciar pacotes Debian. O front-end principal e mais amigável para `dpkg`é aptidão. |
| `apt` | O Apt fornece uma interface de linha de comando de alto nível para o sistema de gerenciamento de pacotes. |
| `aptitude` | O Aptitude é uma alternativa ao apt e é uma interface de alto nível para o gerenciador de pacotes. |
| `snap` | Instalar, configurar, atualizar e remover pacotes snap. Os Snaps permitem a distribuição segura dos aplicativos e utilitários mais recentes para nuvem, servidores, desktops e internet das coisas. |
| `gem` | Gem é o front-end do RubyGems, o gerenciador de pacotes padrão para Ruby. |
| `pip` | Pip é um instalador de pacotes Python recomendado para instalar pacotes Python que não estão disponíveis no arquivo Debian. Ele pode funcionar com repositórios de controle de versão (atualmente apenas repositórios Git, Mercurial e Bazaar), registra a saída extensivamente e evita instalações parciais baixando todos os requisitos antes de iniciar a instalação. |
| `git` | O Git é um sistema de controle de revisão rápido, escalável e distribuído com um conjunto de comandos extraordinariamente rico que fornece operações de alto nível e acesso total aos internos. |

É altamente recomendável configurar nossa máquina virtual (VM) localmente para experimentá-la. Vamos experimentar um pouco em nossa VM local e estendê-la com alguns pacotes adicionais. Primeiro, vamos instalar `git`usando `apt`.

___

#### Gerenciador de pacotes avançado (APT)

As distribuições Linux baseadas em Debian usam o `APT`gerenciador de pacotes. Um pacote é um arquivo compactado contendo vários arquivos ".deb". o `dpkg`utilitário é usado para instalar programas do arquivo ".deb" associado. `APT`facilita a atualização e instalação de programas porque muitos programas têm dependências. Ao instalar um programa a partir de um arquivo ".deb" independente, podemos ter problemas de dependência e precisar baixar e instalar um ou vários pacotes adicionais. `APT`torna isso mais fácil e eficiente empacotando todas as dependências necessárias para instalar um programa.

Cada distribuição do Linux usa repositórios de software que são atualizados com frequência. Quando atualizamos um programa ou instalamos um novo, o sistema consulta esses repositórios em busca do pacote desejado. Os repositórios podem ser rotulados como estáveis, em teste ou instáveis. A maioria das distribuições Linux utiliza o repositório mais estável ou "principal". Isso pode ser verificado visualizando o conteúdo do `/etc/apt/sources.list`Arquivo. A lista de repositórios do Parrot OS está em `/etc/apt/sources.list.d/parrot.list`.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ cat /etc/apt/sources.list.d/parrot.list

# parrot repository
# this file was automatically generated by parrot-mirror-selector
deb http://htb.deb.parrot.sh/parrot/ rolling main contrib non-free
#deb-src https://deb.parrot.sh/parrot/ rolling main contrib non-free
deb http://htb.deb.parrot.sh/parrot/ rolling-security main contrib non-free
#deb-src https://deb.parrot.sh/parrot/ rolling-security main contrib non-free
```

O APT usa um banco de dados chamado cache do APT. Isso é usado para fornecer informações sobre pacotes instalados em nosso sistema offline. Podemos pesquisar o cache APT, por exemplo, para encontrar todos `Impacket`pacotes relacionados.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ apt-cache search impacket

impacket-scripts - Links to useful impacket scripts examples
polenum - Extracts the password policy from a Windows system
python-pcapy - Python interface to the libpcap packet capture library (Python 2)
python3-impacket - Python3 module to easily build and dissect network protocols
python3-pcapy - Python interface to the libpcap packet capture library (Python 3)
```

Podemos então visualizar informações adicionais sobre um pacote.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ apt-cache show impacket-scripts

Package: impacket-scripts
Version: 1.4
Architecture: all
Maintainer: Kali Developers <devel@kali.org>
Installed-Size: 13
Depends: python3-impacket (>= 0.9.20), python3-ldap3 (>= 2.5.0), python3-ldapdomaindump
Breaks: python-impacket (<< 0.9.18)
Replaces: python-impacket (<< 0.9.18)
Priority: optional
Section: misc
Filename: pool/main/i/impacket-scripts/impacket-scripts_1.4_all.deb
Size: 2080
<SNIP>
```

Também podemos listar todos os pacotes instalados.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ apt list --installed

Listing... Done
accountsservice/rolling,now 0.6.55-2 amd64 [installed,automatic]
adapta-gtk-theme/rolling,now 3.95.0.11-1 all [installed]
adduser/rolling,now 3.118 all [installed]
adwaita-icon-theme/rolling,now 3.36.1-2 all [installed,automatic]
aircrack-ng/rolling,now 1:1.6-4 amd64 [installed,automatic]
<SNIP>
```

Se estivermos perdendo alguns pacotes, podemos procurá-los e instalá-los usando o seguinte comando.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ sudo apt install impacket-scripts -y

Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following NEW packages will be installed:
  impacket-scripts
0 upgraded, 1 newly installed, 0 to remove and 0 not upgraded.
Need to get 2,080 B of archives.
After this operation, 13.3 kB of additional disk space will be used.
Get:1 https://euro2-emea-mirror.parrot.sh/mirrors/parrot rolling/main amd64 impacket-scripts all 1.4 [2,080 B]
Fetched 2,080 B in 0s (15.2 kB/s)
Selecting previously unselected package impacket-scripts.
(Reading database ... 378459 files and directories currently installed.)
Preparing to unpack .../impacket-scripts_1.4_all.deb ...
Unpacking impacket-scripts (1.4) ...
Setting up impacket-scripts (1.4) ...
Scanning application launchers
Removing duplicate launchers from Debian
Launchers are updated
```

___

## git

Agora que temos `git`instalado, podemos usá-lo para baixar ferramentas úteis do Github. Um desses projetos é chamado 'Nishang'. Trataremos e trabalharemos com o projeto em si mais tarde. Primeiro, precisamos navegar até o [repositório do projeto](https://github.com/samratashok/nishang) e copiar o link do Github antes de usar o git para baixá-lo.

![imagem](https://academy.hackthebox.com/storage/modules/18/git-nishang.png)

No entanto, antes de baixar o projeto e seus scripts e listas, devemos criar uma pasta específica.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ mkdir ~/nishang/ && git clone https://github.com/samratashok/nishang.git ~/nishang

Cloning into '/opt/nishang/'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 1691 (delta 4), reused 6 (delta 2), pack-reused 1676
Receiving objects: 100% (1691/1691), 7.84 MiB | 4.86 MiB/s, done.
Resolving deltas: 100% (1055/1055), done.
```

___

## DPKG

Também podemos baixar os programas e ferramentas dos repositórios separadamente. Neste exemplo, baixamos 'strace' para Ubuntu 18.04 LTS.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb

--2020-05-15 03:27:17--  http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
Resolving archive.ubuntu.com (archive.ubuntu.com)... 91.189.88.142, 91.189.88.152, 2001:67c:1562::18, ...
Connecting to archive.ubuntu.com (archive.ubuntu.com)|91.189.88.142|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 333388 (326K) [application/x-debian-package]
Saving to: ‘strace_4.21-1ubuntu1_amd64.deb’

strace_4.21-1ubuntu1_amd64.deb       100%[===================================================================>] 325,57K  --.-KB/s    in 0,1s    

2020-05-15 03:27:18 (2,69 MB/s) - ‘strace_4.21-1ubuntu1_amd64.deb’ saved [333388/333388]
```

Além disso, agora podemos usar ambos `apt`e `dpkg`para instalar o pacote. Como já trabalhamos com `apt`, vamos nos voltar para `dpkg`no próximo exemplo.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb 

(Reading database ... 154680 files and directories currently installed.)
Preparing to unpack strace_4.21-1ubuntu1_amd64.deb ...
Unpacking strace (4.21-1ubuntu1) over (4.21-1ubuntu1) ...
Setting up strace (4.21-1ubuntu1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
```

Com isso, já instalamos a ferramenta e podemos testar se ela funciona corretamente.

Gerenciador de pacotes avançado (APT)

```
Denis-25@htb[/htb]$ strace -h

usage: strace [-CdffhiqrtttTvVwxxy] [-I n] [-e expr]...
              [-a column] [-o file] [-s strsize] [-P path]...
              -p pid... / [-D] [-E var=val]... [-u username] PROG [ARGS]
   or: strace -c[dfw] [-I n] [-e expr]... [-O overhead] [-S sortby]
              -p pid... / [-D] [-E var=val]... [-u username] PROG [ARGS]

Output format:
  -a column      alignment COLUMN for printing syscall results (default 40)
  -i             print instruction pointer at time of syscall
```

##### Exercício Opcional:

Pesquise a ferramenta " **evil-winrm** " no Github e instale-a em nossas instâncias interativas. Experimente todos os diferentes métodos de instalação.