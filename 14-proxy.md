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



<a href="#porta">
  
## Configurar porta padrão do Squid para 8080


<a href="#navegador">
  
## Configurar navegadores para acessarem servidor proxy

<a href="#log">
  
## Analisar log de acesso ao servidor proxy

<a href="#acl">
  
## Criação de lista de controle de acesso (ACL) no servidor proxy
