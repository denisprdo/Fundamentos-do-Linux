## Navegação

___

Uma das melhores maneiras de aprender algo novo é experimentá-lo. Aqui, abordamos as seções sobre como navegar no Linux, criar, mover, editar e excluir arquivos e pastas, localizá-los no sistema operacional, diferentes tipos de redirecionamentos e quais são os descritores de arquivo. Em seguida, encontraremos alguns atalhos que facilitarão nosso trabalho com o shell. É recomendável experimentar em nossa VM hospedada localmente. Certifique-se de que criamos um instantâneo para nossa VM, caso nosso sistema seja danificado inesperadamente.

Comecemos pela navegação. Antes de percorrermos o sistema, temos que descobrir em qual diretório estamos. Podemos descobrir onde estamos com o comando `pwd`.

```
cry0l1t3@htb[~]$ pwd

/home/cry0l1t3
```

Apenas o `ls`comando é necessário para navegação. Possui muitas opções adicionais que podem complementar a exibição do conteúdo na pasta atual.

```
cry0l1t3@htb[~]$ ls

Desktop  Documents  Downloads  Music  Pictures  Public  Templates  Videos
```

```
cry0l1t3@htb[~]$ ls -l

total 32
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:37 Desktop
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Documents
drwxr-xr-x 3 cry0l1t3 cry0l1t3 4096 Nov 15 03:26 Downloads
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Music
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Pictures
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Public
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Templates
drwxr-xr-x 2 cry0l1t3 cry0l1t3 4096 Nov 13 17:34 Videos
```

No entanto, não veremos tudo o que está nesta pasta. Para listar o conteúdo de um diretório, não precisamos necessariamente navegar até lá primeiro. Também podemos usar " `ls`" para especificar o caminho onde queremos saber o conteúdo.

```
cry0l1t3@htb[~]$ ls -l /var/

total 52
drwxr-xr-x  2 root root     4096 Mai 15 18:54 backups
drwxr-xr-x 18 root root     4096 Nov 15 16:55 cache
drwxrwsrwt  2 root whoopsie 4096 Jul 25  2018 crash
drwxr-xr-x 66 root root     4096 Mai 15 03:08 lib
drwxrwsr-x  2 root staff    4096 Nov 24  2018 local 
<SNIP>
```

Podemos fazer o mesmo se quisermos navegar até o diretório. Para percorrer os diretórios, usamos o comando `cd`. Vamos mudar para o `/dev/shm`diretório. Claro, podemos ir para o `/dev`diretório primeiro e depois `/shm`. No entanto, também podemos entrar diretamente no caminho completo e pular diretamente para lá.

```
cry0l1t3@htb[~]$ cd /dev/shm

cry0l1t3@htb[/dev/shm]$
```

Como estávamos no diretório inicial antes, podemos voltar rapidamente para o último diretório em que estávamos.

```
cry0l1t3@htb[/dev/shm]$ cd -

cry0l1t3@htb[~]$ 
```

O shell também nos oferece a função auto-completar, que facilita a navegação. Se agora digitarmos `cd /dev/s`e depois pressione `[TAB] twice`, obteremos todas as entradas que começam com a letra " `s`" no diretório de `/dev/`.

```
cry0l1t3@htb[~]$ cd /dev/s [TAB 2x]

shm/ snd/
```

Se adicionarmos a letra " `h`" para a letra " `s`," o shell completará a entrada, caso contrário não haverá pastas neste diretório começando com as letras " `sh`". Se agora exibirmos todo o conteúdo do diretório, veremos apenas o seguinte conteúdo.

```
cry0l1t3@htb[/dev/shm]$ ls -la

total 0
drwxrwxrwt  2 root root   40 Mai 15 18:31 .
drwxr-xr-x 17 root root 4000 Mai 14 20:45 ..
```

A primeira entrada com um único ponto ( `.`) indica o diretório atual em que estamos. A segunda entrada com dois pontos ( `..`) representa o diretório pai `/dev`. Isso significa que podemos pular para o diretório pai com o seguinte comando.

```
cry0l1t3@htb[/dev/shm]$ cd ..

cry0l1t3@htb[/dev]$
```

Como nosso shell está preenchido com alguns registros, podemos limpar o shell com o comando `clear`. No entanto, voltemos ao diretório `/dev/shm`antes da.

```
cry0l1t3@htb[/dev]$ cd shm && clear
```

Servidores VPN

Aviso: Cada vez que você "trocar", suas chaves de conexão são regeneradas e você deve baixar novamente seu arquivo de conexão VPN.

Todas as instâncias de VM associadas ao antigo servidor VPN serão encerradas ao mudar para um novo servidor VPN.  
As instâncias PwnBox existentes mudarão automaticamente para o novo servidor VPN.
