---
title: Construindo seu próprio servidor web em Java - Passo 1
description: "Desafio de programação para aprendizado na prática. Minha versão construindo um servidor web próprio em Java."
published: 2024-03-10
tags:
  - Java
draft: false
toc: true
lang: 'pt'
---

> O seguinte post tem origem no desafio <a target="_blank" href="https://codingchallenges.fyi/challenges/challenge-webserver/" alt="Build Your Own Web Server">Coding Challenges</a>. Farei diversas relações com o desafio original.

## O desafio

É proposto a construção de um servidor web mínimo, utilizando um subset da especificação <a target="_blank" href="https://datatracker.ietf.org/doc/html/rfc2616">HTTP/1.1</a>. Assim como o <a target="_blank" href="https://www.w3.org/Protocols/HTTP/AsImplemented.html">HTTP/0.9</a>, vamos apenas aceitar métodos GET.

### HTTP/0.9 vs HTTP/1.1

Existem diversas diferenças entre as duas especificações, mas acredito que a diferençamais visível é que a versão mais antiga não diferencia o que é enviado.
As respostas serão sempre hipertextos.

```
# HTTP/0.9 request
GET localhost:80/test

# HTTP/0.9 response
<html>
  <p>isso é uma resposta html</p>
</html>
```

Enquanto que HTTP/1.1 contém a informação do protocolo utilizado, um código de status e uma mensagem de descrição do código.

```
# HTTP/1.1 request
GET localhost:80/test

# HTTP/1.1 response
HTTP/1.1 200 OK

<html>
  <p>isso é uma resposta html</p>
</html>

```

Outra diferença é que o HTTP/0.9 aceita apenas método GET. A partir da especificação 1.1 é possível utilizar outros verbos para chamadas HTTP. Como disse anteriormente, o desafio é um subset de HTTP/1.1, então só iremos implementar o GET.

## Primeiro passo

Definimos aqui a parte mais básica. Precisamos fazer com que nosso programa crie um socket e fique conectado ao endereço e porta do servidor.

```java
import java.net.ServerSocket;
public class Server {

  public void start(int port) {
    System.out.println("Server is starting on port " + port);
    try (var server = new ServerSocket(port)) { // 1
      var client = server.accept(); // 2
      var out = new PrintWriter(client.getOutputStream(), true); // 3
      var in = new BufferedReader(new InputStreamReader(client.getInputStream())); // 4

      String received = in.readLine(); // 5

      String[] parts = received.split(" "); // 6
      String method = parts[0];
      String path = parts[1];
      String protocol = parts[2];

      out.println(protocol + " 200 OK\r\n\r\nRequested path: " + path + "\r\n"); // 7
      client.close(); // 8
    }
  }

  public static void main(String[] args) {
    var server = new Server();
    server.start(80);
  }
}
```

Para que isso aconteça, é necessário então criar uma nova instância de ServerSocket, criando o tipo específico de socket para processar as conexões dos clientes ao servidor. Isso é feito onde existe o comentário 1. Como estamos em localhost, não é necessário passar o endereço do servidor, só passamos a porta que queremos escutar. Aqui utilizo o padrão try-with-resources, já que ServerSocket é uma classe que implementa AutoClosable e irá executar o método close() ao sair do bloco try.

Dentro do bloco try temos que aguardar por uma conexão do cliente, o que acontece no comentário 2. Lembrando que server.accept() é bloqueante, fazendo com que a thread fique travada aqui até que aconteça alguma conexão.

Os comentários 3 e 4 servem para conseguirmos escrever uma resposta ao cliente e lermos o que o cliente enviou, respectivamente. O comentário 5 faz a leitura de uma linha recebida do cliente.
O que recebemos do cliente é uma linha contendo algumas informações que são divididas no comentário 6 e nas linhas abaixo. Método (GET, POST etc.), caminho após a porta do endereço e o protocolo (HTTP/1.1).

No comentário 7 fazemos o envio de resposta ao cliente, que possui um padrão comum: inicia-se com o protocolo, coloca o código e a descrição do código, quebra de linha, o conteúdo e por fim, quebra de linha novamente.

No comentário 8 fechamos a conexão com o cliente, já que não é uma conexão contínua.

## Conclusão

Com o código atual temos um servidor mínimo capaz de responder requisições sempre enviando um status 200. Não é muito útil, mas ao menos já temos uma base para realizarmos os próximos passos.

Com esse código, podemos ver o que é necessário para um servidor mínimo funcionar:

1. Iniciar um socket em um endereço e uma porta
2. Aceitar uma requisição do cliente
3. Ler o que é enviado do cliente
4. Responder ao cliente com um padrão definido
5. Fechar as conexões de cliente e servidor

Nos outros posts iremos continuar o desafio, incrementando o código atual para ser possível retornar código html ao cliente, lidar com rotas e múltiplas rotas.
