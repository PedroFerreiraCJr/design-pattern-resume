# Factory Method:
 - O objetivo deste design pattern é separar a lógica de instanciação do código que pode estar separa em 
diversas partes do código para um classe em particular;
 - Este design pattern pode se parecer similar ao **Simple Factory**, mas por outro lado, a principal 
diferença é que neste design, não sabemos de antemão quais classes podem ser instanciadas; também permite 
adicionar novas classes ao sistema e lidar com a criação delas sem afetar o código cliente; e isto é 
alcançado delegando a instanciação para subclasses;
 - A subclasse da classe principal, ou **Creator** é quem define qual objeto produto concreto será
instanciado.

## Principais papéis:
 - **Product**: classe base ou interface que deve ser criada;
 - **ConcreteProductA**: classe que é uma implementação concreta da interface ou classe abstrata **Product**;
 - **Creator**: declara um factory method abstrato que deve ser implementado por subclasses para devolver
o objeto a instancia correta de acordo com a subclasse de **Creator**;
 - **ConcreteCreatorA**: classe que implementa ou estende a classe base que contem o método de fábrica
que deve ser realizado; portanto, implementa o factory method e devolve a instancia de acordo com a subclasse
utilizada.

## Passos de implementação:
 - Começamos criando a classe para o **Creator**; esta classe pode implementar o factory method quando ela 
puder devolver uma instancia padrão para o objeto **Product**;
- As implementações/classes derivadas irão implementar o factory method para retornar o valor adequado de 
acordo com a subclasse;

## A implementação de exemplo:
 - A classe **Message** será a classe **Product**; podendo ser uma interface ou uma classe abstrata;
 - As subclasses utilizadas neste exemplo são:
  1. TextMessage;
  2. JsonMessage;

 - Estas classes derivadas somente alternam a forma de armazenar o conteúdo da mensagem;
 - A classe **MessageCreator** é uma classe abstrata que fornece o **factory method** que deve ser 
implementado para devolver a classe **Product** adequada (neste caso, uma subclasse de **Message**);
 - As subclasse de **MessageCreator** são duas:
  1. TextMessageCreator;
  2. JsonMessageCreator;

 - Estas classes realizam a implementação do método abstrato da classe **MessageCreator**, que devem retornar
p objeto adequado de acordo com a subsclasse instanciada.

```java
/**
 * Esta classe representa a interface para 'Product' que é a
 * mensagem. Implementações irão especificar o tipo do contúdo.
*/
public abstract class Message {
    public abstract String getContent();

    public void addDefaultHeaders() {

    }

    public void encrypt() {

    }
}
```

 -Agora, as implementações desta classe:
 
```java
public class JsonMessage extends Message {
    @Override
    public String getContent() {
        return "{\"json\": []}";
    }
}
```

```java
public class TextMessage extends Message {
    @Override
    public String getContent() {
        return "Text";
    }
}
```

 - A classe abaixo é a classe que fornece o **factory method** que deve ser implementado por cada classe 
que representa uma subclasse de **Creator**;


```java
public abstract class MessageCreator {
    public Message getMessage() {
        Message message = createMessage();
        message.addDefaultHeaders();
        message.encrypt();

        return message;
    }

    /**
     * Este é o factory method que deve ser realizado pelas subclasses
     * e que permite devolver determinada instância de 'Product', que 
     * neste caso, é a classe Message.
    */
    public abstract Message createMessage();
}
```

 - Agora, vamos para as classes concretas do **Creator**;

```java
public class JsonMessageCreator extends MessageCreator {
    @Override
    public Message createMessage() {
        return new JsonMessage();
    }
}
```

```java
public class TextMessageCreator extends MessageCreator {
    @Override
    public Message createMessage() {
        return new TextMessage();
    }
}
```

 - Com as subclasses definidas, vamos partir para a classe **Client**;

```java
public class Client {    
    public static void main(String[] args) {
        printMessage(new JsonMessageCreator());
        printMessage(new TextMessageCreator());
    }

    private static void printMessage(MessageCreator creator) {
        Message message = creator.getMessage();
        System.out.println(message);
    }
}
```

## Considerações de implementação:
 - A classe **Creator** pode ser uma classe concreta, se ela puder fornecer uma instância no 
factory method definido nela;
 - É pissível usar o modo de recebimento de argumentos do Simple Factory para ter algum critério de uso
para instanciar o objeto concreto do tipo "product";
 - O design pattern Template Method, frequentemente faz uso deste design patter; assim como outro design
pattern, o **Abstract Factory** também pode fazer uso deste padrão.

## Exemplos do padrão:
 - A interface **java.util.Collection** (AbstractCollection) possui um método, factory method, para
retornar um Iterator<E> de acordo com a subclasse que implementa esta interface, como por exemplo, 
ArrayList, LinkedList;
 - A principal característica do design pattern **Factory Method** é: uma subclasse fornecendo a instancia
concreta da parte que faz o papél do 'product'; exemplos que usam método estáticos para construir um objeto
não são exemplos do design pattern **Factory Method**.

## Pontos negativos:
 - Mais complexo de implementar, porque envolve a criação de mais classes, e torna que será preciso testar 
unitáriamente mais delas;
 - É preciso utilizar este design pattern deste cedo no projeto, porque senão fica dificil criar a hierarquia 
de classes; não é fácil refatorar o código existente para usar este design;
 - Muitas vezes este design pattern força criar uma subclasse somente para criar uma instância adequada.





