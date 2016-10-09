---
layout: post
title: Desenvolvimento Android, facilitando a vida com AA (Android Annotations)
author: Rafael Pazini
comments: true
---

![Android in the rain](/assets/img/posts/android_rain.jpg)
 

Quando começamos a desenvolver para Android, logo de cara notamos que sempre teremos interações entre os arquivos XML e as classes Java, porque se não fosse assim não seria possível pegar as informações da UI ou atualizar os seus dados. E para isso temos que isntanciar os objetos, o que gera várias linhas de código, mas temos o **Android Annotations** para facilitar isso. <!--more-->

Todo mundo está acostumado com os *annotations* em Java, que é comum para alguns códigos como por exemplo em Servlets, Web services e assim por diante. Caso você não esteja se recordando do que é, o mais comum e que certamente você já usou é o `@Override`.


Limpando o código
=================

Com o Android Annotations podemos além de facilitar o desenvolvimento, conseguir dar uma limpada no código também e esta é uma das coisas mais interessantes no annotations. Nas aplicações Android sempre começamos instanciando os objetos dentro do método `onCreate`

~~~ java
public class MainActivity extends AppCompatActivity {

    private TextView scoreViewA;
    private TextView scoreViewB;

    private ImageView imgOneA;
    private ImageView imgTwoA;
    private ImageView imgOneB;
    private ImageView imgTwoB;
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        scoreViewA = (TextView) findViewById(R.id.scoreViewA);
        scoreViewB = (TextView) findViewById(R.id.scoreViewB);

        imgOneA = (ImageView) findViewById(R.id.img_team_a_1);
        imgTwoA = (ImageView) findViewById(R.id.img_team_a_2);
        imgOneB = (ImageView) findViewById(R.id.img_team_b_1);
        imgTwoB = (ImageView) findViewById(R.id.img_team_b_2);

        setValuesOfPlayers();
    }
}
~~~

Neste exemplo declaramos o `ContentView` que usaremos no XML e também instanciamos os `Views` que vamos utilizar, no caso 4 são ImageViews e 2 são TextViews todos declarados com na forma habitual do android. 

Agora vamos ver como o mesmo código fica com o AA.

~~~ java
@EActivity //declara o content view
public class MainActivity extends AppCompatActivity {
	
// marcação utilizada quando o nome de sua variável tem o mesmo nome que o ID do elemento no XML
    @ViewById TextView scoreViewA; 
    @ViewById TextView scoreViewB;
		
// marcação para declarar variável com um ID diferente no XML
    @ViewById(R.id.img_team_a_1) 
    ImageView imgOneA;
    @ViewById(R.id.img_team_a_2)
    ImageView imgTwoA;
    @ViewById(R.id.img_team_b_1)
    ImageView imgOneB;
    @ViewById(R.id.img_team_b_2)
    ImageView imgTwoB;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        setValuesOfPlayers();
    }
}
~~~

Pronto declaramos as variáveis e para utilizá-las basta setar os valores como já é feito atualmente, por exemplo, no TextView chamar a função `setText`. O código fica mais limpo e caso você não queira, não precisa nem de utilizar o método `onCreate`, neste exemplo eu utilizei apenas para declarar o content view e chamar o método `setValuesOfPlayers`. O content view pode ser declarado diretamente no `@EActivity`, que ficaria desta forma

~~~ java
@EActivity(R.layout.activity_main) //declara o content view
public class MainActivity extends AppCompatActivity {

   ...
   
}
~~~

Assim deixamos o código até mais legível e com menos *boilerplate*, facilitando a manutenção deste no futuro.

Implementação
=============

Você já deve estar doido se perguntando como implementar isto em seu projeto, bom agora vamos para esta parte. 

O AA não é nativo no android, por isso precisamos adicionar algumas configurações em nosso build para utilizarmos sem erros de compilação.

Primeiro você deve dicionar a dependencia do `android-apt` ao build do projeto.

~~~ groovy
dependencies {
   classpath 'com.android.tools.build:gradle:2.2.0'
        
    // Verifique a ultima versão do android-apt no site do desenvolvedor
    classpath 'com.neenbedankt.gradle.plugins:android-apt:1.8'
}
~~~

Agora no build do app iremos criar uma variável para colocar a versão atual do Android Annotations e depois adicionar alguns módulos de dependencia na compilação do mesmo. Dessa forma garantimos que o Android Studio irá interpretar e compilar nosso código com os novos recursos que o annotations proporciona. 

 





