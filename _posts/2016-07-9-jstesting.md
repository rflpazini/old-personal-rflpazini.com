---
layout: post
title: Testes com JavaScript
author: Rafael Pazini
comments: true
---

![Testing JS](/assets/img/posts/jstesting.jpg)

Antes de começarmos a falar sobre os testes, irei fazer uma pergunta que certamente você já ouviu muitas vezes: **Você implementa testes?** 

Caso a resposta seja não, vamos tentar consertá-la e torná-la em um sim. <!--more--> Quando falamos de testes e ainda não utilizamos ou apenas só ouvimos falar sobre eles, ficamos com várias dúvidas de como implementar, o que usar, o que não usar, então vamos tentar clarear um pouco estes pensamentos e fazer de uma forma simples e eficiente.

O que são testes
================


Testes são um conjunto de tarefas que são executadas para verificar se um método está fazendo o que ele deveria fazer. Ou seja, se ele está retornando os valores que deveria retornar, se está adicionando objetos onde deveria e assim por diante. 

Escrever testes também ajuda a criar códigos mais eficientes, desta forma conseguimos assegurar que mesmo quando forem feitas novas implementações não será quebrado algo que já funciona.

Começando a implementação
=========================


Escrever testes manualmente pode ser um pouco estressante e para isso existem frameworks que nos ajudam a facilitar esta tarefa. No caso irei falar um pouco sobre o Jasmine, que é um framework muito utilizado no meio web e é muito fácil de utilizá-lo em qualquer projeto.

### Framework de teste *Jasmine* ###


