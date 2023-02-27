## Gerenciamento de serviços e processos

___

Em geral, existem dois tipos de serviços: internos, os serviços relevantes que são necessários na inicialização do sistema, que, por exemplo, executam tarefas relacionadas ao hardware, e serviços instalados pelo usuário, que geralmente incluem todos os serviços do servidor. Esses serviços são executados em segundo plano sem qualquer interação do usuário. Estes também são chamados `daemons`e são identificados pela letra ' `d`' no final do nome do programa, por exemplo, `sshd`ou `systemd`.

A maioria das distribuições Linux agora mudou para `systemd`. Este demônio é um `Init process`iniciado primeiro e, portanto, tem o ID do processo (PID) 1. Esse daemon monitora e cuida do início e da parada ordenada de outros serviços. Todos os processos têm um PID atribuído que pode ser visualizado em `/proc/`com o número correspondente. Esse processo pode ter um ID de processo pai (PPID), conhecido como processo filho.

Além do mais `systemctl`nós também podemos usar `update-rc.d`para gerenciar links de script de inicialização SysV. Vamos dar uma olhada em alguns exemplos. Nós usaremos o `OpenSSH`servidor nesses exemplos. Se não o tivermos instalado, instale-o antes de prosseguir para esta seção.

___

## SystemctlName

Depois de instalar `OpenSSH`em nossa VM, podemos iniciar o serviço com o seguinte comando.

```
Denis-25@htb[/htb]$ systemctl start ssh
```

Depois de iniciarmos o serviço, podemos verificar se ele é executado sem erros.

```
Denis-25@htb[/htb]$ systemctl status ssh

● ssh.service - OpenBSD Secure Shell server
   Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-05-14 15:08:23 CEST; 24h ago
   Main PID: 846 (sshd)
   Tasks: 1 (limit: 4681)
   CGroup: /system.slice/ssh.service
           └─846 /usr/sbin/sshd -D

Mai 14 15:08:22 inlane systemd[1]: Starting OpenBSD Secure Shell server...
Mai 14 15:08:23 inlane sshd[846]: Server listening on 0.0.0.0 port 22.
Mai 14 15:08:23 inlane sshd[846]: Server listening on :: port 22.
Mai 14 15:08:23 inlane systemd[1]: Started OpenBSD Secure Shell server.
Mai 14 15:08:30 inlane systemd[1]: Reloading OpenBSD Secure Shell server.
Mai 14 15:08:31 inlane sshd[846]: Received SIGHUP; restarting.
Mai 14 15:08:31 inlane sshd[846]: Server listening on 0.0.0.0 port 22.
Mai 14 15:08:31 inlane sshd[846]: Server listening on :: port 22.
```

Para adicionar o OpenSSH ao script SysV para instruir o sistema a executar este serviço após a inicialização, podemos vinculá-lo com o seguinte comando:

```
Denis-25@htb[/htb]$ systemctl enable ssh

Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable ssh
```

Depois de reiniciar o sistema, o servidor OpenSSH será executado automaticamente. Podemos verificar isso com uma ferramenta chamada `ps`.

```
Denis-25@htb[/htb]$ ps -aux | grep ssh

root       846  0.0  0.1  72300  5660 ?        Ss   Mai14   0:00 /usr/sbin/sshd -D
```

Também podemos usar `systemctl`para listar todos os serviços.

```
Denis-25@htb[/htb]$ systemctl list-units --type=service

UNIT                                                       LOAD   ACTIVE SUB     DESCRIPTION              
accounts-daemon.service                                    loaded active running Accounts Service         
acpid.service                                              loaded active running ACPI event daemon        
apache2.service                                            loaded active running The Apache HTTP Server   
apparmor.service                                           loaded active exited  AppArmor initialization  
apport.service                                             loaded active exited  LSB: automatic crash repor
avahi-daemon.service                                       loaded active running Avahi mDNS/DNS-SD Stack  
bolt.service                                               loaded active running Thunderbolt system service
```

