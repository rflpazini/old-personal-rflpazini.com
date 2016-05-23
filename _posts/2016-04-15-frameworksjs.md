---
layout: post
title: Frameworks JS, um bem necessário!
author: Rafael Pazini
comments: true
---

![Frameworks JS](/assets/img/posts/frameworks.jpg)

Se você trabalha ou pelo menos tem uma pequena relação com a web, provavelmente já deve ter notado que nos últimos dois anos um dos assuntos mais comentados são os **Frameworks Js**. Se você nunca ouviu falar de algum deles amigo, esta na hora de correr atrás!<!--more--> 

Existem várias frameworks no mercado, mas as que estão em alta no meio front-end são elas: Angular, React, Ember e Backbone. Estas 4 são as frameworks JavaScript mais utilizadas no momento.

Mas afinal, o que são estas frameworks?
---

Elas agilizam o desenvolvimento de novas aplicações para web, evitam recarregamentos desnecessários de página, facilitam o data binding e organizam nossa arquitetura de desenvolvimento pois implementam MVC *(mais um motivo para dizermos que elas facilitam a vida, organização é tudo...)*. 

Você deve estar se perguntando o porquê de elas estarem sendo tão cobiçadas no mundo do desenvolvimento?! Em um resumo, podemos dizer que elas nos ajudam a criar uma aplicação com UI mais responsivas, ou seja, as aplicações se tornam cada vez mais atrativas para o uso. Já que com o uso destas frameworks, carregamentos podem ser feitos em blocos dispensando a atualização total da página ou a navegação para uma nova área.

Agora que você já entendeu um pouco melhor sobre o que elas são. Vamos conversar um pouco sobre cada uma.

Angular
---

É feita e mantida pelo Google. Segundo a descrição que eles mesmo dão para sua framework ela da "super poderes" para seu HTML, já que para utilizar a mesma, você acrescenta algumas tags em seu html, é desta forma que os dados são processados pela framework.

Nela temos uma das questões mais amadas da framework o "two-way data binding", que permite com que as informações sejam atualizadas tanto do View quanto do Model. Esta forma de implementação do data binding reduz a quantidade de código necessária para criar novas dynamic views. Mas ao mesmo tempo que ela "facilita a vida" pode dificultá-la também, já que alimentando sua aplicação de dois lugares vai complicar o debug e prejudicar a performance.

Falando em performance, dependendo da complexidade da aplicação que está sendo criada, o Angular se torna lento devido a sua arquitetura. Apesar disto ela pode ser uma boa opção para aplicações que não sejam muito grandes em que o problema com a lentidão não apareça. 

A curva de aprendizado da mesma é um tanto quanto mais elevada, já que possui várias funções exclusivas do framework. Sua arquitetura tem algumas influências de Java *(já que a mesma foi produzida por desenvolvedores Java)*.

Sua versão 2.0 está sendo produzida e eles prometem corrigir este problema com a lentidão em aplicações complexas, pois estão reestruturando totalmente a framework.

