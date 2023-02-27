## Descritores e redirecionamentos de arquivos

___

## Descritores de arquivo

Um descritor de arquivo (FD) em sistemas operacionais Unix/Linux é um indicador de conexão mantida pelo kernel para executar operações de Entrada/Saída (E/S). Em sistemas operacionais baseados no Windows, é chamado filehandle. É a conexão (geralmente a um arquivo) do sistema operacional para realizar operações de I/O (Entrada/Saída de Bytes). Por padrão, os três primeiros descritores de arquivo no Linux são:

1.  Fluxo de dados para entrada
    -   `STDIN – 0`
2.  Fluxo de Dados para Saída
    -   `STDOUT – 1`
3.  Fluxo de dados para saída relacionado à ocorrência de um erro.
    -   `STDERR – 2`

___

#### STDIN e STDOUT

Vejamos um exemplo com `cat`. ao correr `cat`, damos ao programa em execução nossa entrada padrão ( `STDIN - FD 0`), marcado `green`, em que neste caso "SOME INPUT" é. Assim que tivermos confirmado nossa entrada com `[ENTER]`, ele é retornado ao terminal como saída padrão ( `STDOUT - FD 1`), marcado em **vermelho** .

![ Imagem do](https://academy.hackthebox.com/storage/modules/18/find0.png)

___

#### STDOUT e STDERR

No próximo exemplo, usando o `find`comando, veremos a saída padrão ( `STDOUT - FD 1`) marcado em `green`e erro padrão ( `STDERR - FD 2`) marcada em vermelho.

STDOUT e STDERR

```
Denis-25@htb[/htb]$ find /etc/ -name shadow
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find1.png)

Nesse caso, o erro é marcado e exibido com " `Permission denied`". Podemos verificar isso redirecionando o descritor de arquivo para os erros ( `FD 2 - STDERR`) para " `/dev/null`." Dessa forma, redirecionamos os erros resultantes para o "dispositivo nulo", que descarta todos os dados.

STDOUT e STDERR

```
Denis-25@htb[/htb]$ find /etc/ -name shadow 2>/dev/null
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find2.png)

___

#### Redirecionar STDOUT para um arquivo

Agora podemos ver que todos os erros ( `STDERR`) apresentado anteriormente com " `Permission denied`" não são mais exibidos. O único resultado que vemos agora é a saída padrão ( `STDOUT`), que também podemos redirecionar para um arquivo com o nome `results.txt`que conterá apenas a saída padrão sem os erros padrão.

Redirecionar STDOUT para um arquivo

```
Denis-25@htb[/htb]$ find /etc/ -name shadow 2>/dev/null > results.txt
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find3.png)

___

#### Redirecione STDOUT e STDERR para arquivos separados

Deveríamos ter notado que não usamos um número antes do sinal de maior ( `>`) no último exemplo. Isso porque redirecionamos todos os erros padrão para o " `null device`" antes, e a única saída que obtemos é a saída padrão ( `FD 1 - STDOUT`). Para tornar isso mais preciso, redirecionaremos o erro padrão ( `FD 2 - STDERR`) e saída padrão ( `FD 1 - STDOUT`) para arquivos diferentes.

Redirecione STDOUT e STDERR para arquivos separados

```
Denis-25@htb[/htb]$ find /etc/ -name shadow 2> stderr.txt 1> stdout.txt
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find4.png)

___

#### Redirecionar STDIN

Como já vimos, em combinação com os descritores de arquivo, podemos redirecionar erros e saída com caractere maior que ( `>`). Isso também funciona com o sinal de menor que ( `<`). No entanto, o sinal de menor que serve como entrada padrão ( `FD 0 - STDIN`). Esses personagens podem ser vistos como " `direction`" na forma de uma seta que nos diz " `from where`" e " `where to`" os dados devem ser redirecionados. Usamos o `cat`comando para usar o conteúdo do arquivo " `stdout.txt`" Como `STDIN`.

Redirecionar STDIN

```
Denis-25@htb[/htb]$ cat < stdout.txt
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find5.png)

___

#### Redirecionar STDOUT e anexar a um arquivo

Quando usamos o sinal de maior que ( `>`) para redirecionar nosso `STDOUT`, um novo arquivo será criado automaticamente se ainda não existir. Se este arquivo existir, ele será substituído sem solicitar confirmação. Se quisermos anexar `STDOUT`ao nosso arquivo existente, podemos usar o duplo sinal de maior que ( `>>`).

Redirecionar STDOUT e anexar a um arquivo

```
Denis-25@htb[/htb]$ find /etc/ -name passwd >> stdout.txt 2>/dev/null
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find9.png)

___

#### Redirecionar fluxo STDIN para um arquivo

Também podemos usar os caracteres duplos menores que ( `<<`) para adicionar nossa entrada padrão por meio de um fluxo. Podemos usar o chamado `End-Of-File` ( `EOF`) de um arquivo do sistema Linux, que define o final da entrada. No próximo exemplo, usaremos o `cat`comando para ler nossa entrada de streaming por meio do stream e direcioná-lo para um arquivo chamado " `stream.txt`."

Redirecionar fluxo STDIN para um arquivo

```
Denis-25@htb[/htb]$ cat << EOF > stream.txt
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find6.png)

___

#### Tubos

Outra forma de redirecionar `STDOUT`é usar tubos ( `|`). Estes são úteis quando queremos usar o `STDOUT`de um programa para ser processado por outro. Uma das ferramentas mais utilizadas é `grep`, que usaremos no próximo exemplo. Grep é usado para filtrar `STDOUT`de acordo com o padrão que definimos. No próximo exemplo, usamos o `find`comando para procurar todos os arquivos no " `/etc/`" diretório com um " `.conf`" extensão. Quaisquer erros são redirecionados para a " `null device`" ( `/dev/null`). Usando `grep`, filtramos os resultados e especificamos que apenas as linhas que contêm o padrão " `systemd`" deve ser exibido.

Tubos

```
Denis-25@htb[/htb]$ find /etc/ -name *.conf 2>/dev/null | grep systemd
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find7.png)

Os redirecionamentos funcionam, não apenas uma vez. Podemos usar os resultados obtidos para redirecioná-los para outro programa. Para o próximo exemplo, usaremos a ferramenta chamada `wc`, que deve contar o número total de resultados obtidos.

Tubos

```
Denis-25@htb[/htb]$ find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l
```

![imagem](https://academy.hackthebox.com/storage/modules/18/find8.png)

Servidores VPN

Aviso: Cada vez que você "trocar", suas chaves de conexão são regeneradas e você deve baixar novamente seu arquivo de conexão VPN.

Todas as instâncias de VM associadas ao antigo servidor VPN serão encerradas ao mudar para um novo servidor VPN.  
As instâncias PwnBox existentes mudarão automaticamente para o novo servidor VPN.
