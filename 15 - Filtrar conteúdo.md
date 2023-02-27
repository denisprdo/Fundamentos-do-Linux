## Filtrar conteúdo

___

Na última seção, aprendemos sobre os redirecionamentos que podemos usar para redirecionar os resultados de um programa para outro para processamento. Para ler arquivos, não precisamos necessariamente usar um editor para isso. Existem duas ferramentas chamadas `more`e `less`, que são muito idênticos. esses são fundamentais `pagers`que nos permitem percorrer o arquivo em uma visão interativa. Vamos dar uma olhada em alguns exemplos.

___

## More

```
Denis-25@htb[/htb]$ more /etc/passwd
```

Depois de lermos o conteúdo usando `cat`e redirecionou para `more`, o já mencionado `pager`abre, e vamos começar automaticamente no início do arquivo.

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
<SNIP>
--More--
```

Com o `[Q]`chave, podemos deixar isso `pager`. Notaremos que a saída permanece no terminal.

___

## Less

Se agora dermos uma olhada na ferramenta `less`, perceberemos na página do manual que ele contém muito mais recursos do que `more`.

```
Denis-25@htb[/htb]$ less /etc/passwd
```

A apresentação é quase a mesma que com `more`.

```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
<SNIP>
:
```

Ao fechar `less`com o `[Q]`chave, vamos notar que a saída que vimos, ao contrário `more`, não permanece no terminal.

___

## Head

Às vezes, estaremos interessados apenas em questões específicas no início ou no final do arquivo. Se quisermos apenas obter o `first`linhas do arquivo, podemos usar a ferramenta `head`. Por padrão, `head`imprime as dez primeiras linhas do arquivo ou entrada fornecida, se não for especificado de outra forma.

```
Denis-25@htb[/htb]$ head /etc/passwd

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
```

___

## Tail

Se quisermos apenas ver as últimas partes de um arquivo ou resultados, podemos usar a contraparte de `head`chamado `tail`, que retorna o `last`dez linhas.

```
Denis-25@htb[/htb]$ tail /etc/passwd

miredo:x:115:65534::/var/run/miredo:/usr/sbin/nologin
usbmux:x:116:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
rtkit:x:117:119:RealtimeKit,,,:/proc:/usr/sbin/nologin
nm-openvpn:x:118:120:NetworkManager OpenVPN,,,:/var/lib/openvpn/chroot:/usr/sbin/nologin
nm-openconnect:x:119:121:NetworkManager OpenConnect plugin,,,:/var/lib/NetworkManager:/usr/sbin/nologin
pulse:x:120:122:PulseAudio daemon,,,:/var/run/pulse:/usr/sbin/nologin
beef-xss:x:121:124::/var/lib/beef-xss:/usr/sbin/nologin
lightdm:x:122:125:Light Display Manager:/var/lib/lightdm:/bin/false
do-agent:x:998:998::/home/do-agent:/bin/false
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

___

## Sort

Dependendo de quais resultados e arquivos são tratados, eles raramente são classificados. Freqüentemente, é necessário classificar os resultados desejados em ordem alfabética ou numérica para obter uma visão geral melhor. Para isso, podemos utilizar uma ferramenta chamada `sort`.

```
Denis-25@htb[/htb]$ cat /etc/passwd | sort

_apt:x:104:65534::/nonexistent:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
dnsmasq:x:107:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
dovecot:x:114:117:Dovecot mail server,,,:/usr/lib/dovecot:/usr/sbin/nologin
dovenull:x:115:118:Dovecot login user,,,:/nonexistent:/usr/sbin/nologin
ftp:x:113:65534::/srv/ftp:/usr/sbin/nologin
games:x:5:60:games:/usr/games:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
htb-student:x:1002:1002::/home/htb-student:/bin/bash
<SNIP>
```

Como podemos ver agora, a saída não começa mais com root, mas agora é classificada em ordem alfabética.

___

## Grep

Mais frequentemente, procuraremos apenas resultados específicos que contenham padrões que definimos. Uma das ferramentas mais utilizadas para isso é `grep`, que oferece muitos recursos diferentes. Assim, podemos procurar usuários que tenham o shell padrão " `/bin/bash`"Deu como exemplo.

```
Denis-25@htb[/htb]$ cat /etc/passwd | grep "/bin/bash"

root:x:0:0:root:/root:/bin/bash
mrb3n:x:1000:1000:mrb3n:/home/mrb3n:/bin/bash
cry0l1t3:x:1001:1001::/home/cry0l1t3:/bin/bash
htb-student:x:1002:1002::/home/htb-student:/bin/bash
```

Outra possibilidade é excluir resultados específicos. Para isso, a opção " `-v`" é usado com `grep`. No próximo exemplo, excluímos todos os usuários que desativaram o shell padrão com o nome " `/bin/false`" ou " `/usr/bin/nologin`".

