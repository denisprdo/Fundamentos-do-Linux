## Gerenciamento de usuários

___

O gerenciamento de usuários é uma parte essencial da administração do Linux. Às vezes, precisamos criar novos usuários ou adicionar outros usuários a grupos específicos. Outra possibilidade é executar comandos como um usuário diferente. Afinal, não é muito raro que usuários de apenas um grupo específico tenham permissões para visualizar ou editar arquivos ou diretórios específicos. Isso, por sua vez, nos permite coletar mais informações localmente na máquina, o que pode ser muito importante. Vamos dar uma olhada no exemplo a seguir de como executar o código como um usuário diferente.

#### Execução como usuário

Execução como usuário

```
Denis-25@htb[/htb]$ cat /etc/shadow

cat: /etc/shadow: Permission denied
```

#### Execução como root

Execução como root

```
Denis-25@htb[/htb]$ sudo cat /etc/shadow

root:<SNIP>:18395:0:99999:7:::
daemon:*:17737:0:99999:7:::
bin:*:17737:0:99999:7:::
<SNIP>
```

Aqui está uma lista que nos ajudará a entender e lidar melhor com o gerenciamento de usuários.

| **Comando** | **Descrição** |
| --- | --- |
| `sudo` | Execute o comando como um usuário diferente. |
| `su` | o `su`utilitário solicita credenciais de usuário apropriadas via PAM e alterna para esse ID de usuário (o usuário padrão é o superusuário). Um shell é então executado. |
| `useradd` | Cria um novo usuário ou atualiza as informações padrão do novo usuário. |
| `userdel` | Exclui uma conta de usuário e arquivos relacionados. |
| `usermod` | Modifica uma conta de usuário. |
| `addgroup` | Adiciona um grupo ao sistema. |
| `delgroup` | Remove um grupo do sistema. |
| `passwd` | Altera a senha do usuário. |

O gerenciamento de usuários é essencial em qualquer sistema operacional, e a melhor maneira de se familiarizar com ele é experimentar os comandos individuais em conjunto com suas várias opções.