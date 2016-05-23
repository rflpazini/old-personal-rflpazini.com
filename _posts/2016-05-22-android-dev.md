---
layout: post
title: Desenvolvimento Android, começando com o pé direito
author: Rafael Pazini
---

![Android Starter Pack](/assets/img/posts/android_dev.jpg)

Praticamente há oito meses comecei a desenvolver para android nativo, já havia trabalhado antes com desenvolvimento android, mas usando o Adobe air e convenhamos que apesar de ser legal não oferece a mesma flexibilidade que o desenvolvimento nativo. Então resolvi mostrar o "caminho das pedras" neste post. <!--more-->

No início deste ano comecei a ter aulas de desenvolvimento android na faculdade e percebi uma certa dificuldade dos meus colegas de classe para entender como funciona o desenvolvimento. Alguns dos principais desafios era com a IDE, configurações de SDK e de JDK que são o inicio de tudo, mesmo antes de você começar a desenvolver algum projeto, deve configurar o ambiente de desenvolvimento. Isto é básico em qualquer linguagem ou plataforma de desenvolvimento. Vamos começar por estas dicas.

Ambiente de desenvolvimento
===========================
Nessa fase o que menos importa é o SO que você está utilizando, pois pode ser um ambiente Linux, Windows ou OS X. Independente da plataforma você conseguirá trabalhar normalmente. 

### JDK ###


Este é o primeiro passo quando estamos falando de Desenvolvimento Android. Como todos sabem, para desenvolver aplicativos nativamente o Android utiliza Java como linguagem padrão (agora com o NDK estão utilizando C++, mas não vamos nos aprofundar). O JDK *(Java Development Kit)* é a base para começar a desenvolver aplicativos Java, nele temos as máquinas virtuais do java, os compiladores e todas as ferramentas necessárias para o desenvolvimento.