Para aprender mais sobre o Angular, você pode visitar o site oficial do projeto 
[angularjs.org](https://angularjs.org/){:target="_blank"}, lá você encontra até um curso grátis do disponibilizado pelo CodeSchool sobre ele.

Ember
---

EmberJs é um framework mantido pela comunidade, foi criada em 2011 por Yehuda Katz, que também fazia parte do core team de Rails. 
Assim como o Angular tem uma auto descrição "uma framework para criar aplicações web ambiciosas" e da mesma maneira que Angular tem uma uma influência do Java, o Ember tem uma influência do Rails *(como eu disse, o seu criador fez parte do core team do Rails)*. 

Costumamos dizer que quando você trabalha com o Ember, você deve fazer as coisas do jeito dele. Quando você vai começar a criar um novo app a única coisa que precisa é do built-in, ali irão ficar as rotas, bibliotecas temporárias e tudo mais que você sempre tem que criar. Isso evita que você fique "recriando a roda" toda vez que começa uma nova aplicação, e sem perder tempo com isso você poderá se preocupar com as outras coisas que realmente serão importantes para o projeto.

Os criadores do Ember disponibilizaram uma ferramenta*(command line tool)* que se chama [Ember CLI](http://ember-cli.com){:target="_blank"}. Os desenvolvedores utilizam ela para minimizar CSS e JS, compilar o SASS entre outras coisas. Então se você já é desenvolvedor web deve estar se perguntando - Poxa, mas é um task runner? - Sim, exatamente. Ela faz o mesmo trabalho que o [Grunt](http://gruntjs.com){:target="_blank"} ou [Gulp](http://gulpjs.com){:target="_blank"} a única diferença é que foi desenvolvida para trabalhar com o Ember. Isso não significa que você deve trocar seu task runner atual por ela, mas caso ainda não tenha um de costume é interessante dar uma olhada neste.

O Ember também implementa o "two-way data binding", porém de uma forma diferente do Angular. Não vou entrar muito em detalhes, já que o time de desenvolvimento anunciou que nas próximas versões da framework irá abandonar esta implementação. 

Ela é uma excelente framework para trabalhar com projetos que variam de médios a grandes, existem algumas restrições que poderiam e irão ser melhoradas num futuro próximo - como a renderização server-side que atualmente não está 100%, mas os commits estão a todo vapor para melhorá-la.

A melhor forma de entender mais sobre o Ember, é acessando seu próprio site [emberjs.com](http://emberjs.com){:target="_blank"}. E para entender ainda mais sobre a mesma veja a página da [Comunidade](http://emberjs.com/community/){:target="_blank"}, lá você vai encontrar todos os canais que os desenvolvedores usam para se comunicar e como interagir com eles, tirar dúvidas e quem sabe até colaborar com algum commit.

React
---

Este é praticamente o "queridinho" do momento, o React foi criado em 2013 e é mantido pelo Facebook. Ele não tem nenhuma auto descrição ou algo do tipo, a única coisa que todos dizem e o facebook também é que o React é o V*(View)* do MVC.

A coisa mais legal do react é que ele é extremamente rápido, o que diferencia ele das demais frameworks. O responsável por esta agilidade é o Virtual DOM, quando fazemos alguma alteração na aplicação ela é primeiro escrita no virtual DOM que compara os dados com os dados que existem no Real DOM e só depois atualiza os dados, mandando apenas o que foi alterado e não as informações completas. Isso aumenta e muito o desempenho da aplicação, já que as alterações no Real DOM são feitas quase que em segundo plano.

Outra parte bastante interessante desta framework é o desenvolvimento em componentes. Você pode criar componentes e reutiliza-los quando e quantas vezes quiser, diminuindo muito o tamanho dos códigos que você irá escrever. Aliás, este é o primeiro pensamento que qualquer um deve ter quando começa a trabalhar com React - no site oficial da framework existe um [artigo](https://facebook.github.io/react/docs/thinking-in-react.html){:target="_blank"} sobre isto - quebrar o layout em partes para começar a desenvolver a aplicação.

Além de rápido, o React é fácil de se aprender já que é praticamente JavaScript puro*(se você é familiar com JS vá em frente)*. Existe também o [React Native](http://facebook.github.io/react-native/){:target="_blank"} que permite criar aplicações para iOS e Android usando react.

Por ser a framework mais nova, o React está sempre em atualização. Então é importante ficar sempre de olho na documentação e nos blogs do Facebook onde todas as atualizações são postadas.

No site oficial do [ReactJs](https://facebook.github.io/react/index.html){:target="_blank"} além de toda a documentação e do passo a passo para iniciar a trabalhar com ele, você irá encontrar um pequeno tutorial para ir se familiarizando com a framework.

Backbone
---

O Backbone é um dos mais antigos frameworks desta seleção que estamos falando, sua primeira versão foi lançada em 2010. Uma de suas maiores vantagens é que ela é extremamente leve para uma framework, apenas 6.3kb. Alguns sites que usam o backbone são Twitter e Pinterest.

Ele é bem versátil e minimalista, por exemplo ele não vem com sua própria "template engine" *(além do básico que é o Underscore)*, deixando assim o desenvolvedor fazer suas próprias escolhas, quais plugins utilizar, quais engines o que a torna muito flexível podendo adapta-la da forma que queremos trabalhar.

Por ela ser tão leve, ele brilha quando falamos de aplicações simples "single page" e exemplos disso são as redes sociais Twitter e Pinterest.

Como eu disse o backbone é bem minimalista e dependendo do seu nível de experiência com o desenvolvimento em JS, isso pode ser uma benção ou um desafio. Existem vários plugins e bibliotecas que podem ser utilizados no desenvolvimento com o Backbone, e quem decide isso é o desenvolvedor, configurando tudo manualmente. Então o que pode ser uma relação de amor para os mais experientes, pode se tornar um desafio para quebrar a cabeça para os marinheiros de primeira viagem.

Como de costume, toda a documentação necessária do Backbone se encontra no site oficial do framework [backbonejs.org](http://backbonejs.org){:target="_blank"}. Lá também existe uma coleção de projetos em que ele é utilizado, assim você pode tirar uma base de como funciona na prática.

Mão na massa
---

Agora que você conhece um pouco mais das características de cada um deles, é hora de escolher o que você sentiu mais afinidade e como dizemos "meter a cara" na documentação, implementar alguns projetos e ir se acostumando com as arquiteturas.

O futuro do desenvolvimento de aplicações web realmente utilizará as frameworks. Então não custa nada saber utilizá-las. Em muitos vagas de empregos, elas já são um item requerido *(pelo menos uma delas)*. E colocar que você tem domínio de uma delas no CV irá lhe dar um brilho extra.

Uma dica para quem está começando a aprender novas tecnologias é utilizar*(e muito)* o [StackoverFLow](http://stackoverflow.com){:target="_blank"}. Lá você faz perguntas, responde e o mais legal é que pode encontrar com as pessoas responsáveis pelos projetos. Por exemplo, o ember utiliza ele como um dos principais meios de comunicação, seus desenvolvedores estão sempre respondendo as questões sobre a framework no fórum. Mãos a obra!






 







