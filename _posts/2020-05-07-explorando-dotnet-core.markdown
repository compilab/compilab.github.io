---
layout: post
title:  "Explorando o .Net Core"
date:   2020-05-07
permalink: "/post/explorando-dotnet-core"

categories: dotnet
author: Bruno Bastos

---

Saudações confederados!

Você já ouviu falar em .Net core?
Pois bem, diferentemente da plataforma .net framework, que trabalha apenas em sistema operacional Windows, o .net Core é uma plataforma desenvolvida pela Microsoft, que opera tanto em Windows, Linux e MacOs. Com ela você pode continuar com o Linux Debian, codar em C# e gerar dlls e todos aqueles artefatos que só viamos no windows. Ficou curioso em como isso funciona? Então esse artigo é para você.


## Introdução
O .Net core é uma revolução vinda da microsoft, pois o .net core é uma plataforma cruzada e de código aberto. Isso mesmo que você leu, código aberto. Quem imaginou isso um dia?

Para utilizarmos o .net Core, vamos precisar instalar o SDK, mas o que é um SDK?

O SDK _(Software development kit)_ do .net Core é um conjunto de bibliotecas e ferramentas que permite o desenvolvimento de aplicações, o download pode ser feito no [site da microsoft](https://dotnet.microsoft.com/download), você só precisa escolher seu SO e baixa-lo. Simples assim :)

O SDK inclue alguns componentes, sendo eles:
- O CLI
- O Runtime 
- O driver dotnet

O **CLI** do .net Core são ferramentas para o desenvolvimento, construção, execução e publicação de suas aplicações. O CLI também disponibiliza alguns comandos, que por sinal são bem intuitivos, como o comando `dotnet new [options]` para criar uma aplicação, ou `dotnet build` para realizar o build de sua aplicação. Todos os comandos podem ser visualizados com o comando `dotnet --help` ou na página [microsoft docs](https://docs.microsoft.com/pt-br/dotnet/core/tools/).

Falando no comando `dotnew new ...`, vou te mostrar algo interesse. Abra o terminal e digite `dotnet new --help`.

{% highlight terminal %}
Templates                               Short Name               Language          Tags  
-------------------------------------------------------------------------------------------------
Console Application                     console                  [C#], F#, VB      Common/Console                       
Class library                           classlib                 [C#], F#, VB      Common/Library                       
WPF Application                         wpf                      [C#]              Common/WPF                           
WPF Class library                       wpflib                   [C#]              Common/WPF        

...        
{% endhighlight %}

Se você executou o comando, você pode ver uma tabela em sua tela, que por sinal é bem maior que essa, eu selecionei apenas as primeiras linhas para mostrar a magnificência do .net Core.

Essa tabela representa que tipo de projeto você deseja criar e em qual linguagem. Você quer desevolver uma aplicação web? uma api? uma lib? Bom, o .net core é generoso e nos entrega um template base para o desenvolvimento. Utilizando o shortname, você pode inicar um projeto rapidamente, por exemplo: `dotnet new classlib -o mylib`, estou dizendo ao dotnet para criar um novo projeto do tipo classlib dentro do diretorio mylib.

Um outro ponto bem interessante é que a plataforma .net Core já nos disponibilza três linguagens de programação (veja na terceira coluna da tabela), sendo elas C#, F# e VB.

Incrivel, não?  Bom, estamos apenas começando, vamos para o próximo item do SDK, o runtime.

O **Runtime**, bem resumidamente, ajuda a facilitar o processo de desenvolvimento fornecendo os vários serviços. No universo .net Core, o runtime utilizado é o **CoreCLR** _(Core Common Language Runtime)_. 

Acima vimos que o .net Core já nos disponibliza três linguagens de programação, e ai você deve estar se perguntando, como o CoreCLR gerencia tudo isso?

Para cada linguagem da plataforma .net core, há um complicador especifico que implementa as especificações chamadas de **CLS** _(Common language Specification)_, que basicamente definem uma série de padrões que o compilador deve seguir para corresponder um bytecode chamado **CIL** _(Common Intermediate Language)_.

Um pouco Confuso? 


Veja assim, independente da linguagem que você use na plataforma .net Core, os seus respectivos compilares irão gerar um CIL. Pois o CIL é a linguagem que o CoreCLR trabalha. Se você é um programador java, fica bem mais fácil de entender, você pode ver o CIL como bytecode e o o CoreCLR com a JVM.

Legal, então depois de convertermos as linguagens para o CIL, o que acontece? O que o CoreCLR faz internamente é incluir o **JIT** _(Just-in-time)_ para compilar o código CIL em código de máquina na medida em que vamos interagindo com a aplicação.

Isso tudo é muito incrível, pois independente da linguagem utilizada, ela será traduzida ao CIL e compilada pelo JIT. Tratando-se disso, tais artefatos permitem que as linguagens se comuniquem pelo CIL e  que a compilação seja feita em tempo de execução.

Tem algo mais? 

Sim! Além do JIT e do CLS, o CoreCLR também tem o **GC** _(Garbage Collector)_ e o **CTS** _(Common Type System)_. 

O GC explicarei em futuro artigo, onde falaremos sobre seus algoritmos, mas para  entendermos o CoreCLR irei dar uma breve descrição do Garbage Collector. o GC é responsável por fornecer e gerenciar automaticamente a memória. É um dos componentes mais importante para uma VM _(Virtual Machine)_, e portanto falaremos dele detalhadamente em um artigo posterior, mas é importante que você saiba que ele é o responsável pelo gerenciamento de memória.

O CTS é o descritor dos tipos de dados. Vimos que a plataforma .net core é composta por várias linguagens, e cada linguagem tem seus tipos de dados. É aqui que surge a necessidade do CTS, sendo responsável por entender todo o sistema de tipos de dados das linguagens do .net Core e traduzi-los em um modo que o CoreCLR possa entende-los.

Lendo um artigo do Dawid Sibiński, no  CodeJorney, vi uma imagem que me ajudou a entender mais facilmente todo esses componentes e seus processos.

<img src="https://i0.wp.com/www.codejourney.net/wp-content/uploads/2018/10/NetExecutionModel.png?w=639&ssl=1">


## Concluindo

Bastante informação? Sim! Mas com foco, **paciencia** e tempo, você pode ir muito além desse artigo. Use a imagem acima como um mapa, releia o artigo, escreva no **papel** a definição de cada componente, e estude também por outras fontes. Deixarei algumas logo abaixo.

- Aquitetura de execução .Net - [CodeJorney](https://www.codejourney.net/2018/10/net-internals-10-application-execution-model/)  (ingles)

- JIT - [wikipedia](https://pt.wikipedia.org/wiki/JIT) (português)

- Guia .Net Core - [Microsft Doc](https://docs.microsoft.com/pt-br/dotnet/core/) (português)

- CoreCLR - [GeeksforGeeks](https://www.geeksforgeeks.org/common-language-runtime-clr-in-c-sharp/) (inglês)

Bons estudos!

_"write once run anywhere"_ -  Sun MicroSystems