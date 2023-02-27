## Descrição do prompt

___

O prompt do bash é fácil de entender e, por padrão, inclui informações como usuário, nome do host e diretório de trabalho atual. O formato pode ser mais ou menos assim:

```
<username>@<hostname><current working directory>$
```

O diretório inicial de um usuário é marcado com um til < `~`\> e é a pasta padrão quando fazemos login.

```
<username>@<hostname>[~]$
```

O cifrão, neste caso, representa um usuário. Assim que fizermos login como `root`, o personagem muda para um `hash`< `#`\> e fica assim:

Vemos aqui o mesmo que quando trabalhamos na GUI do Windows. Estamos logados como usuário em um computador com um nome específico e sabemos em qual diretório estamos quando navegamos em nosso sistema. O prompt do Bash também pode ser personalizado e alterado de acordo com nossas próprias necessidades. O ajuste do prompt do bash está fora do escopo deste módulo. No entanto, podemos olhar para o [bashrcgenerator](http://bashrcgenerator.com/) e [powerline](https://github.com/powerline/powerline) , o que nos dá a possibilidade de adaptar nosso prompt às nossas necessidades.
