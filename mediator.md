# Mediator:
 - Este design pattern tem por objetivo eliminar a complexidade na comunicação/colaboração entre um conjunto
de objetos com outros; quando houver a necessidade de notificar um conjunto de objetos quanto a alteração de
estado em um objeto em particular, este design pattern poderá ser usado; o conjunto de objetos que recebem a
notificação podem tomar alguma ação com relação ao novo valor de estado, ou com relação a uma propriedade em
particular que foi alterada;
 - Tipicamente quando há a necessidade de um objeto se comunicar com outro, há um forte acoplamento entre
estes objetos, porque o objeto que deseja se comunicar através de uma invocação de método em outro objeto,
deve manter uma referência para este outro objeto em questão; mas este design pattern tem por objetivo
mitigar esse acoplamento, fazendo com que o objeto que deseja se comunicar, tenha somente uma referência
para o objeto mediator, o que torna a interligação entre objetos minima, pois o objeto que deseja invocar um
método somente tem uma referência para o objeto mediator;
 - Neste grupo de objetos, quando há uma alteração de estado e, que é necessário notificar outro grupo de
objetos, o grupo onde houve a alteração de estado notifica somente o mediator que, por sua vez, notifica os
demais objetos do grupo que devem receber esta notificação;
 - Uma vantagem deste arranjo de objetos é, quando houver a necessidade de remover algum objeto de um grupo
que é mantido pelo mediator; dessa forma, somente o mediator precisará ser alterado com a remoção de um
objeto do grupo;
 - De maneira semelhante, se houver a necessidade de adição de outro objeto ao grupo de colaboração, somente
o mediator precisará ser alterado com a adição do novo tipo de objeto.

## Principais papéis:
 - Mediator: interface/classe abstrata/classe concreta que representa a API disponível para os integrantes
do grupo de colaboração e, que podem ser invocados para notificar os demais "colegas" do grupo de
colaboração; por exemplo, o método `public void colleagueChanged(Colleague)` serviria para notificar os
demais "colegas" do grupo de comunicação/colaboração sobre uma alteração de estado;
 - Concrete Mediator: caso o tipo Mediator seja uma interface ou classe abstrata, uma classe concreta serviria
para realizar as operações que foram definidas na API da interface/superclasse; outro aspecto desta classe é
que deve manter uma referência para os demais "colegas" de colaboração do grupo; com uma referência para os
"colegas" de grupo, esta classe poderia notificá-los;
- Colleague: classe que participa do conjunto/grupo de objetos que podem receber uma notificação sobre uma
alteração de estado em outros objetos "colegas"; estes objetos mantém uma referência para o Mediator para que
este possa receber uma invocação quando houver a necessidade de notificar os demais "colegas" do grupo em
questão; outro aspecto a se notar é, que o Mediator é fortemente acoplado com os Concretes Colleagues - caso
precisem ser usados como classes derivadas de Colleague, porque o Mediator poderá ter que saber invocar um
método em específico de cada Concrete Colleague.

## Passos de implementação:
 - O primeiro passo é desenvolver a classe Mediator; esta classe deve conter um método genérico que poderá ser
usado por um dos objetos do grupo para notificar os demais sobre uma alteração de estado; este método precisa
saber em qual objeto do conjunto houve a alteração e, em qual propriedade do objeto ocorreu a alteração de
estado; a classe Mediator pode ser desenvolvida como sendo uma interface/classe abstrata ou uma classe concreta
caso não haja a necessidade de derivação no futuro; neste método genérico, deve ser feita a notificação dos
demais objetos do grupo de colaboração; portanto, este método deve notificar os demais objetos, menos o objeto
onde ocorreu a alteração de estado e, assim como o objeto que houve a alteração, deve receber o valor que foi
alterado; outra solução comumente usada é, possibilitar aos objetos que recebem a notificação perguntarem ao
objeto recebido no método qual propriedade foi alterada;
 - O Mediator precisa saber sobre todos os objetos que estão colaborando no conjunto, para que possa enviar a
notificação a eles; outra solução é, o próprio Mediator criar estes objetos;
 - Dependendo de sua implementação específica, você pode precisar lidar com o loop infinito de
change-notify-change que pode resultar se o manipulador de alteração de valor do objeto for chamado para
cada alteração de valor, seja de uma fonte externa ou de um mediador.

## A implementação de exemplo:
 - Neste caso de uso, será usado uma implementação de exemplo que utiliza o framework de componentes de
interface gráfica JavaFX, porque será mais fácil de visualizar e entender como o design pattern pode ser
implementado;
 - Será criado uma única classe concreta para representar o Mediator, chamado de UIMediator; neste caso,
