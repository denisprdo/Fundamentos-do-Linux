## Editando arquivos

___

Existem várias maneiras de editar um arquivo. Um dos editores de texto mais comuns para isso é `Vi`e `Vim`. Mais raramente, ocorre o `Nano`editor. Vamos primeiro lidar com o editor Nano aqui, pois é um pouco mais fácil de entender. Podemos criar um novo arquivo diretamente com o editor Nano especificando o nome do arquivo diretamente como primeiro parâmetro. Neste caso, criamos um novo arquivo chamado `notes.txt`.

```
Denis-25@htb[/htb]$ nano notes.txt
```

Agora devemos ver um chamado " `pager`" aberto, e podemos inserir ou inserir livremente qualquer texto. Nosso shell deve se parecer com algo assim.

#### NanoEditor

NanoEditor

```
  GNU nano 2.9.3                                    notes.txt                                              

Here we can type everything we want and make our notes.▓


^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify     ^C Cur Pos     M-U Undo
^X Exit        ^R Read File   ^\ Replace     ^U Uncut Text  ^T To Spell    ^_ Go To Line  M-E Redo
```

Abaixo vemos duas linhas com breves descrições. o `caret` ( `^`) representa o nosso " `[CTRL]`" chave. Por exemplo, se pressionarmos `[CTRL + W]`, uma " `Search:`" aparece na parte inferior do editor, onde podemos inserir a palavra ou palavras que estamos procurando. Se agora procurarmos a palavra " `we`" e pressione `[ENTER]`, o cursor se moverá para a primeira palavra correspondente.

NanoEditor

```
GNU nano 2.9.3                                    notes.txt                                              

Here ▓we can type everything we want and make our notes.

Search:   notes                                                                                            
^G Get Help    M-C Case Sens  M-B Backwards  M-J FullJstify ^W Beg of Par  ^Y First Line  ^P PrevHstory
^C Cancel      M-R Regexp     ^R Replace     ^T Go To Line  ^O End of Par  ^V Last Line   ^N NextHstory
```

Para pular para a próxima correspondência com o cursor, pressionamos `[CTRL + W]`novamente e confirme com `[ENTER]`sem nenhuma informação adicional.

NanoEditor

```
GNU nano 2.9.3                                    notes.txt                                              

Here we can type everything ▓we want and make our notes.

Search [we]:                                                                                               
^G Get Help    M-C Case Sens  M-B Backwards  M-J FullJstify ^W Beg of Par  ^Y First Line  ^P PrevHstory
^C Cancel      M-R Regexp     ^R Replace     ^T Go To Line  ^O End of Par  ^V Last Line   ^N NextHstory
```

Agora podemos salvar o arquivo pressionando `[CTRL + O]`e confirme o nome do arquivo com `[ENTER]`.

NanoEditor

```
GNU nano 2.9.3                                    notes.txt                                              

Here we can type everything we want and make our notes.

File Name to Write: notes.txt▓                                                                           
^G Get Help    M-C Case Sens  M-B Backwards  M-J FullJstify ^W Beg of Par  ^Y First Line  ^P PrevHstory
^C Cancel      M-R Regexp     ^R Replace     ^T Go To Line  ^O End of Par  ^V Last Line   ^N NextHstory
```

Depois de salvar o arquivo, podemos sair do editor com `[CTRL + X]`.

#### De volta à casca

Para visualizar o conteúdo do arquivo, podemos usar o comando `cat`.

De volta à casca

```
Denis-25@htb[/htb]$ cat notes.txt

Here we can type everything we want and make our notes.
```

Existem muitos arquivos em sistemas Linux que podem desempenhar um papel essencial para nós como testadores de penetração cujos direitos não foram definidos corretamente pelos administradores. Esses arquivos podem incluir o arquivo " `/etc/passwd`".

___

## VIM

`Vim`é um editor de código aberto para todos os tipos de texto ASCII, assim como o Nano. É um clone melhorado do Vi anterior. É um editor extremamente poderoso que se concentra no essencial, ou seja, na edição de texto. Para tarefas que vão além disso, o Vim fornece uma interface para programas externos, como `grep`, `awk`, `sed`, etc., que podem lidar com suas tarefas específicas muito melhor do que uma função correspondente implementada diretamente em um editor normalmente pode. Isso torna o editor pequeno e compacto, rápido, poderoso, flexível e menos sujeito a erros.

