## Localizar arquivos e diretórios

___

## Importância da Pesquisa

É crucial poder encontrar os arquivos e pastas de que precisamos. Depois de ter acesso a um sistema baseado em Linux, será essencial encontrar arquivos de configuração, scripts criados por usuários ou pelo administrador e outros arquivos e pastas. Não precisamos navegar manualmente por cada pasta e verificar quando foi modificado pela última vez. Existem algumas ferramentas que podemos usar para facilitar esse trabalho.

___

##  Which

Uma das ferramentas comuns é `which`. Esta ferramenta retorna o caminho para o arquivo ou link que deve ser executado. Isso nos permite determinar se programas específicos, como cURL , netcat , wget , python , gcc , estão disponíveis no sistema operacional. Vamos usá-lo para procurar Python em nossa instância interativa.

```
Denis-25@htb[/htb]$ which python

/usr/bin/python
```

Se o programa que procuramos não existir, nenhum resultado será exibido.

___

## Find

Outra ferramenta útil é `find`. Além da função de localizar arquivos e pastas, esta ferramenta também contém a função de filtrar os resultados. Podemos usar parâmetros de filtro como o tamanho do arquivo ou a data. Também podemos especificar se procuramos apenas arquivos ou pastas.

#### Sintaxe - Find

Sintaxe - Find

```
Denis-25@htb[/htb]$ find <location> <options>
```

Vejamos um exemplo de como seria um comando com várias opções.

Sintaxe - Find
```
Denis-25@htb[/htb]$ find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

-rw-r--r-- 1 root root 136392 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/auto.conf
-rw-r--r-- 1 root root 82290 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/tristate.conf
-rw-r--r-- 1 root root 95813 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats32.conf
-rw-r--r-- 1 root root 60346 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dynamic.conf
-rw-r--r-- 1 root root 96249 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb32.conf
-rw-r--r-- 1 root root 54755 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats16.conf
-rw-r--r-- 1 root root 22635 May  7 14:33 /usr/share/metasploit-framework/data/jtr/korelogic.conf
-rwxr-xr-x 1 root root 108534 May  7 14:33 /usr/share/metasploit-framework/data/jtr/john.conf
-rw-r--r-- 1 root root 55285 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb16.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /usr/share/doc/sqlmap/examples/sqlmap.conf
-rw-r--r-- 1 root root 25086 Mar  4 22:04 /etc/dnsmasq.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /etc/sqlmap/sqlmap.conf
```

Agora vamos dar uma olhada nas opções que usamos no comando anterior. Se passarmos o mouse sobre as respectivas opções, uma pequena janela aparecerá com uma explicação. Essas explicações também serão encontradas em outros módulos, o que deve nos ajudar se ainda não estivermos familiarizados com uma das ferramentas.

| **Opção** | **Descrição** |
| --- | --- |
| `-type f` | Aqui, definimos o tipo do objeto pesquisado. Nesse caso, ' `f`' apoia ' `file`'. |
| `-name *.conf` | Com ' `-name`', indicamos o nome do arquivo que estamos procurando. O asterisco ( `*`) significa 'todos' os arquivos com a extensão ' `.conf`' extensão. |
| `-user root` | Esta opção filtra todos os arquivos cujo proprietário é o usuário root. |
| `-size +20k` | Podemos então filtrar todos os arquivos localizados e especificar que queremos ver apenas os arquivos maiores que 20 KiB. |
| `-newermt 2020-03-03` | Com esta opção, definimos a data. Somente arquivos mais recentes que a data especificada serão apresentados. |
| `-exec ls -al {} \;` | Esta opção executa o comando especificado, usando as chaves como espaços reservados para cada resultado. A barra invertida evita que o próximo caractere seja interpretado pelo shell porque, caso contrário, o ponto-e-vírgula encerraria o comando e não alcançaria o redirecionamento. |
| `2>/dev/null` | Isto é um `STDERR`redirecionamento para o ' `null device`', ao qual voltaremos na próxima seção. Esse redirecionamento garante que nenhum erro seja exibido no terminal. Este redirecionamento deve `not`ser uma opção do comando 'find'. |

___

## ## Locate

Levará muito tempo para pesquisar em todo o sistema nossos arquivos e diretórios para realizar muitas pesquisas diferentes. O comando `locate`nos oferece uma maneira mais rápida de pesquisar no sistema. Em contraste com o `find`comando, `locate`funciona com um banco de dados local que contém todas as informações sobre arquivos e pastas existentes. Podemos atualizar esse banco de dados com o seguinte comando.

Sintaxe - Locate

```
Denis-25@htb[/htb]$ sudo updatedb
```

Se agora procurarmos todos os arquivos com a extensão " `.conf`", você descobrirá que essa pesquisa produz resultados muito mais rapidamente do que usar `find`.

Sintaxe - Locate

```
Denis-25@htb[/htb]$ locate *.conf

/etc/GeoIP.conf
/etc/NetworkManager/NetworkManager.conf
/etc/UPower/UPower.conf
/etc/adduser.conf
<SNIP>
```

No entanto, esta ferramenta não possui tantas opções de filtro que podemos usar. Portanto, sempre vale a pena considerar se podemos usar o `locate`comando ou, em vez disso, use o `find`comando. Depende sempre do que procuramos.

##### Exercício Opcional:

Experimente os diferentes utilitários e encontre tudo relacionado à **netcat** / **nc .** ferramenta

Servidores VPN

Aviso: Cada vez que você "trocar", suas chaves de conexão são regeneradas e você deve baixar novamente seu arquivo de conexão VPN.

Todas as instâncias de VM associadas ao antigo servidor VPN serão encerradas ao mudar para um novo servidor VPN.  
As instâncias PwnBox existentes mudarão automaticamente para o novo servidor VPN.
