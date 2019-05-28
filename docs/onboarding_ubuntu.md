---
id: onboarding_ubuntu
title: Ubuntu
---

# UBUNTU GERAL

## TWEAKS

Podemos twekar algumas coisas nativas do ubuntu, como desabilitar animações, escolher ícones que irão aparecer no desktop, instalar extensões do ubuntu via browser, etc.. Para isso precisamos instalar o tweak tool, podemos fazer isso com o comando

```
sudo apt install gnome-tweak-tool
```  

## COLOCAR PREFERÊNCIA PARA IPV4

No arquivo abaixo temos que descomentar a linha que faz o ipv4 ser o preferêncial.
```
sudo nano /etc/gai.conf
```
Descomentar a linha:
```
precedence ::ffff:0:0/96  100
```
## AJUSTANDO DELAY DO VOLUME UBUNTU

Abrir o arquivo de config:
```
sudo vim /usr/share/X11/xkb/symbols/br
```
Comentar a seguinte linha:
```
modifier_map Mod3   { Scroll_Lock };
```
Deslogar e logar novamente.

## CRIAR UM PAR DE CHAVES SSH

Primeiramente criar a Key SSH:
```
ssh-keygen
```
Após, mostrar a chave pública para poder inserir nas configurações do Bitbucket:
```
cat ~/.ssh/id_rsa.pub
```

No site do Bitbucket, para inserir a chave pública, vá em: Bitbucket settings > SSH keys > Add Key. Inserir o nome de escolha e a cópia do cat da chave pública.cat ~/.ssh/id_rsa.pub

## RECONHECENDO FORMATO EXFAT NO LINUX!
```
sudo apt-get install exfat-fuse exfat-utils
```
## INSTALAR O ZSH E OH-MY-ZSH

Porque instalar o zsh? https://code.joejag.com/2014/why-zsh.html

Primeiro precisamos instalar o ZSH:
```
sudo apt install zsh
zsh --version
```
Depois precisamos definir ela como nossa shell padrão:
```
chsh -s $(which zsh)
```
A primeira vez que entrarmos no terminal com o ZSH sendo nossa shell padrão, ela irá pedir para criarmos um arquivo .zshrc, o ideal é ignorar essa etapa já que esse arquivo será criado pelo OH-MY-ZSH. Normalmente é a opção 0.

Após definirmos ela como padrão nós precisamos relogar no nosso usuário, ou então reiniciar o computador, depois disso confirmamos que ela é nossa shell padrão:
```
echo $SHELL
```
Depois disso podemos instalar o OH-MY-ZSH, que é um framework baseado no ZSH, normalmente podemos seguir os passos de instalação do próprio repositório, mas pra facilitar:
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```
# UBUNTU DEV

## CONFIGURANDO O .SSH/CONFIG

Para ter acesso aos servidores, a public key necessita estar já configurada no servidor. Após configurar o arquivo .ssh/config
```
vim .ssh/config
```
Após inserir os dados bases e infos do servidor:
```
Host *
    ForwardAgent yes
    StrictHostKeyChecking no
 
Host <nome>

    Hostname <ip>
    User ubuntu
```
## INSTALAR PACOTES BÁSICOS
```
sudo apt update
sudo apt install git curl wget zip vim composer
```
## INSTALAR O APACHE2

Precisamos instalar o apache2 para ser nosso webserver.e
```
sudo apt install apache2
```
Depois precisamos configurar o apache2, liberando o apache para conseguir ler os diretórios onde os projetos vão estar:
```
sudo vim /etc/apache2/apache2.conf
```
Na seção onde tem os diretórios, podemos liberar ele adicionando as linhas (sendo que \<path> é o lugar onde os seus projetos vão estar localizados):
```
<Directory <path>>
    AllowOverride All
    Require all granted
    Order allow,deny
    Allow from all
