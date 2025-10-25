---
title: 'Aprenda Programação em 2025'
published: 2025-09-28T07:16:58.633Z
description: ''
updated: 'Como estudar programação em 2025 com Java - Introdução'
tags:
  - Java
  - Programming
draft: false
pin: 0
toc: true
lang: 'pt'
---
> [!NOTE]
> Se já possuir conhecimento básico de como computadores funcionam, pode pular este tópico

## Como funciona um computador de forma simples

Um computador é uma combinação de componentes feitos
para trabalharem em união para um objetivo em comum.

Pode ser composto de diversos componentes, mas alguns são mais
importantes para um desenvolvedor de software do que outros.

### Unidade Central de Processamento (CPU)
Aqui é onde a magia acontece, onde as operações (na maior parte das vezes) são
realizadas. 

É o componente que recebe dados, realiza operações e devolve os novos dados.
É onde os programas são executados em sua maioria.

Quanto maior a frequência do clock, maior a velocidade em que a CPU
processa os dados. 

É composta de certas unidades, por exemplo:
- [Unidade de controle (CU)](#unidade-de-controle-cu)
- [Unidade aritmética e lógica (ALU)](#unidade-aritmética-e-lógica-alu)
- [Unidade de geração de endereços (AGU)](#unidade-de-geração-de-endereços-agu)
- [Unidade de gerenciamento de memória (MMU)](#unidade-de-gerenciamento-de-memória-mmu)
- [Cache](#cache)
- [Memória de acesso randômico (RAM)](#memória-de-acesso-randômico-ram)
- [Unidade de armazenamento](#unidade-de-armazenamento)
- [Parte lógica](#parte-lógica)
  - [Mas o que é sistema binário?](#mas-o-que-é-sistema-binário)

#### Unidade de controle (CU)
Coordena as outras unidades, definindo quando
cada unidade deve agir e como devem responder às instruções recebidas.

#### Unidade aritmética e lógica (ALU)
Realiza as operações matemáticas de inteiros e as manipulações
de bits.

#### Unidade de geração de endereços (AGU)
Realiza cálculos de endereços de memória (RAM) que serão usados
pela CPU.

#### Unidade de gerenciamento de memória (MMU)
Faz a conversão entre endereços virtuais e endereços físicos.

#### Cache
É um tipo de memória. Possui menor capacidade de armazenamento,
porém é a mais próxima das outras unidades, permitindo que
os processamentos não precisem acessar a memória ram para 
pegar os dados necessários.

Possuem níveis, como L1, L2, L3 etc.

### Memória de acesso randômico (RAM)
Serve para armazenar os dados enquanto o computador está ligado.
É onde os programas ficam quando são carregados, de onde a CPU
pega o que precisa, faz o que precisa fazer e depois envia novamente
para a memória ram.

Possui uma capacidade de armazenar muito mais dados que a CPU,
porém não é tão rápida para ser acessada como os caches.

O nome é acesso randômico porque não existe uma ordem definida
para acessá-la. É possível ir para qualquer endereço definido,
sem precisar passar por outros.

### Unidade de armazenamento
Aqui temos vários tipos, onde os mais comuns são:
- Unidade de disco rígido (HDD), também chamado de HD
- Unidade de estado sólido (SSD)

Ambos possuem o mesmo propósito, só mudam como
atingem esse objetivo, armazenar dados por longos períodos,
mesmo se o computador for desligado.

Possuem uma capacidade muito maior de armazenamento que RAM,
porém o acesso (tanto leitura quanto escrita) é muito mais lento.

Um programa então é carregado do HD/SSD, vai para a RAM e para a CPU,
e a partir daí depende do que o programa faz.

### Parte lógica

Aqui quero tratar de um tópico que está em ambos os lados, software e hardware.

Antes de tudo, é necessário entender que computadores sabem 
apenas uma única linguagem real, a binária. Para o hardware, é o sinal
elétrico ligado ou desligado. Para o software, dois valores, 0 ou 1.

#### Mas o que é sistema binário?

É um sistema numérico que determina a quantidade de símbolos únicos para a representação
de números. O sistema mais comum que temos é o sistema decimal, com 10 símbolos únicos (de 0 a 9).
Após o último símbolo único, passamos a repetir os símbolos conhecidos para formar outros números.

O binário é o mais utilizado em computadores, mas também podemos falar de um outro sistema muito
conhecido, o hexadecimal. Ele possui símbolos de 0 a 9, de A ao F, sendo A equivalente ao 10 decimal
e F equivalente ao 15 decimal. Este sistema é utilizado por representar valores binários grandes 
com menos símbolos, onde 1111b = F.

A partir desse sistema binário, conseguimos criar sequências de sinais
e atribuir significados para essas sequẽncias. Atualmente agrupamos 8
sinais, chamados de byte.

Um sistema que atribui significados para os bytes é chamado de ASCII,
Código Padrão Americano para o Intercâmbio de Informação. Possui 128 sinais
com diferentes categorias.

Alguns exemplos:

| binário   | representação visual |
| --------- | -------------------- |
| 0011 0000 | 0                    |
| 0011 0001 | 1                    |
| 0100 0001 | A                    |

Além disso, podemos também fazer conversões entre sistemas. Os mais comuns
são decimal e hexadecimal.

Vamos fazer a conversão de binário para decimal.
0000 0010 é igual a 2 em decimal. Para cada dígito, fazemos assim:

$$
f(i) = 2^i
$$

onde **i** é o índice/posição do dígito começando da direita para a esquerda, em zero.

| binário | índice | valor quando é 1  |
| ------- | ------ | ----------------- |
| 0       | 0      | 2<sup>0</sup> = 1 |
| 1       | 1      | 2<sup>1</sup> = 2 |
| 0       | 2      | 2<sup>2</sup> = 4 |
| 0       | 3      | 2<sup>3</sup> = 8 |

aqui temos então que com 4 dígitos em binário, podemos representar no máximo até o valor 15, que é a soma dos 4 dígitos se forem valor 1.

Para converter o número 1010: Sabemos que temos "ativado" o a posição 3 e a posição 1, então basta somar seus valores, 8 + 2 = 10.

Agora um número maior, que é utilizado para representar **A** em ASCII:

| binário | índice | valor |
| ------- | ------ | ----- |
|    0    |    7   |   0   |
|    1    |    6   |  64   |
|    0    |    5   |   0   |
|    0    |    4   |   0   |
|    0    |    3   |   0   |
|    0    |    2   |   0   |
|    0    |    1   |   0   |
|    1    |    0   |   1   |

0100 0001 -> 65 (A)

Algo que pode notar é que sempre será um número ímpar se o dígito no índice 0 for 1.

De forma bem superficial, a CPU entende que certos padrões binários representam comandos, e esses comandos
devem ser processados para então realizar determinada tarefa. É por meio de programação podemos definir tarefas
que serão convertidas (compiladas) para os comandos que a máquina já conhece e então executadas. Existem linguagens
que precisam de mais passos até chegar nessa versão compreensível pela máquina e outras linguagens que já estão, 
de certa forma, mais próximas dos comandos reais.