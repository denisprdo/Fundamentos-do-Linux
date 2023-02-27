## Conseguindo ajuda

___

Sempre nos depararemos com ferramentas cujos parâmetros opcionais não conhecemos de memória ou ferramentas que nunca vimos antes. Portanto, é vital saber como podemos nos ajudar a nos familiarizar com essas ferramentas. As duas primeiras formas são as páginas de manual e as funções de ajuda. É sempre uma boa ideia nos familiarizarmos com a ferramenta que queremos experimentar primeiro. Também aprenderemos alguns truques possíveis com algumas das ferramentas que pensávamos que não eram possíveis. Nas páginas do manual, encontraremos os manuais detalhados com explicações detalhadas.

#### Sintaxe:

Sintaxe:

```
Denis-25@htb[/htb]$ man <tool>
```

Vejamos um exemplo:

#### Exemplo:

Exemplo:

```
Denis-25@htb[/htb]$ man curl
```

Exemplo:

```
curl(1)                                                             Curl Manual                                                            curl(1)

NAME
       curl - transfer a URL

SYNOPSIS
       curl [options] [URL...]

DESCRIPTION
       curl  is  a tool to transfer data from or to a server, using one of the supported protocols (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS,  
       IMAP, IMAPS,  LDAP,  LDAPS,  POP3,  POP3S,  RTMP, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET, and TFTP). The command is designed to work without user interaction.

       curl offers a busload of useful tricks like proxy support, user authentication, FTP upload, HTTP post, SSL connections, cookies, file transfer resume, Metalink,  and more. As we will see below, the number of features will make our head spin!

       curl is powered by libcurl for all transfer-related features.  See libcurl(3) for details.

Manual page curl(1) line 1 (press h for help or q to quit)

```

Depois de ver alguns exemplos, também podemos ver rapidamente os parâmetros opcionais sem navegar pela documentação completa. Temos várias maneiras de fazer isso.

#### Sintaxe:

Sintaxe:

```
Denis-25@htb[/htb]$ <tool> --help
```

#### Exemplo:

Exemplo:

```
Denis-25@htb[/htb]$ curl --help

Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --anyauth       Pick any authentication method
 -a, --append        Append to target file when uploading
     --basic         Use HTTP Basic Authentication
     --cacert <file> CA certificate to verify peer against
     --capath <dir>  CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
<SNIP>
```

Também podemos usar a versão curta dele:

#### Sintaxe:

Sintaxe:

```
Denis-25@htb[/htb]$ <tool> -h
```

#### Exemplo:

Exemplo:

```
Denis-25@htb[/htb]$ curl -h

Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --anyauth       Pick any authentication method
 -a, --append        Append to target file when uploading
     --basic         Use HTTP Basic Authentication
     --cacert <file> CA certificate to verify peer against
     --capath <dir>  CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
<SNIP>
```

Como podemos ver, os resultados um do outro não diferem neste exemplo. Outra ferramenta que pode ser útil no começo é `apropos`. Cada página de manual tem uma breve descrição disponível dentro dela. Essa ferramenta pesquisa as descrições de instâncias de uma determinada palavra-chave.

#### Sintaxe:

Sintaxe:

```
Denis-25@htb[/htb]$ apropos <keyword>
```

#### Exemplo:

Exemplo:

```
Denis-25@htb[/htb]$ apropos sudo

sudo (8)             - execute a command as another user
sudo.conf (5)        - configuration for sudo front end
sudo_plugin (8)      - Sudo Plugin API
sudo_root (8)        - How to run administrative commands
sudoedit (8)         - execute a command as another user
sudoers (5)          - default sudo security policy plugin
sudoreplay (8)       - replay sudo session logs
visudo (8)           - edit the sudoers file
```

Outro recurso útil para obter ajuda se tivermos problemas para entender um comando longo é: [https://explainshell.com/](https://explainshell.com/)