Vim segue o princípio Unix aqui: muitos pequenos programas especializados que são bem testados e comprovados, quando combinados e se comunicando entre si, resultando em um sistema flexível e poderoso.

#### VIM

VIM

```
Denis-25@htb[/htb]$ vim
```

VIM

```
  1 $
~
~                              VIM - Vi IMproved                                
~                                                                               
~                               version 8.0.1453                                
~                           by Bram Moolenaar et al.                            
~           Modified by pkg-vim-maintainers@lists.alioth.debian.org             
~                 Vim is open source and freely distributable                   
~                                                                               
~                           Sponsor Vim development!                            
~                type  :help sponsor<Enter>    for information                  
~                                                                               
~                type  :q<Enter>               to exit                          
~                type  :help<Enter>  or  <F1>  for on-line help                 
~                type  :help version8<Enter>   for version info                 
~                                                                               
                                                                         
                                                                    0,0-1         All
```

Ao contrário do Nano, `Vim`é um editor modal que pode distinguir entre texto e entrada de comando. Vim oferece um total de seis modos fundamentais que facilitam nosso trabalho e tornam este editor tão poderoso:

| **Modo** | **Descrição** |
| --- | --- |
| `Normal` | No modo normal, todas as entradas são consideradas como comandos do editor. Portanto, não há inserção dos caracteres inseridos no buffer do editor, como ocorre na maioria dos outros editores. Depois de iniciar o editor, geralmente estamos no modo normal. |
| `Insert` | Com algumas exceções, todos os caracteres inseridos são inseridos no buffer. |
| `Visual` | O modo visual é usado para marcar uma parte contígua do texto, que será destacada visualmente. Ao posicionar o cursor, mudamos a área selecionada. A área destacada pode ser editada de várias maneiras, como exclusão, cópia ou substituição. |
| `Command` | Ele nos permite inserir comandos de linha única na parte inferior do editor. Isso pode ser usado para classificar, substituir seções de texto ou excluí-las, por exemplo. |
| `Replace` | No modo de substituição, o texto inserido recentemente substituirá os caracteres de texto existentes, a menos que não haja mais caracteres antigos na posição atual do cursor. Em seguida, o texto recém-inserido será adicionado. |

Quando temos o editor Vim aberto, podemos entrar no modo de comando digitando " `:`" e depois digitando " `q`" para fechar o Vim.

VIM

```
  1 $
~
~                              VIM - Vi IMproved                                
~                                                                               
~                               version 8.0.1453                                
~                           by Bram Moolenaar et al.                            
~           Modified by pkg-vim-maintainers@lists.alioth.debian.org             
~                 Vim is open source and freely distributable                   
~                                                                               
~                           Sponsor Vim development!                            
~                type  :help sponsor<Enter>    for information                  
~                                                                               
~                type  :q<Enter>               to exit                          
~                type  :help<Enter>  or  <F1>  for on-line help                 
~                type  :help version8<Enter>   for version info                 
~                                                                               
:q▓
```

Vim oferece uma excelente oportunidade chamada `vimtutor`para praticar e se familiarizar com o editor. Pode parecer muito difícil e complicado no começo, mas só vai parecer assim por um curto período de tempo. A eficiência que ganhamos com o Vim quando nos acostumamos com ele é enorme.

#### VimTutorGenericName

VimTutorGenericName

```
Denis-25@htb[/htb]$ vimtutor
```

VimTutorGenericName

```
===============================================================================
=    W e l c o m e   t o   t h e   V I M   T u t o r    -    Version 1.7      =
===============================================================================

     Vim is a very powerful editor that has many commands, too many to
     explain in a tutor such as this.  This tutor is designed to describe
     enough of the commands that you will be able to easily use Vim as
     an all-purpose editor.

     The approximate time required to complete the tutor is 25-30 minutes,
     depending upon how much time is spent with experimentation.

     ATTENTION:
     The commands in the lessons will modify the text.  Make a copy of this
     file to practice on (if you started "vimtutor" this is already a copy).

     It is important to remember that this tutor is set up to teach by
     use.  That means that you need to execute the commands to learn them
     properly.  If you only read the text, you will forget the commands!

     Now, make sure that your Caps-Lock key is NOT depressed and press
     the   j   key enough times to move the cursor so that lesson 1.1
     completely fills the screen.
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
```

##### Exercício Opcional:

Brinque com o vimtutor. Familiarize-se com o editor e experimente seus recursos.