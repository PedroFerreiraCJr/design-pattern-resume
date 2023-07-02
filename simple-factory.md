# Simple Factory:
 - O objetivo deste padrão de projeto é separar a lógica de instanciação de um objeto para uma classe 
que contém um método em particular, que geralmente é estático;
 - Algumas pessoas não consideram o design pattern **Simple Factory** como sendo um design pattern, porquê
ele é constituído de apenas um método; e que não tem nenhum código complexo;
 - Este design é comumente confundido com o design pattern **Factory Method**;
 - Tipicamente usamos este design pattern quando nós temos algumas classes que podem ser instanciadas, e
onde precisam ser escolhidas de acordo com determinado critério; onde esta instaciação é baseada em uma 
comparação simples de uma variável.

## Principais papéis:
 - **Client**: ;
 - **SimpleFactory**: Geralmente é uma classe que possui um método estático e que fornece uma instância 
da classe relacionada a **Product** baseado em um parâmetro do próprio método de fábrica; fornece um método 
estático para obter uma instância da classe **Product**;
 - **Product**: Interface ou uma classe abstrata que é instanciada de acordo com um determinado critério;
 - **ProductA**, **ProductB**: Implementação da interface ou classe abstrata que possui a lógica que é 
usada pela classe **Client**.

## Passos de implementação:
 - Para implementar este design pattern basta seguir alguns passos para alcançar este objetivo, 
que basicamente envolve, criar uma classe separada para representar a classe que realiza o papél de factory;
depois, adicionar o método que retorna a instância desejada de acordo com a interface ou classe abstrata
**Product**; este método geralmente é estático e recebe alguns poucos argumentos que devem possibilitar a 
escolha da classe que deve ser devolvida na invocação do método de fábrica; também podem ser fornecidos 
argumentos que possam ser necessários para instanciar a classe desejada.

## Exemplo de implementação:
 - Neste exemplo de implementação, iremos usar classes relacionadas publicação (**Post**);

 ```java
 public class Post {
    private Long id;
    private String title;
    private String content;
    private LocalDateTime createdOn;
    private LocalDateTime publishedOn;

    // getters e setters
 }
 ```

 - Existem algumas subclasses que representam diferentes publicações (**Post**);
 - As principais subclasses são:
  1. **NewsPost**;
  2. **BlogPost**;
  3. **ProductPost**.

 ```java
 public class NewsPost extends Post {
    private String headline;
    private LocalDateTime newsTime;
    
    // getters e setters
 }
 ```

 ```java
 public class BlogPost extends Post {
    private String author;
    private String[] tags;
    
    // getters e setters
 }
 ```

 ```java
 public class ProductPost extends Post {
    private String name;
    private String imageUrl;
    
    // getters e setters
 }
 ```

 - Agora, vamos declarar a classe que em si estabelece o design pattern **Simple Factory**:

 ```java
 public class PostFactory {
    
 }
 ```

 - Para sermos capazes de declarar esta classe como sendo um exemplo deste design pattern, precisam declarar 
um método estático que fornece as funcionalidades de instanciação dos objetos do tipo **Post**; o argumento 
fornecido para o método **createPost** fornece o critério de seleção do tipo específico do "produto" a ser 
devolvido por este método; então baseados neste critério poderemos instanciar e retornar o valor adequado;

```java
 public class PostFactory {
    public static Post createPost(String type) {
        switch(type) {
            case "blog": {
                return new BlogPost();
            }
            case "news": {
                return new NewsPost();
            }
            case "product": {
                return new ProductPost();
            }
            default: {
                throw new IllegalArgumentException("Post type is unkown");
            }
        }
    }
 }
 ```

 - Agora, vamos implementar o cliente que faz uso desta fábrica;

```java
 public class Client {
    public static void main(String[] args) {
        Post post = PostFactory.createPost("blog");

        System.out.println(post);
    }
 }
 ```

## Considerações de implementação:
 - O **Simple Factory** pode ser implementado apenas como um método em uma classe pré-existente; mas 
adicionar uma classe separada permite que outras partes da aplicação usem o **Simple Factory** mais 
facilemtne;
 - **Simple Factory** também pode usar outros design patterns, como por exemplo, o padrão de projeto 
**Builder** para construir os objetos desejados;
 - Se você deseja especializar sua classe **Simple Factory**, então é porque você precisa do design 
pattern **Factory Method**;

## Exemplos do padrão:
 - O Java possui a classe **NumberFormat** no pacote **java.text** que define um método 
chamado: **getInstance**; que é na realidade um **Simple Factory**;

## Comparação de padrões:
 - Comparação do design pattern **Simple Factory** com o **Factory Method**; o design pattern 
**Simple Factory** é apenas o encapsulamento da lógica de instanciação para tornar o código cliente mais
limpo; já o design pattern Factory Method é usado quando se deseja delegar a instanciação de um objeto 
para as subclasses;
 - O design pattern **Simple Factory** deve conhecer todas as implementações de classes que ele pode 
criar; o **Factory Method** não conhece de antemão todas as subclasses;

## Pontos negativos:
 - O critério usado pelo **Simple Factory** pode se tornar complexo com o passar do tempo; e portanto, isto 
pode indicar que pode ser melhor usar o design pattern **Factory Method**.

