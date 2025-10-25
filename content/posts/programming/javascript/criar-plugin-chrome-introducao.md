---
title: Criação de plugin para Google Chrome - Uma introdução
description: "Crie seu primeiro plugin agora mesmo!"
published: 2022-04-04
tags:
  - JavaScript
draft: false
toc: true
lang: 'pt'
---
## Introdução
Ao criar um plugin (extensão) para navegadores baseados em Chromium, é necessário entender que são como páginas web rodando localmente no navegador em que está instalado. Rodam em um ambiente separado, mas com capacidade de interagirem com o navegador, com abas (sites) abertos e até mesmo com outros plugins instalados.

As mesmas tecnologias usadas para criação de um site são empregadas ao criar um plugin, sendo o mínimo necessário apenas Javascript. Para uma melhor apresentação e maior interação, HTML e CSS são utilizados.

É possível realizar leitura do conteúdo de uma determinada página, salvar dados locais e até mesmo compartilhados entre outros navegadores em que você está logado.

No nosso exemplo vamos criar um plugin para inverter as cores de uma página qualquer.

### O que é necessário?
O arquivo mais importante para começar seu plugin é o arquivo `manifest.json`, o qual guarda informações importantes sobre o projeto, como nome, versão, arquivo de execução principal, permissões etc.

#### Arquivo manifesto
Como dito antes, é o arquivo mais importante. Nele você vai especificar alguns dados relacionados ao seu plugin.
Os 3 dados necessários são: name, manifest_version e version.
```json
{
    "name": "Nome da extensão",
    "manifest_version": 3,
    "version": "0.0.1"
}
```
O detalhe importante aqui é a versão do manifesto. Existe a versão 2 e versão 3. Estaremos utilizando a versão 3. Futuramente pretendo explicar um pouco a diferença entre as versões.

Um arquivo json com esses dados já são um plugin válido que já pode ser colocado no Chrome.  Para testar, entre em `chrome://extensions`, ative o modo de desenvolvedor e clique no botão Carregar sem compactação. Após isso, deve existir um plugin na página com o nome que colocou e a versão.
Obviamente esse plugin não faz nada, mas logo veremos como dar vida a isso.

##### Background
A próxima chave que vamos conhecer é a `background` que abriga o conjunto chave/valor a seguir:
```json
{
    "name": "Nome da extensão",
    "manifest_version": 3,
    "version": "0.0.1",
    "background": {
        "service_worker": "background.js"
    }
}
```
Definimos então nosso primeiro arquivo javascript que é a base para o plugin.  O nome do arquivo do nosso <a href="https://developer.mozilla.org/pt-BR/docs/Web/API/Service_Worker_API" target="_blank">service worker</a> é colocado aqui. Com isso podemos criar um arquivo com o mesmo nome no diretório atual.

Para ver a execução, coloce um
```js
console.log('Hello Plugin')
```
no arquivo do service worker. Para visualizar o console, volte à página de extensões e clique no ícone de atualizar para o plugin carregar as novas informações. Após isso, deve aparecer um link escrito "service worker". Clique nesse link e será aberto o Chrome Dev Tools do plugin.
No Chrome Dev Tools, clique na aba do Console e lá deve encontrar a mensagem que deixou no arquivo do service worker.

##### Permissões
As permissões dão a possibilidade de adicionarmos funcionalidades que não seriam possíveis sem elas, como injeção de scripts, armazenar informações etc.

Por exemplo, para que seja possível usarmos as funções de guardar dados, é necessário adicionar a permissão `storage`.
Para isso, incluímos uma chave `permissions` em nosso manifesto que recebe uma lista de strings.
```json
{
    "name": "Nome da extensão",
    "manifest_version": 3,
    "version": "0.0.1",
    "background": {
        "service_worker": "background.js"
    },
    "permissions": ["storage"]
}
```

Com a permissão de storage, podemos utilizar duas funções dentro do arquivo background.js: set e get.
Eles funcionam da seguinte forma:
```js
// Assim salvamos uma chave key com um valor qualquer
// O callback é chamado após o armazenamento, sendo então dispensável.
// a propriedade storage só estará disponível se a permissão falada anteriormente tiver sido colocada.
chrome.storage.local.set({key: value}, callback) // pode ser local ou sync

// A forma de recuperar a chave é parecida, utilizamos a função get(),
// onde o primeiro parâmetro é uma lista de strings com as chaves que deseja pegar.
// o segundo parâmetro (opcional) é uma função que tem um objeto com o resultado.
chrome.storage.local.get(['key'], ({key}) => {}) // também pode ser local ou sync.
```

Existe uma versão com retorno `Promise` tanto para set() como para get(), basta remover o callback.

##### Action
A action permite realizar configurações e operações relacionadas ao plugin na barra de ferramentas (barra onde ficam os plugins, ao lado da barra de endereço). É possível adicionar título que aparece ao passar o mouse por cima do plugin, adicionar ação de popup (criado com tecnologias web), definir o ícone, colocar texto por cima do ícone (badge) etc.

