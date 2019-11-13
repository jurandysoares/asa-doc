# Proxy

## Objetivos de aprendizagem

* [Definir o que é um servidor proxy](#proxy)
* [Instalar servidor *squid* no Ubuntu servidor](#install)
* [Configurar porta padrão do Squid para 8080](#porta)
* [Configurar navegadores para acessarem servidor proxy](#navegador)
* [Analisar log de acesso ao servidor proxy](#log)
* [Criação de lista de controle de acesso (ACL) no servidor proxy](#acl)

## Arquivos, diretórios e comandos
* `/etc/squid/squid.conf`
* `/var/log/squid/access.log`
* `/var/log/squid/cache.log`

<a href="#proxy">
  
## Definir o que é um servidor proxy
* O que é um servidor proxy?
* Para que server?

<a href="#install">
  
## Instalar servidor *squid* no Ubuntu servidor
* `sudo apt update`
* `sudo apt install -y squid`

Após a instalação, recomendo a limpeza do arquivo de configuração, isto é, 
remover todos os comentários e linhas em branco. Para isso, vamos utilizar o 
editor [sed](https://aurelio.net/sed/).

Vamos utilizar expressões regulares para fazer a limpeza. Tenha ciência que:
* `/` significa procurar no sed;
* `^` significa início da linha;
* `$` significa fim de linha.

Assim:
* `/^#`: significa procurar linhas que comecem com comentário;
* `/^$`: significa procurar linhas em branco (só com um ENTER).

Por fim, `/d` no sed significa excluir (*delete* em Inglês).

Dito isso, execute:
* `sed -e '/^#/d' -e '/^$/d' /etc/squid/squid.conf`

Ou:
* `sed '/^#/d;/^$/d' /etc/squid/squid.conf`

Se você ficou contente com a limpeza, grave-a com a opção `-i` do *sed*:
* `sed -i '/^#/d;/^$/d' /etc/squid/squid.conf`

Caso tenha dado permissão negada, pense um pouco como resolver este problema.

Uma vez removidas as linhas em branco e com comentário, o arquivo de configuração
do squid deve ter ficado mais ou menos assim:

```
acl SSL_ports port 443
acl Safe_ports port 80          # http
acl Safe_ports port 21          # ftp
acl Safe_ports port 443         # https
acl Safe_ports port 70          # gopher
acl Safe_ports port 210         # wais
acl Safe_ports port 1025-65535  # unregistered ports
acl Safe_ports port 280         # http-mgmt
acl Safe_ports port 488         # gss-http
acl Safe_ports port 591         # filemaker
acl Safe_ports port 777         # multiling http
acl CONNECT method CONNECT
http_access deny !Safe_ports
http_access deny CONNECT !SSL_ports
http_access allow localhost manager
http_access deny manager
http_access allow localhost
http_access deny all
http_port 3128
coredump_dir /var/spool/squid
refresh_pattern ^ftp:           1440    20%     10080
refresh_pattern ^gopher:        1440    0%      1440
refresh_pattern -i (/cgi-bin/|\?) 0     0%      0
refresh_pattern (Release|Packages(.gz)*)$      0       20%     2880
refresh_pattern .               0       20%     4320
```

<a href="#porta">
  
## Configurar porta padrão do Squid para 8080
Podemos utilizar o 

<a href="#navegador">
  
## Configurar navegadores para acessarem servidor proxy

<a href="#log">
  
## Analisar log de acesso ao servidor proxy

<a href="#acl">
  
## Criação de lista de controle de acesso (ACL) no servidor proxy
