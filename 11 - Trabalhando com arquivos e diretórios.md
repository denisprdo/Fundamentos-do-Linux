## Trabalhando com arquivos e diretórios

___

## Criar, mover e copiar

Em seguida, vamos trabalhar com arquivos e diretórios e aprender como criar, renomear, mover, copiar e excluir. Primeiro, vamos criar um arquivo vazio e um diretório. Podemos usar `touch`para criar um arquivo vazio e `mkdir`para criar um diretório.

A sintaxe para isso é a seguinte:

#### Sintaxe - toque

Sintaxe - toque

```
Denis-25@htb[/htb]$ touch <name>
```

#### A sintaxe é mkdir

A sintaxe é mkdir

```
Denis-25@htb[/htb]$ mkdir <name>
```

Neste exemplo, nomeamos o arquivo `info.txt`e o diretório `Storage`. Para criá-los, seguimos os comandos e sua sintaxe mostrados acima.

#### Criar um arquivo vazio

Criar um arquivo vazio

```
Denis-25@htb[/htb]$ touch info.txt
```

#### Criar um diretório

Criar um diretório

```
Denis-25@htb[/htb]$ mkdir Storage
```

Podemos querer ter diretórios específicos no diretório e seria muito demorado criar esse comando para cada diretório. O comando `mkdir`tem uma opção marcada `-p`para adicionar diretórios pai.

Criar um diretório

```
Denis-25@htb[/htb]$ mkdir -p Storage/local/user/documents
```

Podemos ver toda a estrutura depois de criar os diretórios pai com a ferramenta `tree`.

Criar um diretório

```
Denis-25@htb[/htb]$ tree .

.
├── info.txt
└── Storage
    └── local
        └── user
            └── documents

4 directories, 1 file
```

Também podemos criar arquivos diretamente nos diretórios especificando o caminho onde o arquivo deve ser armazenado. O truque é usar o ponto único ( `.`) para informar ao sistema que queremos iniciar a partir do diretório atual. Portanto, o comando para criar outro arquivo vazio fica assim:

#### Criar userinfo.txt

Criar userinfo.txt

```
Denis-25@htb[/htb]$ touch ./Storage/local/user/userinfo.txt
```

Criar userinfo.txt

```
Denis-25@htb[/htb]$ tree .

.
├── info.txt
└── Storage
    └── local
        └── user
            ├── documents
            └── userinfo.txt

4 directories, 2 files
```

Com o comando `mv`, podemos mover e também renomear arquivos e diretórios. A sintaxe para isso se parece com isso:

#### Sintaxe - mv

Sintaxe - mv

```
Denis-25@htb[/htb]$ mv <file/directory> <renamed file/directory>
```

Primeiro, vamos renomear o arquivo `info.txt`para `information.txt`e, em seguida, mova-o para o diretório `Storage`.

#### Renomear arquivo

Renomear arquivo

```
Denis-25@htb[/htb]$ mv info.txt information.txt
```

Agora vamos criar um arquivo chamado `readme.txt`no diretório atual e copie os arquivos `information.txt`e `readme.txt`no `Storage/`diretório.

#### Criar readme.txt

Criar readme.txt

```
Denis-25@htb[/htb]$ touch readme.txt 
```

#### Mover arquivos para um diretório específico

Mover arquivos para um diretório específico

```
Denis-25@htb[/htb]$ mv information.txt readme.txt Storage/
```

Mover arquivos para um diretório específico

```
Denis-25@htb[/htb]$ tree .

.
└── Storage
    ├── information.txt
    ├── local
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt

4 directories, 3 files
```

Suponhamos que queremos ter o `readme.txt`no `local/`diretório. Então podemos copiá-los lá com os caminhos especificados.

#### Copiar readme.txt

Copiar readme.txt

```
Denis-25@htb[/htb]$ cp Storage/readme.txt Storage/local/
```

Agora podemos verificar se o arquivo está usando a ferramenta `tree`novamente.

Copiar readme.txt

```
Denis-25@htb[/htb]$ tree .

.
└── Storage
    ├── information.txt
    ├── local
    │   ├── readme.txt
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt

4 directories, 4 files
```

##### Exercício Opcional:

Use as ferramentas que já conhecemos para descobrir como deletar arquivos e diretórios.

Servidores VPN

Aviso: Cada vez que você "trocar", suas chaves de conexão são regeneradas e você deve baixar novamente seu arquivo de conexão VPN.

Todas as instâncias de VM associadas ao antigo servidor VPN serão encerradas ao mudar para um novo servidor VPN.  
As instâncias PwnBox existentes mudarão automaticamente para o novo servidor VPN.