Para começar, adicionamos uma nova chave no arquivo manifesto, a chave `action`. Essa chave é de um objeto que aceita diversas chaves, como `default_icon`, `default_title`, `default_popup` etc.
```json
{
    "name": "Nome da extensão",
    "manifest_version": 3,
    "version": "0.0.1",
    "background": {
        "service_worker": "background.js"
    },
    "permissions": ["storage"],
    "action": {
        "default_title": "Meu título que aparece no hover",
        "default_popup": "popup.html"
    }
}
```
Em `default_popup` deve ser passado o endereço e nome do arquivo HTML que será aberto ao clicarmos na extensão.

Caso instale o plugin dessa forma, sem criar o popup.html, e clicar no plugin, verá uma página de erro informando que não conseguiu encontrar o arquivo. Para resolver isso, basta criar o arquivo no endereço indicado.

## Exemplo
Nossa extensão servirá para inverter as cores de uma página.

Não usaremos o arquivo de background.js nesse projeto.

Teremos um plugin que abre um popup contendo um check button para ativar/desativar a inversão de cores.
Assim usaremos de tudo que vimos até agora.

### Manifesto
Nosso manifesto será:

manifest.json
```json
{
    "name": "Inverte cores extension",
    "manifest_version": 3,
    "version": "0.0.1",
    "permissions": ["storage", "scripting"],
    "action": {
        "default_title": "Clique aqui para abrir",
        "default_popup": "popup.html"
    },
    "host_permissions": ["https://*/*"]
}
```
Aqui temos algumas mudanças do que vimos antes, trocamos o texto de `name` e `default_title`, adicionamos uma nova permissão (scripting), além de incluírmos o `host_permissions` com um valor que permite o plugin ser executado em qualquer site. Removemos o `background`.

Lembre-se de criar os arquivos do service worker e do popup.


### Arquivo do popup
Adicionamos um checkbox para saber se o efeito deve estar ativado ou não na página.

popup.html
```html
<!DOCTYPE html>
<html>
<body>
    <div style="width: 100px;">
        <input type="checkbox" id="activate" /> Inverter cor
    </div>
    <script src="popup.js"></script>
</body>
</html>
```

Além do checkbox, temos também o `popup.js` que será utilizado para informar quando o status da checkbox mudar.

Toda vez que o popup é aberto, esse arquivo será executado novamente.

popup.js
```js
// Encontra o checkbox que está no HTML
const checkbox = document.getElementById('activate')

// Função usada dentro do listener que veremos a seguir.
async function listener() {
    const currentTab = await getCurrentTab()

    // Salva o estado atual do checkbox com base na aba,
    // possibilitando sabermos o estado para cada aba.
    // Além disso, armazenamos em invert o estado atual,
    // facilitando a alteração do estado local futuramente.
    await chrome.storage.local.set({
        [currentTab.id]: checkbox.checked,
        invert: checkbox.checked
    })
    
    // Executa o script que aplica o filtro ou não depenpendo do estado.
    chrome.scripting.executeScript({
        target: {tabId: currentTab.id },
        files: ['activate.js']
    })
}

// Ao passarmos null como argumento, informamos que queremos tudo que está armazenado.
chrome.storage.local.get(null, async (data) => {
    // adicionamos uma função de listener quando ocorrer o evento change.
    checkbox.addEventListener('change', listener, false)

    const currentTab = await getCurrentTab()

    // altera o valor de checked caso o estado já tenha sido salvo antes para essa aba.
    if (data[currentTab.id]) {
        checkbox.checked = data[currentTab.id]
    }
})

// Removemos o evento quando o popup é fechado.
window.onclose = () => {
    checkbox.removeEventListener('change', listener, false)
}

// É feito uma busca nas queries com base nas opções active e currentWindow,
// assim pegamos a aba que estamos executando o popup.
async function getCurrentTab() {
    let queryOptions = { active: true, currentWindow: true };
    let [tab] = await chrome.tabs.query(queryOptions);
    return tab;
}
```


### Arquivo de scripting
Este arquivo é executado após a chamada de scripting que ocorre no arquivo de popup.js, dentro do listener.

Quando o arquivo é executado, já existem alguns valores salvos, e queremos verificar o que está em invert, caso invert seja verdadeiro, aplicamos o filtro, caso não seja verdadeiro, removemos o filtro.
```js
chrome.storage.local.get(['invert'], async ({invert}) => {
    const html = document.getElementsByTagName('html')[0]
    if (invert) {
        html.style.filter = 'invert(100%)'
    } else {
        html.style.filter = ''
    }
})
```

## Conclusão
Criamos um plugin bem simples, mas completo em questões de usabilidade. Possui ações para o plugin, utiliza armazenamento local, além de utilização de execução de scripts.
