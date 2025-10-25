---
title: Mudanças do Selenium 4
published: 2021-11-22
description: "Mudanças importantes que a versão 4 do Selenium trouxe."
tags:
  - Java
  - Selenium
draft: false
toc: true
lang: 'pt'
---

## Lista de mudanças

Sem enrolação, aqui está a lista de mudanças que falarei no decorrer do post.

- [Screenshot através do elemento](#screenshot-através-do-elemento)
- [Localizadores Relativos](#localizadores-relativos)
- [Remoção de métodos utilitários de busca](#remoção-de-métodos-utilitários-de-busca)
- [Alteração das classes utilizadas para Timeout](#alteração-das-classes-utilizadas-para-timeout)

#### Screenshot através do elemento

Logo na versão `v4.0.0.0-alpha-1` foi incluído a capacidade de tirar screenshot por meio de um WebElement, utilizando a interface TakesScreenshot que a interface de WebElement passou a estender.

Para utilizar o comando, basta chamar o seu WebElement com o método

```java
element.getScreenshotAs(outputType);
```

que exige um argumento do tipo `OutputType<X>`, o qual é uma interface onde `X` indica o tipo de retorno da implementação.
Possui as implementações para: `BASE64` com retorno de `String`, `BYTES` com retorno de `byte[]` e `FILE` com retorno de `File`.

---

**_OBS.:_**
Caso use `OutputType.FILE`, saiba que o arquivo é temporário, e será apagado assim que a JVM encerrar. No Windows, o arquivo se encontra em _`C:\Users\seuUsuario\AppData\Local\Temp\`_.

---

#### Localizadores Relativos

Além das formas tradicionais de localizar um elemento na página, agora é possível utilizar localizadores relativos, onde encontra elementos próximos de outros.

Os métodos disponíveis são: `above`, `below`, `toLeftOf`, `toRightOf` e `near`.

Para utilizar, deve ser utilizado o método estático `RelativeLocator.with(By by)` que retorna uma classe que estende `By`. É essa classe (`RelativeLocator.RelativeBy`) que possui os métodos citados acima. Como é uma estensão de `By`, os métodos utilizados para encontrar elementos podem ser utilizados da mesma forma antes da adição.

Um exemplo utilizando o método `below` em uma busca no Google.

```java
By searchButtonSelector = By.cssSelector("input[type='submit']");
WebElement searchField = driver.findElement(By.name("q"));
searchField.sendKeys("Selenium 4");
WebElement searchButton = driver.findElement(
                                    with(searchButtonSelector)
                                    .below(searchField));

searchButton.click();
```

#### Remoção de métodos utilitários de busca

Antes da versão 4 do Selenium, você podia selecionar um método específico para realizar a busca de um elemento de acordo com a forma desejada.
Exemplo: `findElementByClassName`, `findElementById`, `findElementByXpath` etc.

Na versão mais recente, tais métodos foram removidos, e é necessário utilizar `findElement(By by)`, onde `by` identificará a forma desejada para a busca.
A mudança também se aplica para os métodos `findElementsBy*`

#### Alteração das classes utilizadas para Timeout

Tanto métodos quanto classes utilizadas para manipulação de Timeout alteraram suas assinaturas para aceitar apenas a classe `Duration` para definir o tempo de timeout, ao invés de utilizar um número junto com um enum de `TimeUnit`.
