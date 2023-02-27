## Segurança do Linux

___

Todos os sistemas de computador têm um risco inerente de invasão. Alguns apresentam mais riscos do que outros, como um servidor da Web voltado para a Internet que hospeda vários aplicativos da Web complexos. Os sistemas Linux também são menos propensos a vírus que afetam os sistemas operacionais Windows e não apresentam uma superfície de ataque tão grande quanto os hosts ingressados no domínio do Active Directory. Independentemente disso, é essencial ter certos fundamentos para proteger qualquer sistema Linux.

Uma das medidas de segurança mais importantes dos sistemas operacionais Linux é manter o sistema operacional e os pacotes instalados atualizados. Isso pode ser feito com um comando como:

```
Denis-25@htb[/htb]$ apt update && apt dist-upgrade
```

Se as regras de firewall não forem definidas adequadamente no nível da rede, podemos usar o firewall do Linux e/ou `iptables`para restringir o tráfego de entrada/saída do host.

Se o SSH estiver aberto no servidor, a configuração deve ser definida para não permitir login com senha e impedir que o usuário root faça login via SSH. Também é importante evitar entrar e administrar o sistema como usuário root sempre que possível e gerenciar adequadamente o controle de acesso. O acesso dos usuários deve ser determinado com base no princípio do menor privilégio. Por exemplo, se um usuário precisa executar um comando como root, esse comando deve ser especificado no `sudoers`configuração em vez de dar a eles direitos totais de sudo. Outro mecanismo de proteção comum que pode ser usado é `fail2ban`. Essa ferramenta conta o número de tentativas de login com falha e, se um usuário atingir o número máximo, o host que tentou se conectar será tratado conforme configurado.

Também é importante auditar periodicamente o sistema para garantir que não existam problemas que possam facilitar a escalação de privilégios, como um kernel desatualizado, problemas de permissão do usuário, arquivos graváveis por todo o mundo e cron jobs mal configurados ou serviços mal configurados. Muitos administradores se esquecem da possibilidade de algumas versões do kernel precisarem ser atualizadas manualmente.

Uma opção para bloquear ainda mais os sistemas Linux é `Security-Enhanced Linux` ( `SELinux`) ou `AppArmor`. Este é um módulo de segurança do kernel que pode ser usado para políticas de controle de acesso de segurança. No SELinux, todo processo, arquivo, diretório e objeto do sistema recebe um rótulo. As regras de política são criadas para controlar o acesso entre esses processos e objetos rotulados e são impostas pelo kernel. Isso significa que o acesso pode ser configurado para controlar quais usuários e aplicativos podem acessar quais recursos. O SELinux fornece controles de acesso muito granulares, como especificar quem pode anexar a um arquivo ou movê-lo.

Além disso, existem diferentes aplicativos e serviços como [Snort](https://www.snort.org/) , [chkrootkit](http://www.chkrootkit.org/) , [rkhunter](https://packages.debian.org/sid/rkhunter) , [Lynis](https://cisofy.com/lynis/) e outros que podem contribuir para a segurança do Linux. Além disso, algumas configurações de segurança devem ser feitas, como:

-   Removendo ou desabilitando todos os serviços e softwares desnecessários
-   Removendo todos os serviços que dependem de mecanismos de autenticação não criptografados
-   Certifique-se de que o NTP esteja ativado e o Syslog esteja em execução
-   Certifique-se de que cada usuário tenha sua própria conta
-   Reforce o uso de senhas fortes
-   Configure a duração da senha e restrinja o uso de senhas anteriores
-   Bloquear contas de usuário após falhas de login
-   Desative todos os binários SUID/SGID indesejados

Esta lista está incompleta, pois a segurança não é um produto, mas um processo. Isso significa que sempre devem ser tomadas medidas específicas para proteger melhor os sistemas e depende dos administradores o quanto eles conhecem seus sistemas operacionais. Quanto melhor os administradores estiverem familiarizados com o sistema e quanto mais treinados forem, melhores e mais seguras serão suas precauções e medidas de segurança.