não será preciso criar um Mediator abstrato, porque este é um cenário mais simplificado; iremos criar
uma interface que deve ser implementada por cada um dos objetos que desejam participar do conjunto de
colaboração; esta estratégia não é algo que seja solicitado pelo design pattern, mas sim, com o objetivo
de simplificar esta implementação em particular; a interface mencionada anteriormente, é a interface
`UIControl` que é usada para representar um `Colleague` que participa do conjunto de objetos que devem
colaborar entre si;
 - Para este exemplo, será utilizado três componentes de interface que devem colaborar entre si; eles
são: `Slider`, `TextBox`, `Label`; neste caso, quando, por exemplo, o campo de texto - `TextBox`, alterar
seu valor por conta da interação com o usuário da aplicação, os demais componentes de tela podem terão a
chance de reagir a essa alteração do valor do campo de texto do `TextBox`; o mesmo pode ser dito para o
componente `Slider`, onde quando atualizado por conta da interação com o usuário, através do Mediator,
deverá notificar os demais componentes do conjunto de colleagues; sem o uso deste design pattern, Mediator,
o componente, por exemplo, `Slider`, teria que ter uma referência para os demais componentes que ele deseja
notificar quando o valor dele fosse alterado através da interação com o usuário da aplicação; isso faria com
que houvesse um maior acoplamento entre os elementos da interface da aplicação, pois cada componente teria
que manter um referência para os demais elementos de interface;
 - A classe concreta que representa o Mediator nesta implementação em particular, a classe  `UIMediator`,
possui um método de registro de elementos que desejam colaborar entre si, que se chama
`public void register(UIControl control)`; esta classe também possui um método chamado
`public void valueChanged(UIControl control)`; este método serve para que um determinado integrante do grupo
de objetos colaboradores notifique os demais quanto a alteração do seu estado interno;
 - Mas, como lidar com a alteração de valor em um colleague? através da interface estabelecida neste caso
de uso em particular, a interface `UIControl`, ela possui um método chamado `public void controlChanged()` e
outro chamado `public T getValue()`; então, onde quer que haja a alteração de um componente de tela, ele deve
invocar o Mediator (`UIMediator`), com o objetivo de notificar os demais componentes, onde o método que deve
ser invocado recebe como argumento um colleague, que é um `UIControl`; que neste caso é o próprio elemento onde
houve a alteração de estado, portanto, ele recebe como argumento o elemento em si; o papel do Mediator é passar
essa referência de componente de tela onde houve a alteração de estado para os demais componentes (colleagues)
para que, cada um deles, possa obter o valor que foi alterado no objeto recebido, ou seja, invocar o método
`public T getValue()`.

## Considerações de implementação:
 - É importante que o Mediator possa identificar qual objeto fez o envio da notificação, para que ele possa
ser filtrado com o objetivo de não enviar a notificação de volta para o mesmo objeto;
 - Se o método de algum objeto do conjunto de objetos levar muito tempo para desempenhar a ação necessária,
talvez isto possa afetar a performance do design como um todo; esta é uma consideração não somente deste
design pattern, mas sim, em design patterns que utilizam esse mecanisco de notificação, como por exemplo, o
design pattern Observer;
 - Frequentimente acontece de termos a classe Mediator muito complexa, porque ela se torna o ponto central
de comunicação entre diversos objetos e, caso esta comunicação seja mais específica, com relação ao método
que deve ser invocado nos objetos do conjunto de colaboração, isto pode tornar a implementação mais difícil
de manter, assim como, desenvolver testes unitários para essa classe.

## Considerações de design:
 - Um aspecto que deve ser notado é que é possível estender a classe Mediator para criar diferentes variações
com o objetivo de criar uma forma de comunicação, de forma que ele possa ficar dependente da plataforma;
 - Um mediator abstrato muitas vezes não é preciso porque os objetos participando como colleagues são
normalmente os mesmos;
 - É possível usar o design pattern Observer para implementar o mecanismo de notificação dos elementos que
fazem parte do conjunto de objetos colaboradores.

## Exemplos do padrão:
 - Uma característica determinante deste design pattern é, que ele simplifica (streamlines) a
comunicação entre vários objetos; então uma classe que simplesmente invoca métodos em algumas classes
não pode ser chamada de Mediator;
 - A classe javax.swing.ButtonGroup é um exemplo de Mediator; ela toma de conta de assegurar que somente
um elemento do grupo de botões esteja selecionado; os botôes participantes invocam o Mediator
(ButtonGroup) quando eles são selecionados;
 - Muitas vezes o Front Controller é dado como um exemplo do design pattern Mediator; como por exemplo,
o DispatcherServlet do framework Spring MVC; vale notar que o Front Controller é uma forma especializada
de representar o design pattern Mediator.
