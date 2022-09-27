# Observer:
 - Usando este design pattern é feita a notificação quando o estado de determinado objeto mudar;
 - Os objetos que desejam saber sobre a alteração de estado do objeto observado, são chamados
de observer, e o objeto que mantém o estado observado é chamado de subject (Observable);
 - Este design pattern também é conhecido pelos termos publisher/subscriber ou pub/sub;
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
 - Concrete Subject: classe que implementa a interface Subject, e que mantém o estado que está sendo observado,
assim como, os observadores;
 - Observer: interface que deve ser implementada por observadores com o objetivo de receber notificações
do objeto que implementa a interface Subject (Observable, ou observável);
 - Concrete Observer: classe que implementa a interface Observer com o objetivo receber notificações da
implementação concreta de Subject.

## Passos de implementação:
 - O primeiro passo é definir a interface Observer, que geralmente é uma interface simples que declara
um método que deve ser invocado pela implementação da interface Subject (Observable), ou seja, a
classe concreta que define o estado sendo observado;
 - O segundo passo é criar uma interface para representar o Subject, também conhecido por Observable,
que geralmente envolve os métodos de registro (attach), desregistro (detach), e notificação dos ouvintes
(notifyObservers);
 - Agora, somente será preciso definir as implementações concretas das interface acima. A classe que mantem
a lista de objetos ouvintes e as implementações concretas de ouvintes que desejam receber a alteração de
estado publicada pela classe Subject.

## A implementação de exemplo:
 - Neste exemplo será criado as classes:
    - Order;
    - OrderObserver;
    - PriceObserver;
    - QuantityObserver;
 - Neste exemplo, não será preciso definir uma interface a ser implementada para a classe Observable, ou
seja a interface Subject, pois é um exemplo simplificado;
 - Os métodos attach, detach, recebem como parâmetro uma instância da interface `OrderObserver` que é a
interface dos ouvintes ou observadores de evento;
 - A interface `OrderObserver` declara um método, que servirá para receber a notificação, que define
o parâmetro `Order`, que é a classe Subject que está sendo passada para o objeto Observer ou
listener (ouvinte).

## Considerações de implementação:
 - Em alguns cenários talvez possa acontecer de ocorrer um loop infinito de atualização; por exemplo, digamos
que o observador receba uma notificação sobre uma alteração de estado do observável, e execute alguma ação,
que possa alterar o estado corrente do observável, fazendo com que seja disparado mais uma notificação para o
observador; caso esse cenário não tenha um controle de término desse sequência de atualizações que fazem com
que uma nova notificação seja recebida, faz com que acabe em um loop infinito;
 - Os objetos observadores podem escutar a diferentes observáveis; caso o objeto observador recebe no método
de notificação da alteração de estado uma referência para o objeto que gerou a notificação, então é possível
saber de qual origem veio a notificação;
 - Outro aspecto a se notar, é a performance da aplicação quando há muitos observadores para processar uma
notificação, e que possam levar um tempo considerável para executar uma ação em relação a notifcação
recebida; isso pode causar acumular muitas notificação ou até mesmo perder algumas notificações.

## Considerações de design:
 - Como uma forma de reduzir o número de notificações que são demandadas, é possível segregar os observadores
para diferentes tipos de eventos ou propriedades, fazendo com que, somente os observadores que foram
registrados para determinada propriedade ou evento, sejam notifcadores em caso de alteração no estado em
questão;
 - Tipicamente quem é resposável por enviar a notificação sobre a alteração de estado é a classe Subject; mas
outra maneira enviar a notificação na alteração de estado, é através do código cliente da classe Subject; por
exemplo, quando há uma grande quantidade de alterações de estado, e onde seja requerido que somente uma
notificação seja enviada, então, uma forma de fazer isso é deixando o código que faz a alteração na classe
Subject, responsável por solicitar o envio da notificação de alteração de estado.

## Exemplos do padrão:
 - A biblioteca padrão do Java possui classes e interfaces que representam este design pattern; a interface
java.util.Observer, e a classe java.util.Observable;
 - Outro exemplo deste design pattern, mas na Java EE, são alguns ouvintes de estada da aplicação; como por
exemplo, HttpSessionListener, e ServletRequestListener; então é preciso fazer o registro destes listeners
no contexto da aplicação, para que em determinado momento recebam as notificações sobre a alteração de estado
da aplicação;
 - O Spring também suporta este design pattern através da implementação da interface ApplicationListener.

## Comparação de padrões:
 - O design pattern Observer pode ser comparado com o design pattern Mediator;
 - A diferença do Observer para o Mediator é, o Observer mantém uma comunicação "um-para-muitos", sendo o lado
"um" o Subject (Observable), e o lado "muitos" os Observadores (Observer, que implementam a interface de
notificação da alteração de estado).

## Pontos negativos:
 - A performance do método de notificação dos observadores tem que ser levado em consideração, quando houver
muitos observadores, e caso haja algum observador que leve um tempo considerável para executar a devida ação
com relação a notificação recebida;