O [Jasmine](http://jasmine.github.io/){:target="_blank"} é um framework que implementa o método BDD *(Behavior Driven Development)* e mesmo que você nunca tenha implementado um teste na vida, ele proporciona um jeito amigável de se trabalhar e escrever os testes, você escreve o que deveria ocorrer ou espera que ocorra quando o teste for executado. Vamos a um exemplo: Vamos supor que iremos criar um teste para verificar se o método `soma` está realmente executando a soma correta de dois números, o teste ficaria mais ou menos assim...

~~~ js
describe('Calcula', function() {

    it('deve somar DOIS números', function() {
    	var calcula = new Calcula(),
    	   a = 2,
    	   b = 6;

        expect(calcula.soma(a, b)).toEqual(a+b);
    });
});
~~~

E como eu disse que ela é fácil de se trabalhar para quem nunca mexeu com testes, vou falar um pouco da versão [stand alone](https://github.com/jasmine/jasmine/releases){:target="_blank"}, que é a que está utilizando como base para este artigo. Nesta versão você executa os testes através de um documento HTML e ali mesmo observa se eles estão falhando ou não. Basta adicionar os arquivos `.js` no Html.

~~~ html
  <link rel="shortcut icon" type="image/png" href="lib/jasmine-2.4.1/jasmine_favicon.png">
  <link rel="stylesheet" href="lib/jasmine-2.4.1/jasmine.css">

  <script src="lib/jasmine-2.4.1/jasmine.js"></script>
  <script src="lib/jasmine-2.4.1/jasmine-html.js"></script>
  <script src="lib/jasmine-2.4.1/boot.js"></script>

  <!-- include source files here... -->
  <script src="src/Calcula.js"></script>

  <!-- include spec files here... -->
  <script src="spec/CalculaSpec.js"></script>
~~~

Depois é só executá-lo no browser e pronto, você verá a seguinte tela que faz os testes no Jasmine e se existir algum teste como neste, ele já é executado.

![Jasmine testing](/assets/img/posts/jasmine_testing_screen.jpg)

Como todo bom desenvolvedor que está aprendendo sobre alguma tecnologia, indico a leitura da [documentação do Jasmine](http://jasmine.github.io/2.4/introduction.html){:target="_blank"}. Lá você vai encontrar alguns exemplos e dicas de como utilizar os testes, e até mesmo outras formas mais complexas de utilizar o framework e conseguir integrá-lo a seu ambiente de desenvolvimento atual.

>Teste de software é o processo de executar o software de uma maneira controlada com o objetivo de avaliar se o mesmo se comporta conforme o especificado.

### Clico de testes *Red, green, refactor*###

Quando vamos começar a implementar testes, é interessante saber que existem padrões de se fazer isto. É o que este ciclo irá no mostrar. Ele basicamente é separado em três etapas: 

* Red *(vermelho)* - o teste que escrevemos obrigatoriamente irá falhar;
* Green *(verde)* - o teste é aprovado;
* Refactor *(relatora)* - podemos refatorar/limpar o código sem medo.




### Red ###

Primeiro escrevemos nosso teste, vamos continuar no exemplo do método soma. Ele irá falhar, pois ainda não existe um método soma para que o mesmo passe no teste.

Então para escrever este teste vamos pensar que o seguinte - Estamos desenvolvendo uma Calculadora, onde teremos uma classe chamada `Calculadora.js` e que haverá um método que soma dois números. Portanto...

* O método `soma` deverá somar números;
* Conseguir somar números flutuantes *(0.3 + 0.4)*
* Retornar o valor da soma dos números;

Seguindo esta base de raciocínio, nossa classe de teste ficará assim:


~~~ js
describe('Calculadora', function() {
    var calculadora,
    	a,
    	b;
    
    //Inicia as variáveis antes de executar qualquer rotina de teste
    beforeEach(function() {
    	calculadora = new Calculadora();
    	a = 5;
    	b = 6;
    });

    //Teste que verificará se nosso método está retornando a soma correta
    it('deve somar DOIS números', function() {
        expect(calculadora.soma(a, b)).toEqual(a + b);
    });

    //Teste de soma de números flutuantes
    it('deve somos DOIS números FLUTUANTES', function() {
    	expect(calculadora.soma(0.1, 0.2)).toEqual(0.3);
    }) 
});
~~~

Quando rodarmos este teste o mesmo irá falhar e é isto que queremos que aconteça. Hora de escrever a classe para implementar o método soma.

### Green ###

Sinal verde para que o teste seja executado com sucesso, então vamos escrever a classe.

Como eu havia dito nossa classe é a `Calculadora.js`, para que os testes fiquem verdes, ela deverá receber números e também conseguir somar números decimais. Nossa classe ficará mais ou menos assim.


~~~ js
class Calculadora {
    soma(a, b) {
        let result = a + b;

        // Verifica se o resultado da soma convertido em inteiro não é igual ao resultado
        // se isso for verdade, convertemos o número para float e limitamos o mesmo
        // para apenas duas casas depois da vírgula
        if (parseInt(result) != result) {
            result = parseFloat(result.toFixed(2));
        }

        return result;
    }
}
~~~

No código existe uma comparação para saber se o número que estamos procurando era um número quebrado ou não. Se ele for um número flutuante, o mesmo é convertido para float e também é limitado o número de casas decimais para 2, que é o que uma calculadora normal faz. Sendo assim, nossos dois testes ficam verdes. O que garante que nosso código está atendendo as expectativas.

### Refactor ###

A parte de refatorar o código é uma das mais complexas, pois sem querer podemos quebrar alguma coisa que já funciona. Mas como temos nossos testes implementados, eles irão assegurar de que nada será quebrado quando adicionarmos novas *features* ou formos corrigir algo no código, caso elas quebrem os testes irão falhar e então saberemos o que quebrou.

No momento se passarmos duas Strings como parâmetros `"2"+"3"` ele ainda irá aceitar e concatenar as Strings, retornando `23` como resultado da soma. E claro que está incorreto. 

Então para que isto não seja permitido, basta adicionarmos uma feature que retorna um erro quando tentamos usar Strings como parâmetros do método soma. Desta forma adicionaremos um teste que simula a entrada de uma String e que verifica se o erro está sendo retornado, nosso teste será mais ou menos assim

~~~ js
describe('Calculadora', function() {
	
   ...
    
    // Teste responsável pela verificação do erro quando 
    // existe Strings como parâmetros
    it('deve gerar um ERRO ao receber uma String como parâmetro', function() {
    	expect(function() {
    		calculadora.soma(2, 'teste')
    	}).toThrowError(Error);
    });
});
~~~

E agora que temos um teste para simular a entrada de Strings, é hora de implementar nosso código com a comparação que verificará se os números são realmente números. Para isso utilizaremos a função `typeof` para verificar o tipo da variável que iremos calcular.


~~~ js
class Calculadora {
    soma(a, b) {
        let result;

        // Verifica se os tipos dos arguentos que recebemos
        // são do tipo 'number'. Caso não forem, iremos retornar um erro
        if (typeof a != 'number' || typeof b != 'number') {
            throw new Error("Os valores devem ser apenas números");
        }

        result = a + b;

        // Verifica se o resultado da soma convertido em inteiro não é igual ao resultado
        // se isso for verdade, convertemos o número para float e limitamos o mesmo
        // para apenas duas casas depois da vírgula
        if (parseInt(result) != result) {
            result = parseFloat(result.toFixed(2));
        }

        return result;
    }
}
~~~

Sendo assim criamos uma nova implementação e garantimos que a mesma está funcionando com seu devido teste. Se rodarmos novamente os testes, todos estarão no estado verde.

Como podemos perceber, a implementação de testes é algo que não é complicado e nos ajuda muito durante o desenvolvimento das aplicações. Caso você queria ver o código final da implementação de exemplo, ele estará disponível no [github](https://github.com/rflpazini/jstesting){:target="_blank"}. Espero que possa ter te ajudar um pouco com esta explicação, e qualquer dúvida é só deixar um comentário.

