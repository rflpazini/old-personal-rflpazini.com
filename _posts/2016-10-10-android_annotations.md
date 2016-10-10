---
layout: post
title: Desenvolvimento Android, facilitando a vida com AA (Android Annotations)
author: Rafael Pazini
comments: true
---

![Android in the rain](/assets/img/posts/android_rain.jpg)
 

Quando começamos a desenvolver para Android, logo de cara notamos que sempre teremos interações entre os arquivos XML e as classes Java, porque se não fosse assim não seria possível pegar as informações da UI ou atualizar os seus dados. E para isso temos que instanciar os objetos, o que gera várias linhas de código *boilerplate*, mas temos o **Android Annotations** para facilitar isso. <!--more-->

Todo mundo está acostumado com os *annotations* em Java, que é comum para alguns códigos como por exemplo em Servlets, Web services e assim por diante. Caso você não esteja se recordando do que é, o mais comum e que certamente você já usou é o `@Override`. 

Com o AA podemos facilitar algumas ações que levariam algum tempo para serem codificadas, como por exemplo declarar 15 elementos em uma view. Ele como o próprio slogam do repositório diz, ele permite que nos concentremos no que realmente importa, simplificando o código e facilitando a manutenção. Vamos ver como ele funciona.


Limpando o código e vendo o funcionamento
=========================================

Com o Android Annotations podemos além de facilitar o desenvolvimento, conseguir dar uma limpada no código também e esta é uma das coisas mais interessantes no annotations. Como já foi dito, nas aplicações Android sempre começamos instanciando os objetos dentro do método `onCreate`

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

Pronto declaramos as variáveis e para utilizá-las basta setar os valores como já é feito atualmente, por exemplo em um TextView chamar a função `setText`. O código fica mais limpo e caso você não queira, não precisa nem de utilizar o método `onCreate`, neste exemplo eu utilizei apenas para declarar o content view e chamar o método `setValuesOfPlayers`. 

Caso você prefira o content view pode ser declarado diretamente no `@EActivity`, que ficaria desta forma

~~~ java
@EActivity(R.layout.activity_main) //declara o content view
public class MainActivity extends AppCompatActivity {

   ...
   
}
~~~

Assim deixamos o código até mais legível e com menos *boilerplate*, facilitando a manutenção deste no futuro.

>Menos é mais... Não importa onde isso seja dito

Implementação
=============

Você já deve estar doido se perguntando como implementar isto em seu projeto, bom agora vamos para esta parte. 

O AA não é nativo no android, por isso precisamos adicionar algumas configurações em nosso build para utilizarmos sem erros de compilação.

Primeiro você deve adicionar a dependencia do `android-apt` ao build do projeto.

~~~ groovy
dependencies {
   classpath 'com.android.tools.build:gradle:2.2.0'
        
    // Verifique a última versão do android-apt no site do desenvolvedor
    classpath 'com.neenbedankt.gradle.plugins:android-apt:1.8'
}
~~~

Agora no build do app iremos criar uma variável para colocar a versão atual do Android Annotations e depois adicionar alguns módulos de dependencia na compilação do mesmo. Dessa forma garantimos que o Android Studio irá interpretar e compilar nosso código com os novos recursos que o annotations proporciona. 

~~~ groovy
apply plugin: 'com.android.application'
apply plugin: 'android-apt' // Aplicamos o plugin do android-apt
def AAVersion = '4.1.0' // Variável com a versão atual do AA

...

dependencies {
    apt "org.androidannotations:androidannotations:$AAVersion"
    compile "org.androidannotations:androidannotations-api:$AAVersion"
    ...
}
~~~

A variável `AAVersion` deixa mais fácil de controlarmos quando houver uma atualização já que utilizamos este número em mais de uma dependencia. Assim quando for necessário trocar de versão basta apenas alterar um lugar em nosso build.

Depois que configuramos nosso build e sincronizamos com o projeto, todas as funções do AA estão disponíveis para uso. Agora é só alegria :D.

Já ia me esquecendo, quando você começa a utilizar o AA, você também deverá trocar o nome das classes quando for chamá-las. Por exemplo, em nosso `AndroidManifest.xml` a classe `MainActivity` era declarada da seguinte forma:

~~~ xml 
<activity
     android:name=".MainActivity"
     android:label="@string/app_name">
</activity>
~~~

Quando estamos utilizando o Android Annotations ele automaticamente gera uma nova classe com o mesmo nome da que programamos, mas com um **underline**( _ ) no final dela. Então deveremos referenciar a classe desta forma: 
 
~~~ xml 
<activity
     android:name=".MainActivity_" //Adicionar um underline ao fim do nome
     android:label="@string/app_name">
</activity>
~~~

Isso também vale para quando queremos iniciar um novo intent ou qualquer outra forma onde formos declarar a classe em nosso código. Um exemplo pode ser este.

~~~ java 
// Iniciando uma activity com uma classe onde o AA é implementado
Intent intent = new Intent(this, MainActivity_.class);
startActivity(intent);
finish();

~~~

Com estas configurações seu projeto está pronto e com o AA implementado, é só utilizar todas as suas funções e novos meios de "programar no android". 

Para saber melhor como ele se comporta e todas suas funcionalidades recomendo que acessem o [site do desenvolvedor](http://androidannotations.org/){:target="_blank"}, lá você poderá encontrar desde exemplos básicos de código até um [cookbook](https://github.com/androidannotations/androidannotations/wiki/Cookbook){:target="_blank"} com muitas dicas legais sobre as implementações do AA.

Bom era isto que eu tinha pra dizer. Estou usando e gostando muito de sua produtividade, agora mãos na massa para ver como ele se comporta em seus projetos ;)).







