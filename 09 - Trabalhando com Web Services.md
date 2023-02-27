## Trabalhando com Web Services

___

Outro componente essencial é a comunicação com os servidores web. Existem muitas maneiras diferentes de configurar servidores da Web em sistemas operacionais Linux. Um dos servidores web mais usados e difundidos, além do IIS e Nginx, é o Apache. Para um servidor web Apache, podemos usar módulos apropriados, que podem criptografar a comunicação entre navegador e servidor web (mod\_ssl), usar como servidor proxy (mod\_proxy) ou realizar manipulações complexas de dados de cabeçalho HTTP (mod\_headers) e URLs (mod\_rewrite ).

O Apache oferece a possibilidade de criar páginas da Web dinamicamente usando linguagens de script do lado do servidor. As linguagens de script comumente usadas são PHP, Perl ou Ruby. Outras linguagens são Python, JavaScript, Lua e .NET, que podem ser usadas para isso. Podemos instalar o servidor web Apache com o seguinte comando.

```
Denis-25@htb[/htb]$ apt install apache2 -y

Reading package lists... Done
Building dependency tree       
Reading state information... Done
Suggested packages:
  apache2-doc apache2-suexec-pristine | apache2-suexec-custom
The following NEW packages will be installed:
  apache2
0 upgraded, 1 newly installed, 0 to remove and 17 not upgraded.
Need to get 95,1 kB of archives.
After this operation, 535 kB of additional disk space will be used.
Get:1 http://de.archive.ubuntu.com/ubuntu bionic-updates/main amd64 apache2 amd64 2.4.29-1ubuntu4.13 [95,1 kB]
Fetched 95,1 kB in 0s (270 kB/s)   
<SNIP>
```

Depois de iniciá-lo, podemos navegar usando nosso navegador para a página padrão (http://localhost).

![imagem](https://academy.hackthebox.com/storage/modules/18/apache-default.png)

Esta é a página padrão após a instalação e serve para confirmar se o servidor web está funcionando corretamente.

___

## CURL

`cURL`é uma ferramenta que nos permite transferir arquivos do shell através de protocolos como `HTTP`, `HTTPS`, `FTP`, `SFTP`, `FTPS`, ou `SCP`. Esta ferramenta nos dá a possibilidade de controlar e testar sites remotamente. Além do conteúdo dos servidores remotos, também podemos visualizar solicitações individuais para observar a comunicação do cliente e do servidor. Usualmente, `cURL`já está instalado na maioria dos sistemas Linux. Este é outro motivo crítico para nos familiarizarmos com esta ferramenta, pois ela pode facilitar muito alguns processos posteriormente.

```
Denis-25@htb[/htb]$ curl http://localhost

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
  <!--
    Modified from the Debian original for Ubuntu
    Last updated: 2016-11-16
    See: https://launchpad.net/bugs/1288690
  -->
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <title>Apache2 Ubuntu Default Page: It works</title>
    <style type="text/css" media="screen">
...SNIP...
```

Na tag de título, podemos ver que é o mesmo texto do nosso navegador. Isso nos permite inspecionar o código-fonte do site e obter informações dele. No entanto, voltaremos a isso em outro módulo.

___

## Wget

Uma alternativa ao curl é a ferramenta `wget`. Com esta ferramenta podemos baixar arquivos de servidores FTP ou HTTP diretamente do terminal e serve como um bom gerenciador de downloads. Se usarmos o wget da mesma forma, a diferença para o curl é que o conteúdo do site é baixado e armazenado localmente, conforme o exemplo a seguir.

```
Denis-25@htb[/htb]$ wget http://localhost

--2020-05-15 17:43:52--  http://localhost/
Resolving localhost (localhost)... 127.0.0.1
Connecting to localhost (localhost)|127.0.0.1|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 10918 (11K) [text/html]
Saving to: 'index.html'

index.html                 100%[=======================================>]  10,66K  --.-KB/s    in 0s      

2020-05-15 17:43:52 (33,0 MB/s) - ‘index.html’ saved [10918/10918]
```

___

## Python 3

Outra opção muito utilizada quando se trata de transferência de dados é o uso do Python 3. Neste caso, o diretório raiz do servidor web é onde é executado o comando para iniciar o servidor. Para este exemplo, estamos em um diretório onde o WordPress está instalado e contém um "readme.html". Agora, vamos iniciar o servidor web Python 3 e ver se podemos acessá-lo usando o navegador.

```
Denis-25@htb[/htb]$ python3 -m http.server

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```

![imagem](https://academy.hackthebox.com/storage/modules/18/python3-browser.png)

Podemos ver quais solicitações foram feitas se olharmos agora para os eventos do nosso servidor web Python 3.

```
Denis-25@htb[/htb]$ python3 -m http.server

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
127.0.0.1 - - [15/May/2020 17:56:29] "GET /readme.html HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/css/install.css?ver=20100228 HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/images/wordpress-logo.png HTTP/1.1" 200 -
127.0.0.1 - - [15/May/2020 17:56:29] "GET /wp-admin/images/wordpress-logo.svg?ver=20131107 HTTP/1.1" 200 -
```
