---
layout: post
title:  "Gerenciando serviços com systemctl"
date:   2020-05-05
permalink: "/post/gerenciando-servicos-com-systemctl"

categories: linux 
author: Bruno Bastos

---

Saudações confederados!


Gerenciar os serviços em seu SO pode parecer um pouco confuso se você é um iniciante no Linux. Nesse tutorial iremos conhecer os recursos básicos para gerenciarmos nossos serviços.


## Introdução
Um serviço Linux, bem resumidamente é um _daemon_. 

O daemon é um programa que roda em _background_, ou seja, ele trabalha em plano de fundo em vez de estar sob controle direto do usuário. Se você tem algum servidor http _(apache, nginx)_ instalado em sua máquina, ou algum banco de dados _(mysql, mariadb, postgreSql)_, você já deve ter notado que eles iniciam automaticamente assim que o sistema é liberado para uso, mas como isso é possível? Cortesia do Systemd.

O Systemd é o primeiro processo que assume controle do kernel após o boot. Sendo assim, os daemons são carregados a partir dele. Ora, então todos os meus serviços que iniciam automaticamente _(mariadb, nginx, ...)_ são inicializados pelo Systemd? 

Sim, e tem mais!

Para interagirmos com o Systemd nós utilizamos o comando systemctl, que nos fornece alguns recursos como habilitar e desabilitar um serviço _(nosso objetivo)_. 


## Gerenciando Serviços
Abra seu terminal e digite o seguinte comando:

{% highlight console %}
$ systemctl list-unit-files --type=service
{% endhighlight %}

Você receberá uma lista com todos os seus serviços, parecida com essa.

{% highlight console %}
UNIT FILE                                  STATE          
...            
apache2.service                            disabled       
apache2@.service                           disabled  
postgresql.service                         enabled        
...
{% endhighlight %}

Antes de entendermos essa lista vamos entender o nosso comando. 

O **systemctl** recebe como parametro o `list-unit-files`, que irá listar todos os arquivos instalados, em `type=service`, filtramos para trazer apenas os serviços.

Nosso resultado é composto por duas colunas, representada pelo nome do serviço e seu respectivo status. Observe que o meu serviço do postgresql está habilitado, ou seja, quando meu sistema operacional inicializar, o postgresql será inicializado também. 

Para desativar um serviço na inicialização utilize o seguinte comando, alterando  [service_name] para o serviço que deseja desativar: 

{% highlight console %}
$ sudo systemctl disable [service_name]
{% endhighlight %}

Caso deseja ativar o serviço novamente, utilize o seguinte comando:

{% highlight console %}
$ sudo systemctl enable [service_name]
{% endhighlight %}

Se você digitar o `systemctl list-unit-files --type=service` em seu terminal, e buscar os serviços que desativou, verá que agora eles estão disable. Porém isso não significa que esses serviços não estejam rodando, para verificar se um serviço está ou não rodando, você pode executar o seguinte comando:

{% highlight console %}
$ systemctl status [service_name]
{% endhighlight %}

A saidá será algo assim:

{% highlight console %}
● postgresql.service - PostgreSQL RDBMS
   Loaded: loaded (/lib/systemd/system/postgresql.service; disabled; vendor preset: enabled)
   Active: active (exited) since Tue 2020-05-05 10:42:03 -03; 2h 49min ago
 Main PID: 2125 (code=exited, status=0/SUCCESS)
{% endhighlight %}

Observe o `Active:active`, isso significa que nosso serviço está rodando, para desativa-lo na sessão atual você pode executar o seguinte comando:

{% highlight console %}
$ systemctl stop [service_name]
{% endhighlight %}

E para iniciar um serviço, você pode executar:

{% highlight console %}
$ systemctl start [service_name]
{% endhighlight %}


## Conclusão
Aprendemos o básico sobre o Systemctl e Systemd, eu espero que a leitura tenha sido proveitosa e o conhecimento adquirido. As recomendações são, leia sobre o Systemd, Systemcli e repasse o conhecimento. 

_"Tudo vale a pena quando a alma não é pequena"_ - Fernando Pessoa