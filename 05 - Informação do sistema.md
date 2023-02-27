## Informação do sistema

___

Como trabalharemos com vários sistemas Linux diferentes, precisamos aprender a estrutura e as informações sobre o sistema, seus processos, configurações de rede, usuários, diretórios, configurações do usuário e os parâmetros correspondentes. Aqui está uma lista das ferramentas necessárias que nos ajudarão a obter as informações acima. A maioria deles é instalada por padrão.

| **Comando** | **Descrição** |
| --- | --- |
| `whoami` | Exibe o nome de usuário atual. |
| `id` | Retorna a identidade dos usuários |
| `hostname` | Define ou imprime o nome do sistema host atual. |
| `uname` | Imprime informações básicas sobre o nome do sistema operacional e o hardware do sistema. |
| `pwd` | Retorna o nome do diretório de trabalho. |
| `ifconfig` | O utilitário ifconfig é usado para atribuir ou visualizar um endereço para uma interface de rede e/ou configurar parâmetros de interface de rede. |
| `ip` | IP é um utilitário para mostrar ou manipular roteamento, dispositivos de rede, interfaces e túneis. |
| `netstat` | Mostra o status da rede. |
| `ss` | Outro utilitário para investigar soquetes. |
| `ps` | Mostra o status do processo. |
| `who` | Exibe quem está logado. |
| `env` | Imprime o ambiente ou define e executa o comando. |
| `lsblk` | Lista os dispositivos de bloqueio. |
| `lsusb` | Lista dispositivos USB |
| `lsof` | Lista arquivos abertos. |
| `lspci` | Lista os dispositivos PCI. |

Vejamos alguns exemplos.

#### nome de anfitrião

o `hostname`O comando é bastante autoexplicativo e imprimirá apenas o nome do computador ao qual estamos conectados

nome de anfitrião

```
Denis-25@htb[/htb]$ hostname

nixfund
```

#### Quem sou eu

Este comando rápido e fácil pode ser usado nos sistemas Windows e Linux para obter nosso nome de usuário atual. Durante uma avaliação de segurança, obtemos acesso shell reverso em um host, e um dos primeiros bits de consciência situacional que devemos fazer é descobrir com qual usuário estamos executando. A partir daí, podemos descobrir se o usuário tem algum privilégio/acesso especial.

Quem sou eu

```
cry0l1t3@htb[/htb]$ whoami

cry0l1t3
```

#### Identidade

o `id`comando se expande no `whoami`comando e imprime nossa associação de grupo e IDs efetivos. Isso pode ser interessante para testadores de penetração que procuram ver qual acesso um usuário pode ter e administradores de sistema que procuram auditar permissões de contas e membros de grupos. Nesta saída, o `hackthebox`grupo é de interesse porque não é padrão, o `adm`grupo significa que o usuário pode ler arquivos de log em `/var/log`e potencialmente obter acesso a informações confidenciais, associação ao `sudo`grupo é de particular interesse, pois significa que nosso usuário pode executar alguns ou todos os comandos como o todo-poderoso `root`do utilizador. Os direitos de sudo podem nos ajudar a aumentar os privilégios ou podem ser um sinal para um administrador de sistema de que ele pode precisar auditar permissões e associações de grupo para remover qualquer acesso que não seja necessário para um determinado usuário realizar suas tarefas diárias.

Identidade

```
cry0l1t3@htb[/htb]$ id

uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),1337(hackthebox),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),116(lpadmin),126(sambashare)
```

#### nome

Vamos cavar no `uname`comandar um pouco mais. Se digitarmos `man uname`em nosso terminal, abriremos a página de manual do comando, que mostrará as possíveis opções que podemos executar com o comando e os resultados.

nome

```

UNAME(1)                                    User Commands                                   UNAME(1)

NAME
       uname - print system information

SYNOPSIS
       uname [OPTION]...

DESCRIPTION
       Print certain system information.  With no OPTION, same as -s.

       -a, --all
              print all information, in the following order, except omit -p and -i if unknown:

       -s, --kernel-name
              print the kernel name

       -n, --nodename
              print the network node hostname

       -r, --kernel-release
              print the kernel release

       -v, --kernel-version
              print the kernel version

       -m, --machine
              print the machine hardware name

       -p, --processor
              print the processor type (non-portable)

       -i, --hardware-platform
              print the hardware platform (non-portable)

       -o, --operating-system
```

Corrida `uname -a`imprimirá todas as informações sobre a máquina em uma ordem específica: nome do kernel, nome do host, versão do kernel, versão do kernel, nome do hardware da máquina e sistema operacional. o `-a`bandeira irá omitir `-p`(tipo de processador) e `-i`(plataforma de hardware) se forem desconhecidos.

nome

```
cry0l1t3@htb[/htb]$ uname -a

Linux box 4.15.0-99-generic #100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
```

No comando acima, podemos ver que o nome do kernel é `Linux`, o nome do host é `box`, a versão do kernel é `4.15.0-99-generic`, a versão do kernel é `#100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020`, e assim por diante. A execução de qualquer uma dessas opções por conta própria nos dará a saída de bit específica em que estamos interessados.

#### Uname para obter a liberação do kernel

Suponha que queremos imprimir a versão do kernel para procurar explorações potenciais do kernel rapidamente. podemos digitar `uname -r`para obter esta informação.

Uname para obter a liberação do kernel

```
cry0l1t3@htb[/htb]$ uname -r

4.15.0-99-generic
```

Com essas informações, poderíamos pesquisar "4.15.0-99-generic exploit" e o primeiro [resultado](https://www.exploit-db.com/exploits/47163) imediatamente parece útil para nós.

É altamente recomendável estudar os comandos e entender para que servem e quais informações eles podem fornecer. Embora um pouco tedioso, podemos aprender muito estudando as páginas de manual para comandos comuns. Podemos até descobrir coisas que nem sabíamos que eram possíveis com um determinado comando. Esta informação não é usada apenas para trabalhar com Linux. No entanto, também será usado posteriormente para descobrir vulnerabilidades e configurações incorretas no sistema Linux que podem contribuir para a escalação de privilégios. Aqui estão alguns exercícios opcionais que podemos resolver para fins de prática, que nos ajudarão a nos familiarizar com alguns dos comandos.

___

## Fazendo login via SSH

`Secure Shell` ( `SSH`) refere-se a um protocolo que permite aos clientes acessar e executar comandos ou ações em computadores remotos. Em hosts e servidores baseados em Linux ou em outro sistema operacional semelhante ao Unix, o SSH é uma das ferramentas padrão permanentemente instaladas e é a escolha preferida de muitos administradores para configurar e manter um computador por meio de acesso remoto. É um protocolo mais antigo e comprovado que não requer ou oferece uma interface gráfica do usuário (GUI). Por isso, funciona de forma muito eficiente e ocupa poucos recursos. Usamos este tipo de conexão nas seções a seguir e na maioria dos outros módulos para oferecer a possibilidade de experimentar os comandos e ações aprendidos em um ambiente seguro. Podemos nos conectar aos nossos alvos com o seguinte comando:

#### Login SSH

Login SSH

```
Denis-25@htb[/htb]$ ssh [username]@[IP address]
```

Servidores VPN

Aviso: Cada vez que você "trocar", suas chaves de conexão são regeneradas e você deve baixar novamente seu arquivo de conexão VPN.

Todas as instâncias de VM associadas ao antigo servidor VPN serão encerradas ao mudar para um novo servidor VPN.  
As instâncias PwnBox existentes mudarão automaticamente para o novo servidor VPN.