Então, caso você ainda não tenha o JDK instalado em seu computador, faça o download do mesmo que está disponível na [página da Oracle](http://www.oracle.com/technetwork/pt/java/javase/downloads/index.html){:target="_blank"}. Escolha o sistema operacional que você utiliza, faça o download **PS: Baixe somente o JDK**. Por fim instale o JDK seguindo os comandos que ele pede, é uma instalação simples.

### IDE *Android Studio* ###

Logo que o desenvolvimento android teve início sua principal ferramenta de desenvolvimento era o Eclipse com ADT *(Android Developer Tools)*, mas com o passar do tempo acabou-se notando algumas dificuldades em utilizar plataformas de terceiros para o desenvolvimento. Hoje o Google disponibiliza uma IDE própria para desenvolvimento Android que é o [Android Studio](http://developer.android.com/sdk/index.html){:target="_blank"} ele foi baseado na versão open source da [IntelliJ IDEA](https://www.jetbrains.com/idea/){:target="_blank"}, uma das mais famosas e completas IDE's para desenvolvimento Java. 

Até um tempo atrás o Android Studio possuía alguns bugs, mas com o lançamento da versão 2.0 praticamente todos estes bugs foram extintos e o ambiente ficou muito mais estável desde a máquina virtual até a forma de compilação. E a tendência é ele ficar ainda melhor, já que a versão 2.2 está em desenvolvimento*(até o momento do post)*. 

A primeira coisa que você deve fazer é o download do Android Studio no site oficial. Para os **usuários de Windows** recomendo que prestem atenção no download que irão efetuar, pois existem 3 tipos de download para esta plataforma - *(baixem a versão que já vem com o SDK, assim evitarão dores de cabeça com configuração de SDK futuramente)*. Agora é só instalar a IDE, **para usuários Linux** dependendo da versão que estão rodando, é necessário a instalação das bibliotecas x86. Isto é comum no Ubuntu e no Debian x64, caso aconteça algum erro na instalação como por exemplo, o Android Studio não consegue encontrar o SDK ou algo parecido, é só instalar as bibliotecas digitando estes comandos no terminal:

~~~~~~~~
$ sudo apt-get install lib32z1 lib32ncurses5 lib32stdc++6
~~~~~~~~

Se quiser ler mais sobre o [Issue 82711](https://code.google.com/p/android/issues/detail?id=82711){:target="_blank"} fique a vontade. Tanto no Linux quanto no OS X a IDE fará os downloads do SDK durante a instalação, então não se preocupe se demorar um pouco. Quando tudo ocorrer bem você verá a tela de welcome do Android studio.

![Android Studio Welcome Screen](/assets/img/posts/androidstudio_welcome.jpg)

A configuração de nosso ambiente de trabalho é uma coisa simples, apenas um pouco trabalhosa e dependendo de sua conexão de internet, pode ser um pouco demorada também.


Iniciando os trabalhos
======================
Agora que já temos nosso ambiente de desenvolvimento configurado vamos entender um pouco melhor o Android Studio, saber o que os painéis nos dizem e como podemos usá-los a nosso favor.

### A interface do Android Studio ###
![Android Studio Project Screen](/assets/img/posts/android_interface.jpg)

Como  eu disse no começo deste post, a interface do AS é baseado no IntelliJ IDEA. Então se você já é familiarizado com ela, não irá estranhar nem um pouco. Na figura acima, estão destacados 5 pontos que são os mais importantes da IDE e que sempre nos auxiliam na hora do desenvolvimento. Vamos a eles: 

1. A **barra de ferramentas** é onde temos controle sobre o projeto e acessamos as principais ferramentas da IDE, como a *run*, *debug*, *avd*, etc.
2. A **barra de navegação** te mostra o caminho do arquivo em que está mexendo, é muito útil para se localizar dentro do sistema.
3. **Janela de edição**, é aqui que a mágica acontece, onde escrevemos os códigos e podemos editar os arquivos visuais.
4. **Janelas de ferramentas** aqui podemos ter acesso a tarefas específicas, ver o que está acontecendo com o dispositivo, ver o controle de versão. De muita atenção a estas áreas, pois todos os projetos sempre dependerão delas.
5. A **barra de status** mostra todas as informações sobre o que está acontecendo com a IDE, mensagens de processos, avisos, erros e assim por diante.

Conforme você for desenvolvendo seu app ou fazendo os testes para se acostumar com essa interface, vai reparar que estas áreas são muito úteis. Você também pode modificá-las para deixar a IDE com sua cara, dando mais espaço e melhorando seu fluxo de trabalho.

Um dos jeitos que mais gosto de trabalhar é com o modo livre de distração ativado *(Distraction Free Mode)*, ele permite focar completamente na classe que estamos desenvolvendo visualizando apenas o código, sem os painéis na lateral. É bem útil quando se quer focar completamente, basta colocar o fone de ouvido, ligar a música no máximo e deixar a "mágica" acontecer :D.

![Android Studio Distraction Free Mode](/assets/img/posts/android_distraction-free.jpg)

### Estrutura do projeto ###


No Android Studio temos um controle total do projeto através do painel lateral da esquerda. Por ele conseguimos adicionar novos arquivos, ver a estrutura de pastas, estrutura de arquivos e assim por diante. 

![Android Studio Project Structure](/assets/img/posts/android_project-structure.jpg)

Neste painel basicamente você verá o projeto dividido em duas partes. A primeira se chama "app" que é onde encontramos todos os arquivos relacionados a nossa aplicação, ela é dividida em três partes: *manifests*, *java* e *res*. A manifests é onde fica o arquivo de configuração do android, ele recebe as permissões e faz as configurações iniciais de nossa aplicação, como setar o nome, exibir o ícone de inicialização e definir o tema da aplicação. Na parte de Java é onde ficam todos os arquivos de código de nossa aplicação, pacotes de teste e essas coisas. No res, que tem este nome por se referir aos *Resources* de nossa aplicação, vamos encontrar todos os arquivos referentes aos layouts, tema, imagens, enfim a parte visual de nossa aplicação fica nesta parte.

Logo abaixo desta primeira seção que ficam os arquivos do Gradle, que são os responsáveis por compilar nossa aplicação. Quando precisamos adicionar novas extensões, plugins ou algo do tipo, sempre utilizamos esta seção, pois o grade baixará e adicionará o os arquivos automaticamente para nosso projeto. Iremos falar dele daqui a pouco.

Esta é a estrutura básica de toda aplicação android, sempre que você for trabalhar com um projeto nativo, ele será dividido desta forma. Ao meu ver é uma maneira simples e fácil de nos localizarmos dentre os arquivos. Basta nos acostumar com a estrutura.

### Gradle ###

O [Gradle](http://gradle.org){:target="_blank"} é uma ferramenta de build muito poderosa, multi plataformas e foi adotado como padrão para o android. Ele é o responsável por adicionar plugins e fazer o build de nossa aplicação, sempre que você clicar em "run" ele começará a executar as tarefas para criar a aplicação. Não se esqueça de que ele é seu amigo, sempre irá te ajudar a achar os erros também quando começar a fazer o build, ele indica o que está errado no painel de mensagens da aplicação. Algumas das vantagens de utilizar o Gradle são:

* Customizar, configurar e extender o processo de build.
* Criar múltiplos APKs para o seu app, com diferentes features utilizando os mesmos módulos e mesmo projeto.
* Reutilizar códigos e resources

Você sempre utilizará o arquivo `build.gradle` para adicionar à compilação os arquivos que deseja, por exemplo, em uma aplicação que terá o [Google Play Services](https://developers.google.com/android/guides/overview#the_google_play_services_client_library){:target="_blank"} para seder algum serviço você será necessário adicionar nas dependências do arquivo build a seguinte linha de comando.

~~~ gradle
apply plugin: 'com.android.application'
    ...

    dependencies {
        compile 'com.google.android.gms:play-services:9.0.0'
    }
    
~~~

Não precisamos nos aprofundar muito neste assunto, basicamente temos que entender para o que ele serve, como ele nos ajuda e como utilizá-lo. Caso queira ler mais sobre o assunto, no [site oficial](http://gradle.org/getting-started-android/){:target="_blank"} existem alguns materiais para quem está começando, não custa dar uma olhada.


### Verificando updates de SDK ###

A última parte deste post vamos falar um pouco dos updates e instalação de outros SDKs. Uma coisa muito importante que temos que saber é que não temos que fazer o download de todas as imagens de sistema, ou ferramentas que o android studio nos oferece quando vamos utilizar um novo SDK.

O que realmente precisamos para começar a desenvolver uma aplicação quando iremos instalar um novo SDK são basicamente dois downloads, *SDK Platform* e a imagem do sistema para utilizarmos no emulador. Existem também os Build-tools, Platform-Tools e SDK Tools que desde que não estejam em uma versão beta o android studio irá baixá-los automaticamente.

![Android Studio SDK Manager](/assets/img/posts/android_sdk-manager.jpg)

Na figura acima temos a configuração do Android N(preview) no Android Studio, apenas estão instalados o SDK e a imagem do sistema para o celular/tablet. Como não será um projeto para a Android TV ou Android Wear, não é necessário instalar as imagens destes dispositivos. Isso nos ajuda a economizar algum tempo de download e instalação das imagens de sistema em nosso computador. A dica que deixo nesta parte é, veja qual será o alvo do seu app e baixe apenas a imagem do dispositivo que irá recebe-lo.

Bom estas são as dicas para quem está começando com o desenvolvimento Android. Creio que as principais dificuldades dos iniciantes foram tratadas aqui. Mas lógico que cada um é cada um, então se por um acaso você ainda tem alguma dúvida que não foi esclarecida neste post, por favor, fique a vontade para entrar em contado comigo em alguma rede social. Ficarei muito feliz em poder ajudar ;D !