É bem possível que os serviços não iniciem devido a um erro. Para ver o problema, podemos usar a ferramenta `journalctl`para visualizar os registros.

```
Denis-25@htb[/htb]$ journalctl -u ssh.service --no-pager

-- Logs begin at Wed 2020-05-13 17:30:52 CEST, end at Fri 2020-05-15 16:00:14 CEST. --
Mai 13 20:38:44 inlane systemd[1]: Starting OpenBSD Secure Shell server...
Mai 13 20:38:44 inlane sshd[2722]: Server listening on 0.0.0.0 port 22.
Mai 13 20:38:44 inlane sshd[2722]: Server listening on :: port 22.
Mai 13 20:38:44 inlane systemd[1]: Started OpenBSD Secure Shell server.
Mai 13 20:39:06 inlane sshd[3939]: Connection closed by 10.22.2.1 port 36444 [preauth]
Mai 13 20:39:27 inlane sshd[3942]: Accepted password for master from 10.22.2.1 port 36452 ssh2
Mai 13 20:39:27 inlane sshd[3942]: pam_unix(sshd:session): session opened for user master by (uid=0)
Mai 13 20:39:28 inlane sshd[3942]: pam_unix(sshd:session): session closed for user master
Mai 14 02:04:49 inlane sshd[2722]: Received signal 15; terminating.
Mai 14 02:04:49 inlane systemd[1]: Stopping OpenBSD Secure Shell server...
Mai 14 02:04:49 inlane systemd[1]: Stopped OpenBSD Secure Shell server.
-- Reboot --
```

___

## Matar um processo

Um processo pode estar nos seguintes estados:

-   Corrida
-   Aguardando (esperando por um evento ou recurso do sistema)
-   Parou
-   Zombie (parou, mas ainda tem uma entrada na tabela de processos).

Os processos podem ser controlados usando `kill`, `pkill`, `pgrep`, e `killall`. Para interagir com um processo, devemos enviar um sinal para ele. Podemos visualizar todos os sinais com o seguinte comando:

```
Denis-25@htb[/htb]$ kill -l

 1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
 6) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
11) SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
16) SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
21) SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
26) SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
31) SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
38) SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
43) SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
48) SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
53) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
58) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
63) SIGRTMAX-1  64) SIGRTMAX
```

Os mais comumente usados são:

| **Sinal** | **Descrição** |
| --- | --- |
| `1` | `SIGHUP`\- É enviado para um processo quando o terminal que o controla é fechado. |
| `2` | `SIGINT`\- Enviado quando um usuário pressiona `[Ctrl] + C`no terminal de controle para interromper um processo. |
| `3` | `SIGQUIT`\- Enviado quando um usuário pressiona `[Ctrl] + D`para sair. |
| `9` | `SIGKILL`\- Mate imediatamente um processo sem operações de limpeza. |
| `15` | `SIGTERM`\- Encerramento do programa. |
| `19` | `SIGSTOP`\- Pare o programa. Não pode mais ser manuseado. |
| `20` | `SIGTSTP`\- Enviado quando um usuário pressiona `[Ctrl] + Z`para solicitar a suspensão de um serviço. O usuário pode lidar com isso depois. |

Por exemplo, se um programa congelasse, poderíamos forçar a sua eliminação com o seguinte comando:

```
Denis-25@htb[/htb]$ kill 9 <PID> 
```

___

## Plano de fundo de um processo

Às vezes, será necessário colocar em segundo plano a verificação ou processo que acabamos de iniciar para continuar usando a sessão atual para interagir com o sistema ou iniciar outros processos. Como já vimos, podemos fazer isso com o atalho `[Ctrl + Z]`. Como mencionado acima, nós enviamos o `SIGTSTP`sinal para o kernel, que suspende o processo.

```
Denis-25@htb[/htb]$ ping -c 10 www.hackthebox.eu

Denis-25@htb[/htb]$ vim tmpfile
[Ctrl + Z]
[2]+  Stopped                 vim tmpfile
```