</Directory>
```
Depois precisamos configurar o usuário e o grupo que irá rodar o serviço do apache:

```
sudo vim /etc/apache2/envvars
```
Nesse arquivo podemos mudar as linhas, onde \<user> e \<group> é o seu user e grupo padrão do sistema operacional:
```
export APACHE_RUN_USER=<user>
export APACHE_RUN_GROUP=<user>
```
Também já podemos habilitar o mod_rewrite:
```
sudo a2enmod rewrite
```
Após isso reiniciamos o apache:
```
sudo service apache2 restart
```
## INSTALAR O NODE.JS

https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions

## ADICIONAR PPA DO ONDREJ

O comando irá adicionar um repositório ao nosso apt, que irá deixar disponivel a instalação das 3 versões PHP.
```
sudo add-apt-repository ppa:ondrej/php
```
## INSTALAR O PHP 5.6
```
sudo apt install php5.6 php5.6-{bz2,cli,common,curl,dba,dev,enchant,fpm,gd,gmp,imap,interbase,intl,json,ldap,mbstring,mcrypt,mysql,odbc,opcache,pgsql,phpdbg,pspell,readline,recode,snmp,soap,sqlite3,sybase,tidy,xml,xmlrpc,xsl,zip}
```
## INSTALAR O PHP 7.0
```
sudo apt install php7.0 php7.0-{bcmath,bz2,cli,common,curl,dba,dev,enchant,fpm,gd,gmp,imap,interbase,intl,json,ldap,mbstring,mcrypt,mysql,odbc,opcache,pgsql,phpdbg,pspell,readline,recode,snmp,soap,sqlite3,sybase,tidy,xml,xmlrpc,xsl,zip}
```
## INSTALAR O PHP 7.1
```
sudo apt install php7.1 php7.1-{bcmath,bz2,cli,common,curl,dba,dev,enchant,fpm,gd,gmp,imap,interbase,intl,json,ldap,mbstring,mcrypt,mysql,odbc,opcache,pgsql,phpdbg,pspell,readline,recode,snmp,soap,sqlite3,sybase,tidy,xml,xmlrpc,xsl,zip}
```
## INSTALAR O MOD DO PHP NO APACHE2
```
sudo apt install libapache2-mod-php5.6 libapache2-mod-php7.0 
```
## INSTALAR O XDEBUG

Primeiro precisamos instalar o xdebug, lembrando que quando instalamos ele, já estamos instalando para todas as versões do php.
```
sudo apt install php-xdebug
```
A configuração para rodar é muito simples, só precisamos editar o arquivo de configuração:
```
sudo vim /etc/php/<phpversion>/mods-available/xdebug.ini
```

Trocando \<phpversion> pela versão do php que desejamos habilitar (5.6, 7.0 ou 7.1), e colocar as linhas abaixo:
```
xdebug.remote_enable=true
xdebug.remote_autostart=true
```
Depois disso é só reiniciar o apache2 e receber as conexões do xdebug em sua IDE.

## LIGAR OS ERROS NO APACHE2

Por padrão o apache2 vem configurado para trabalhar em modo de produção, então temos que modificar algumas coisas para que os erros sejam mostrados.
```
sudo vim /etc/php/<phpversion>/apache2/php.ini
```
Modificar as seguintes linhas:
```
error_reporting = E_ALL
display_errors = On
display_startup_errors = On
```
Depois é só reiniciar o apache2.
```
sudo service apache2 restart
```
## INSTALAR O MYSQL
```
sudo apt install mysql-server
```
Depois de instalar precisamos trocar o plugin de autenticação do user root, de auth_socket para mysql_native_password, para isso podemos conectar ao mysql com sudo e executar:
```
sudo mysql
mysql> ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root';
mysql> FLUSH PRIVILEGES;
```
Depois de conectar no mysql com sudo.
Se quisermos liberar o user root para ser acessado via rede precisamos fazer mais duas modificações.

Primeiro temos que liberar o mysql server para ser acessado de qualquer IP, isso pode ser feito modificando a linha “bind-address” para “0.0.0.0” ao invés de “127.0.0.1”.

Segundo temos que mudar a qual ip nosso usuário root está bindado, por padrão ele vem bindado ao host “localhost”, sendo “root@localhost”. Usando um mysql gui podemos modificar isso para “root@%”, onde % é o wildcard.

## INSTALAR O GENERATE-MODMAN

https://github.com/mhauri/generate-modman

TRABALHANDO COM CLIENTES
IMPORTANDO O BANCO DE DADOS

\<path> = Path local onde baixamos o dumps \
\<cliente> = Nome do cliente que estamos trabalhando \
\<dbname> = Nome do banco de dados local que estamos criando \
\<user> = Nome do user local do banco de dados (normalmente root) \
\<pass> = Senha do user local do banco de dados (pode ser sem senha) 

Os dumps dos clientes estão disponíveis em uma pasta no Google Drive, após baixa-los em qualquer pasta, vamos ter dois arquivos:

\<path>/\<cliente>_structure.sql.gz \
\<path>/\<cliente>_data.sql.gz

Primeiro temos que ter um banco de dados criado, se o mesmo já existe e você deseja refaze-lo, pode executar o seguinte comando:
```
mysql -u'root' -p'pass' -e 'drop database <dbname>'
```
E depois executar o comando abaixo para criar o novo banco de dados:
```
mysql -u'root'  -p'pass' -e 'create database <dbname>'
```
Para importarmos localmente, podemos executar os seguintes comandos, desde que já tenhamos o banco de dados criado:
```
zcat <path>/<cliente>_structure.sql.gz | mysql -u'<user>' -p'<senha>' <dbname>
zcat <path>/<cliente>_data.sql.gz | mysql -u'<user>' -p'<senha>' <dbname> 
```
Ou se tiver só um com all:
```
zcat <path>/<cliente>_all.sql.gz | mysql -u'<user>' -p'<senha>' <dbname> 
```
## FALTA DO SYMLINK NO BANCO DE DADOS

Algumas vezes após fazer o procedimento de preparação para abertura do site no localhost, pode acontecer de faltar no banco de dados o symlink, assim ficando toda tela em branco. Para resolução:
```
INSERT INTO core_config_data (config_id, scope, scope_id, path, value) VALUES (NULL , ‘default’, ‘0’, ‘dev/template/allow_symlink’, ‘1’); 
```

## VERIFICANDO SE O CRON ESTA ATIVO

Um dos possíveis erros causados pelo cron não rodando é a falta de configuração no servidor do cliente, para verificar basta rodar dentro do servidor o comando:
```
crontab -e
```
E após verificar o \<path> se está correto:
```
* * * * * ! test -e /mnt/<cliente>/app/public/maintenance.flag && /bin/bash /mnt/<cliente>/app/public/scheduler_cron.sh --mode always
* * * * * ! test -e /mnt/<cliente>/app/public/maintenance.flag && /bin/bash /mnt/<cliente>/app/public/scheduler_cron.sh --mode default
```
## CRIANDO UM MÓDULO PARA O MAGENTO 1

Criar um repositório no seguinte formato (tudo minúsculo):

m1-\<vendor>-\<module>

No branch master desse novo repositório apenas vamos commitar o README.md (nome do módulo).

Vamos criar um novo branch a partir do master no formato “version-\<version>”, sendo o \<version> a versão do módulo que pode ser encontrada em “app/code/\<pool>/\<vendor>/\<module>/etc/config.xml” ou no site da compra do módulo.

Gerar o modman:
```
generate-modman
```
INSERINDO NO REPOSITÓRIO

Acessar servidor Renegade e inserir o módulo dentro de satis.json:
```
cd packages.souhibrido.com.br/
vim satis.json
```
Dentro do satis.json, colocar:
```
{
    “type”: “git“,
    “Url”: “ssh://git@altssh.bitbucket.org:443/hibrido/<module-name>.git”
},
```
E após usar o comando:
```
make
```
Aguardar:



E ao final conferir se esta disponível no https://packages.souhibrido.com.br/

## VERIFICANDO REPORT ERROR
```
cat public/var/report/<RECORDNUMBER>
```
