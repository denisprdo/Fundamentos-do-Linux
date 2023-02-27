## Introdução ao Shell

___

É crucial aprender a usar o shell Linux, pois existem muitos servidores baseados em Linux. Eles são frequentemente usados porque o Linux é menos sujeito a erros do que os servidores Windows. Por exemplo, os servidores da Web geralmente são baseados no Linux. Saber como usar o sistema operacional para controlá-lo efetivamente requer entender e dominar a parte essencial do Linux, o `Shell`. Quando mudamos do Windows para o Linux, ele se parece com isto:

![ Imagem do](https://academy.hackthebox.com/storage/modules/18/first_linux2.png)

Um terminal Linux, também chamado de `shell`ou linha de comando, fornece uma interface de entrada/saída (I/O) baseada em texto entre usuários e o kernel para um sistema de computador. O termo console também é típico, mas não se refere a uma janela, mas a uma tela em modo texto. Na janela do terminal, comandos podem ser executados para controlar o sistema.

___

## Emuladores de terminal

Emuladores de terminal são frequentemente usados para isso. A emulação de terminal é um software que emula a função de um terminal. Ele permite o uso de programas baseados em texto dentro de uma interface gráfica do usuário ( `GUI`). Existem muitos emuladores de terminal diferentes, como `GNOME Terminal`, `XFCE4 Terminal`, `XTerm`, e muitos outros. Existem também as chamadas interfaces de linha de comando que são executadas como terminais adicionais em um terminal e, portanto, são `multiplexers`. Esses multiplexadores incluem `Tmux`, `GNU Screen`, e outros. Resumindo, um terminal serve como uma interface para o interpretador de shell.

Emuladores de terminal e multiplexadores são extensões benéficas para o terminal. Eles nos fornecem diferentes métodos e funções para trabalhar com o terminal, como dividir o terminal em uma janela, trabalhar em vários diretórios, criar diferentes espaços de trabalho e muito mais. Um exemplo do uso de tal multiplexador chamado Tmux poderia ser mais ou menos assim:

![imagem](https://academy.hackthebox.com/storage/modules/18/tmux.png)

___

## Shell

O shell mais comumente usado no Linux é o `Bourne-Again Shell` ( `BASH`) e faz parte do projeto GNU. Tudo o que fazemos por meio da GUI, podemos fazer com o shell. O shell nos dá muito mais possibilidades de interagir com programas e processos para obter informações mais rapidamente. Além disso, muitos processos podem ser facilmente automatizados com scripts menores ou maiores que facilitam muito o trabalho manual.

Além do Bash, também existem outros shells como [Tcsh/Csh](https://en.wikipedia.org/wiki/Tcsh) , [Ksh](https://en.wikipedia.org/wiki/KornShell) , [Zsh](https://en.wikipedia.org/wiki/Z_shell) , [Fish](https://en.wikipedia.org/wiki/Friendly_interactive_shell) shell e outros.
