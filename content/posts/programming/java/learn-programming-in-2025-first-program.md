---
title: 'Aprenda Programação em 2025 - Primeiro código'
date: 2025-11-01T18:50:58.633Z
description: 'Aprenda a escrever suas primeiras linhas de código em Java'
tags:
  - Java
  - Programming
draft: false
pin: 0
toc: true
lang: 'pt'
---

Antes de realmente escrevermos nosso primeiro programa, é preciso entender algumas coisas.
Sabemos que o computador não entende nada além de bits, então precisamos converter nosso
código para algo que uma máquina entenda.  

Existem dois tipos principais de programas que fazem isso: compilador e interpretador.
A diferença principal entre os dois é que o compilador pega o seu código inteiro e converte (compila)
para a linguagem do seu computador, enquanto o interpretador faz isso linha por linha e executa essa linha
interpretada. Geralmente dizemos que linguagem X é compilada e linguagem Y é interpretada, mas não é bem verdade. Quando falamos isso, é que a ferramenta mais popular daquela linguagem é um compilador ou um interpretador. Um exemplo disso é a linguagem Python que foi criada juntamente com um interpretador, mas que hoje em dia pode ser tanto interpretada quanto compilada.

Ok, agora sabemos que precisamos dessa ferramenta. O que mais precisamos? Bom, precisamos da linguagem em si. Aqui pretendo ensinar a linguagem Java, que é uma linguagem dos anos 90 e já possui décadas de 
experiência e maturidade, sendo usada em basicamente todos os campos possíveis atualmente. É interessante
aprender sobre a história da linguagem, mas não é sobre isso que estarei falando nessas postagens, para isso pode sempre consultar a wikipédia da vida ou algum outro material pela internet.

### Primeiro código

Como quero que o início seja o mais simples possível, vamos utilizar uma ferramenta online para
realizar a compilação do nosso código e executar automaticamente, sem precisarmos instalar nada
em nossos dispositivos. Acesse o [playground](https://dev.java/playground/) e deve aparecer algo
similar à imagem.

![Java playground](/assets/java/java-playground.png "Página java playground")

Apague o código existente apertando o botão `Clear`.

Existe uma tradição no mundo da programação em que nosso primeiro programa em qualquer linguagem deve ser um que imprime a mensagem `Hello, World!` na tela. Para não quebrar a tradição, é isso que faremos também.
Primeiro colocaremos o código e depois explicarei o que faz. 

```java
IO.println("Hello, World!");
```

Aqui temos `IO` que vem de Input/Output, significando que qualquer coisa após o ponto final tem relação com
entrada ou saída de dados. Após o ponto final temos `println` e é um comando que diz para mostrar algo na tela e adicionar uma nova linha no final. Entre aspas temos o nosso texto que queremos que apareça na tela.
Para vermos isso acontecer, aperte o botão `Run`, deve aparecer uma mensagem rápida escrita __Compiling__ e depois apareceça nossa mensagem.

Não é muito, mas você já pode dizer que já programou alguma vez na vida! Já é capaz de colocar uma mensagem na tela em Java.

### Segundo código

Vamos "complicar" as coisas um pouco. Como um computador, seu dispositivo deve ser capaz de computar valores. Vamos imprimir na tela um valor que não colocamos inicialmente.

```java
IO.println(1 + 1);
```

Não estamos dando a resposta para nosso programa, mas pedindo para que realize uma operação de adição
simples e que coloque na tela o resultado dessa operação. No caso desse programa, o valor que deve aparecer na tela é __2__. Aqui você pode testar as operações básicas:

| operação      | símbolo |
| ------------- | ------- |
| adição        |    +    |
| subtração     |    -    |
| multiplicação |    *    |
| divisão       |    /    |

Tente fazer algumas contas, experimente com o que já conhece. Tente quebrar o programa com coisas que sabe 
que não podem ser feita, como por exemplo uma divisão por zero. Faça testes apenas com esse mínimo que 
aprendeu e descubra novas coisas.