```
Denis-25@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin"

root:x:0:0:root:/root:/bin/bash
sync:x:4:65534:sync:/bin:/bin/sync
postgres:x:111:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
user6:x:1000:1000:,,,:/home/user6:/bin/bash
```

___

## Cut

Resultados específicos com caracteres diferentes podem ser separados como delimitadores. Aqui é útil saber como remover delimitadores específicos e mostrar as palavras em uma linha em uma posição especificada. Uma das ferramentas que podem ser usadas para isso é `cut`. Portanto, usamos a opção " `-d`" e defina o delimitador para o caractere de dois pontos ( `:`) e defina com a opção " `-f`" a posição na linha que queremos enviar.

```
Denis-25@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | cut -d":" -f1

root
sync
mrb3n
cry0l1t3
htb-student
```

___

## Tr

Outra possibilidade de substituir certos caracteres de uma linha por caracteres definidos por nós é a ferramenta `tr`. Como primeira opção, definimos qual caractere queremos substituir e, como segunda opção, definimos o caractere pelo qual queremos substituí-lo. No próximo exemplo, substituímos o caractere de dois pontos por espaço.

```
Denis-25@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " "

root x 0 0 root /root /bin/bash
sync x 4 65534 sync /bin /bin/sync
mrb3n x 1000 1000 mrb3n /home/mrb3n /bin/bash
cry0l1t3 x 1001 1001  /home/cry0l1t3 /bin/bash
htb-student x 1002 1002  /home/htb-student /bin/bash
```

___

## Column

Uma vez que tais resultados podem muitas vezes ter uma representação pouco clara, a ferramenta `column`é adequado para exibir esses resultados em forma de tabela usando o " `-t`."

```
Denis-25@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | column -t

root         x  0     0      root               /root        /bin/bash
sync         x  4     65534  sync               /bin         /bin/sync
mrb3n        x  1000  1000   mrb3n              /home/mrb3n  /bin/bash
cry0l1t3     x  1001  1001   /home/cry0l1t3     /bin/bash
htb-student  x  1002  1002   /home/htb-student  /bin/bash
```

___

## awk

Como podemos ter notado, o usuário " `postgres`" tem uma linha a mais. Para simplificar ao máximo a classificação desses resultados, o ( `g`) `awk`programação é benéfica, o que nos permite exibir o primeiro ( `$1`) e por ultimo ( `$NF`) resultado da linha.

```
Denis-25@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}'

root /bin/bash
sync /bin/sync
mrb3n /bin/bash
cry0l1t3 /bin/bash
htb-student /bin/bash
```

___

## Sed

Haverá momentos em que queremos alterar nomes específicos em todo o arquivo ou na entrada padrão. Uma das ferramentas que podemos usar para isso é o editor de stream chamado `sed`. Um dos usos mais comuns disso é a substituição de texto. Aqui, `sed` procura padrões que definimos na forma de expressões regulares (regex) e os substitui por outro padrão que também definimos. Atenhamo-nos aos últimos resultados e digamos que queremos substituir a palavra " `bin`" com " `HTB`."

O " `s`" sinalizador no início representa o comando substituto. Em seguida, especificamos o padrão que queremos substituir. Após a barra ( `/`), inserimos o padrão que queremos usar como substituto na terceira posição. Finalmente, usamos o " `g`" flag, que significa substituir todas as correspondências.

```
Denis-25@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | sed 's/bin/HTB/g'

root /HTB/bash
sync /HTB/sync
mrb3n /HTB/bash
cry0l1t3 /HTB/bash
htb-student /HTB/bash
```

___

## Wc

Por último, mas não menos importante, muitas vezes será útil saber quantas correspondências bem-sucedidas temos. Para evitar a contagem manual de linhas ou caracteres, podemos utilizar a ferramenta `wc`. Com o " `-l`", especificamos que apenas as linhas são contadas.

```
Denis-25@htb[/htb]$ cat /etc/passwd | grep -v "false\|nologin" | tr ":" " " | awk '{print $1, $NF}' | wc -l

5
```

___

## Prática

Pode ser um pouco complicado no início lidar com tantas ferramentas diferentes e suas funções se não estivermos familiarizados com elas. Não se apresse e experimente as ferramentas. Dê uma olhada nas páginas do manual ( `man <tool>`) ou chame a ajuda para isso ( `<tool> -h` / `<tool> --help`). A melhor maneira de se familiarizar com todas as ferramentas é praticando. Tente usá-los com a maior frequência possível e poderemos filtrar muitas coisas intuitivamente em pouco tempo.

Servidores VPN

Aviso: Cada vez que você "trocar", suas chaves de conexão são regeneradas e você deve baixar novamente seu arquivo de conexão VPN.

Todas as instâncias de VM associadas ao antigo servidor VPN serão encerradas ao mudar para um novo servidor VPN.  
As instâncias PwnBox existentes mudarão automaticamente para o novo servidor VPN.