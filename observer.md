# Observer:
 - Usando este design pattern é feita a notificação quando o estado de determinado objeto mudar;
 - Os objetos que querem saber sobre a alteração de estado do objeto observer, são chamados de observer,
e o objeto que mantém o estado observado é chamado de observable;
 - Este design também é conhecido pelos termos publisher/subscriber ou pub/sub;
 - O que é estabelecido por este padrão é uma comunicação one-to-many (um para muitos), mas de uma forma
onde não há o alto acoplamento entre os objetos, pois o relacionamento entre eles é estabelecido através
de interfaces;
 - Os observadores não recebem uma notificação sobre uma propriedade em específico, mas sim, uma genérica.
Com base nisso os observadores podem executar alguma lógica adicional para saber o que exatamente ocorreu;
 - Este padrão é considerado genérico porque ele geralmente não transfere muitas informaçoes na
notificação, pois os observadores podem não estar preocupados com as informações, mas sim, simplesmente
por ter acontecido o evento de alteração;
 - A característica de design genérico, por sem um design pattern, pode ser alterado de acordo com a
necessárida, pois um design pattern é apenas um guideline.

## Principais papéis:
 - Subject: interface para registro dos observadores; essa interface deve ser implementada por uma classe
que mantém o estado a ser observado; contém métodos attach(Observer), detach(Observer), notify();
 - ConcreteSubject: classe que implementa a interface Subject, e que mantém o estado que está sendo observado,
assim como, os observadores;
 - Observer: interface que deve ser implementada por observadores com o objetivo de receber notificações do objeto que implementa a interface Subject (Observable, ou observável);
 - Concrete Observer: classe que implementa a interface Observer com o objetivo receber notificações da
implementação concreta de Subject.

## Passos de implementação:
 - O primeiro passo é definir a interface Observer ou também conhecido por Listener, que geralmente é uma interface simples que declara
um método que deve ser invocado pela implementação da interface Subject (Observable), ou seja, a classe concreta que define o estado sendo observado;
 - O segundo passo é criar um interface para representar o Subject, também conhecido por Observable, que geralmente envolve os métodos de
registro (attach), desregistro (detach), e notificação dos ouvintes (notifyObservers);
 - Agora, somente será preciso definir as implementações concretas das interface acima. A classe que mantem a lista de objetos ouvintes e as implementações concretas de ouvintes.

## A implementação de exemplo:
 - Neste exemplo será criado as classes:
    - Order;
    - OrderObserver;
    - PriceObserver;
    - QuantityObserver;
 - Neste exemplo, não será preciso definir uma interface a ser implementada para a classe Observable, ou
seja a interface Subject, pois é um exemplo simplificado;
 - Os métodos attach, detach, recebem como parâmetro uma instância da interface OrderObserver que é a
interface dos ouvintes ou observadores de evento;
 - A interface OrderObserver declara um método, que servirá para receber a notificação, que define o parâmetro
Order, que é a classe Subject que está sendo passada para o objeto Observer ou listener (ouvinte).

## Comparação de padrões:
 - O design pattern Observer pode ser comparado com o design pattern Mediator;
 - A diferença do Observer para o Mediator é, o Observer mantém uma comunicação "um-para-muitos", sendo o lado
"um" o Subject (Observable), e o lado "muitos" os Observadores (Observer, que implementam a interface de
notificação da alteração de estado).