Agora todos os processos em segundo plano podem ser exibidos com o seguinte comando.

```
Denis-25@htb[/htb]$ jobs

[1]+  Stopped                 ping -c 10 www.hackthebox.eu
[2]+  Stopped                 vim tmpfile
```

o `[Ctrl] + Z`atalho suspende os processos e eles não serão mais executados. Para mantê-lo funcionando em segundo plano, temos que inserir o comando `bg`para colocar o processo em segundo plano.

```
Denis-25@htb[/htb]$ bg

Denis-25@htb[/htb]$ 
--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 113482ms

[ENTER]
[1]+  Exit 1                  ping -c 10 www.hackthebox.eu
```

Outra opção é definir automaticamente o processo com um sinal AND ( `&`) no final do comando.

```
Denis-25@htb[/htb]$ ping -c 10 www.hackthebox.eu &

[1] 10825
PING www.hackthebox.eu (172.67.1.1) 56(84) bytes of data.
```

Assim que o processo terminar, veremos os resultados.

```
Denis-25@htb[/htb]$ 

--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 9210ms

[ENTER]
[1]+  Exit 1                  ping -c 10 www.hackthebox.eu
```

___

## Primeiro plano de um processo

Depois disso, podemos usar o `jobs`comando para listar todos os processos em segundo plano. Os processos em segundo plano não requerem interação do usuário e podemos usar a mesma sessão de shell sem esperar até que o processo termine primeiro. Assim que a verificação ou processo terminar seu trabalho, seremos notificados pelo terminal de que o processo foi concluído.

```
Denis-25@htb[/htb]$ jobs

[1]+  Running                 ping -c 10 www.hackthebox.eu &
```

Se quisermos colocar o processo em segundo plano em primeiro plano e interagir com ele novamente, podemos usar o `fg <ID>`comando.

```
Denis-25@htb[/htb]$ fg 1
ping -c 10 www.hackthebox.eu

--- www.hackthebox.eu ping statistics ---
10 packets transmitted, 0 received, 100% packet loss, time 9206ms
```

___

## Executar vários comandos

Existem três possibilidades para executar vários comandos, um após o outro. Estes são separados por:

-   Ponto e vírgula ( `;`)
-   Dobro `ampersand`personagens ( `&&`)
-   Tubos ( `|`)

A diferença entre eles está no tratamento dos processos anteriores e depende se o processo anterior foi concluído com sucesso ou com erros. O ponto e vírgula ( `;`) é um separador de comandos e executa os comandos ignorando os resultados e erros dos comandos anteriores.

```
Denis-25@htb[/htb]$ echo '1'; echo '2'; echo '3'

1
2
3
```

Por exemplo, se executarmos o mesmo comando, mas o substituirmos em segundo lugar, o comando `ls`com um arquivo que não existe, obtemos um erro e o terceiro comando será executado mesmo assim.

```
Denis-25@htb[/htb]$ echo '1'; ls MISSING_FILE; echo '3'

1
ls: cannot access 'MISSING_FILE': No such file or directory
3
```

No entanto, parece diferente se usarmos os caracteres AND duplos ( `&&`) para executar os comandos um após o outro. Se houver um erro em um dos comandos, os seguintes não serão mais executados e todo o processo será interrompido.

```
Denis-25@htb[/htb]$ echo '1' && ls MISSING_FILE && echo '3'

1
ls: cannot access 'MISSING_FILE': No such file or directory
```

Tubos ( `|`) dependem não apenas do funcionamento correto e sem erros dos processos anteriores, mas também dos resultados dos processos anteriores. Vamos lidar com os tubos mais tarde no `File Descriptors and Redirections`seção.

Servidores VPN

Aviso: Cada vez que você "trocar", suas chaves de conexão são regeneradas e você deve baixar novamente seu arquivo de conexão VPN.

Todas as instâncias de VM associadas ao antigo servidor VPN serão encerradas ao mudar para um novo servidor VPN.  
As instâncias PwnBox existentes mudarão automaticamente para o novo servidor VPN.