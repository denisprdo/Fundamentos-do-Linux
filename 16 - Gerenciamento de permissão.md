## Gerenciamento de permissão

___

## Visão geral

No Linux, as permissões são atribuídas a usuários e grupos. Cada usuário pode ser membro de grupos diferentes, e a participação nesses grupos fornece ao usuário permissões adicionais específicas. Cada arquivo e diretório pertence a um usuário específico e a um grupo específico. Assim, as permissões para usuários e grupos que definiram um arquivo também são definidas para os respectivos proprietários. Quando criamos novos arquivos ou diretórios, eles pertencem ao grupo ao qual pertencemos e a nós. Todo o sistema de permissões nos sistemas Linux é baseado no sistema numérico octal e, basicamente, existem três tipos diferentes de permissões que podem ser atribuídas a um arquivo ou diretório:

-   ( `r`) - Ler
-   ( `w`) - Escreva
-   ( `x`) - Executar

As permissões podem ser definidas para o `owner`, `group`, e `others`como apresentado no próximo exemplo com suas permissões correspondentes.

```
Denis-25@htb[/htb]$ ls -l /etc/passwd

- rwx rw- r--   1 root root 1641 May  4 23:42 /etc/passwd
- --- --- ---   |  |    |    |   |__________|
|  |   |   |    |  |    |    |        |_ Date
|  |   |   |    |  |    |    |__________ File Size
|  |   |   |    |  |    |_______________ Group
|  |   |   |    |  |____________________ User
|  |   |   |    |_______________________ Number of hard links
|  |   |   |_ Permission of others (read)
|  |   |_____ Permissions of the group (read, write)
|  |_________ Permissions of the owner (read, write, execute)
|____________ File type (- = File, d = Directory, l = Link, ... )
```

___

## Alterar permissões

Podemos modificar as permissões usando o `chmod`comando, referências de grupo de permissão ( `u`\- proprietário, `g`\- Grupo, `o`\- outros, `a`\- Todos os usuários) e um \[ `+`\] ou um \[ `-`\] para adicionar, remova as permissões designadas. No exemplo a seguir, um usuário cria um novo script de shell pertencente a esse usuário, não executável e definido com permissões de leitura/gravação para todos os usuários.

```
cry0l1t3@htb[/htb]$ ls -l shell

-rwxr-x--x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

Podemos então aplicar `read`permissões para todos os usuários e veja o resultado.

```
cry0l1t3@htb[/htb]$ chmod a+r shell && ls -l shell

-rwxr-xr-x   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

Também podemos definir as permissões para todos os outros usuários para `read`usando apenas a atribuição de valor octal.

```
cry0l1t3@htb[/htb]$ chmod 754 shell && ls -l shell

-rwxr-xr--   1 cry0l1t3 htbteam 0 May  4 22:12 shell
```

Vejamos todas as representações associadas a ele para entender melhor como a atribuição de permissão é calculada.

```
Binary Notation:                4 2 1  |  4 2 1  |  4 2 1
----------------------------------------------------------
Binary Representation:          1 1 1  |  1 0 1  |  1 0 0
----------------------------------------------------------
Octal Value:                      7    |    5    |    4
----------------------------------------------------------
Permission Representation:      r w x  |  r - x  |  r - -
```

Se somarmos os bits definidos do `Binary Representation`atribuído aos valores de `Binary Notation`juntos, obtemos o `Octal Value`. o `Permission Representation`representa os bits definidos no `Binary Representation`usando os três caracteres, que reconhece apenas as permissões definidas com mais facilidade.

___

## Alterar proprietário

Para alterar o proprietário e/ou as atribuições de grupo de um arquivo ou diretório, podemos usar o `chown`comando. A sintaxe é como a seguir:

#### Sintaxe - chown

Sintaxe - chown

```
cry0l1t3@htb[/htb]$ chown <user>:<group> <file/directory>
```

Neste exemplo, "shell" pode ser substituído por qualquer arquivo ou pasta arbitrária.

Sintaxe - chown

```
cry0l1t3@htb[/htb]$ chown root:root shell && ls -l shell

-rwxr-xr--   1 root root 0 May  4 22:12 shell
```

___

## SUL & GUID

Além de atribuir permissões diretas de usuário e grupo, também podemos configurar permissões especiais para arquivos definindo o `Set User ID` ( `SUID`) e `Set Group ID` ( `GUID`) bits. Esses `SUID`/ `GUID`bits permitem, por exemplo, que os usuários executem programas com os direitos de outro usuário. Os administradores costumam usar isso para dar aos seus usuários direitos especiais para determinados aplicativos ou arquivos. A carta " `s`" é usado em vez de um " `x`". Ao executar tal programa, o SUID/GUID do proprietário do arquivo é usado.

Muitas vezes, os administradores não estão familiarizados com os aplicativos, mas ainda atribuem os bits SUID/GUID, o que leva a um risco de segurança elevado. Tais programas podem conter funções que permitem a execução de um shell a partir do pager, como o aplicativo " `journalctl`."

Se o administrador definir o bit SUID como " `journalctl`, qualquer usuário com acesso a este aplicativo pode executar um shell como `root`. Mais informações sobre este e outros aplicativos podem ser encontrados em [GTFObins](https://gtfobins.github.io/gtfobins/journalctl/) .