# State:
 - O design pattern State, permite aos objetos se comportarem de maneira diferente baseado no estado
interno atual do objeto;
 - Para cada diferente valor de estado que deve ser representado, é criado uma nova classe para manter
o comportamento a ser implementado para aquele determinado estado;
 - Quando o Client solicita uma nova operação, a solicitação é delegada para a classe que representa o
estado atual do objeto;
 - Transições de estado podem ser disparadas pelas próprias classes que representam os comportamentos
de estado; onde cada estado sabe sobre ao menos um outro estado existente;
 - Então, os próprios estados decidem quando é necessário fazer a transição para um novo estado, baseado em
um input que foi recebido de uma solicitação no objeto Context (principal);
 - Um aspecto positivo deste design pattern é que é possível adicionar novos estados através da criação de
novas classes para representar os novos comportamentos (estados), sem ter que alterar a classe principal,
dependendo de como for implementado a transição de estado.

## Principais papéis:
 - Context: representa a classe principal onde a classe Client interage; essa classe utiliza composição
de classes, onde a classe que compõe é um estado que são representados por implementações da interface
State; a classe Context, delega a operação para a classe que mantem o estado atual do objeto;
 - State: interface que define quais são os métodos que estão presentes nas implementações de cada estado, e
que é implementada pelas classes Concrete State;
 - Concrete State: implementa a interface State, e são as representações de um conjunto de valores que são
mantidos como o estado do objeto; essas classes concretas, representam valores, por exemplo, um estado A, B,
ou C; fazendo com que, quando um objeto está no estado A, ele se comporte de uma maneira, geralmente, diferente
do estado representado pelo valor B, e assim para o estado C.

## Passos de implementação:
 - O primeiro passo, é encontrar os valores distintos de cada estado no qual o objeto possa estar; cada
valor de estado irá ser representado por uma classe diferente; essas classes irão fornecer
comportamentos específicos para cada valor que eles representam; por exemplo, se houver um objeto que
representa um pedido, poderá haver um estado para representar, o estado `novo`, `pago`, `em transição`,
`entregue`, `cancelado`;
 - Então, é preciso identificar os valores, que podem existir, e que podem ser representados por uma
classe; essas classes irão definir comportamentos para cada um desses valores;
 - Na classe Context, as implementações de método irão delegar para o objeto de estado atual a operação a ser
realizada; então, cada estado não é exposto para a classe Client; dessa forma, a classe Client não tem
conhecimento sobre o estado atual do objeto Context, que apenas delega a solicitação da invocação de
método para o objeto que representa o estado atual da classe Context;
 - É preciso definir como a transição de estado irá acontecer; o próprio estado pode decidir, através de um
input recebido no método, qual será o próximo estado da classe Context; outra opção é a própria classe
Context realizar a transição de estado baseado nos valores atuais das variáveis de instância dela;
 - A classe Client interage com a classe Context, mas não está ciente da existência das classes que fazem
parte do estado interno da classe Context.

## A implementação de exemplo:
 - Neste exemplo de implementação, será usado uma classe chamada `Order` para abstrair um Pedido; essa
classe é composta por um estado que informa qual a situação atual de um pedido; para este cenário, apenas
o método de cancelamento será implementado; a classe `Order` possui alguns métodos na sua API, mas o método
em questão para este exemplo é o método de `cancelamento`; quando um `Order` (Pedido) for cancelado, de acordo
com o estado atual do pedido, uma determinada implementação da interface `OrderState` irá ser usada para
executar a operação de cancelamento; Por exemplo, caso o estado atual do pedido seja `A`, que é represen-
tado pela classe `New`, a classe `New` será responsável por lidar com a operação de cancelamento daquele
pedido;
 - Os estados são definidos nas realizações da interface `OrderState`; essa interface possui um único método
chamado `public void handleCancellation()`;
 - As classes concretas que implementam a interface acima, são: `New`, `Paid`, `InTransit`, `Delivered`,
`Cancel`;
 - A classe `Order` também possui outros métodos que serão utilizados para fazer a transição de estado
através dela, que são:
`public void paymentSuccessful()`;
`public void dispatcher()`;
`public void delivered()`.

## Considerações de implementação:
 - Em algumas implementações, é possível permtir ao código cliente informar o estado inicial da classe Context;
após a inicialização da classe Context, a transição de estado é feita através das classes de estado ou da
própria classe Context, dependendo da escolha de implementação;
 - Em algumas situações, a classe Client poderá estar em melhor condição de informar qual deve ser o estado
inicial da classe Context (principal);
 - Se a transição de estado for feita pelas classes que representam um estado da classe Context, elas terão
que saber ao menos sobre ao menos uma das outras classes que são implementações de estado; caso seja escolhido
usar essa forma de implementação, se houver a necessidade de adição de outras classes de estado, será
necessário fazer alterações nas classes de estado para que seja possível transitar para o novo estado.

## Considerações de design:
 - Como cada estado é um comportamento, e geralmente não mantem estado da classe Context, é possível
compartilhar as classes de estado em outras instâncias de Context;
 - O design pattern State não é o mesmo que uma máquina de estados; a máquina de estados recebe inputs e
mapeia para estados, geralmente usando uma tabela ou estrutura map; o design pattern State, tem os valores
de estado que representam os diferentes comportamentos de uma classe Context (principal).

## Exemplos do padrão:
 - Um exemplo deste design pattern é o ciclo de vido do framework JSF; a FacesServlet do JSF quando recebe uma
requisição, utiliza deste design pattern para processar a requisição de acordo com as fases do ciclo de vida
do processamento do framework; onde cada fase de processamento de uma requisção, é uma classe que representa
um comportamento a ser executado.

## Comparação de padrões:
 - State vs Command: O design pattern State, implementa um comportamento em si de um objeto específico para
um estado em particular; o design pattern Command, por outro lado, não implementa comportamento, simplesmente
executa chamadas a uma operação específica em determinado receiver;
 - O objeto state representa o estado atual de um objeto Context; o objeto Command, por outro lado, representa
uma operação, ou requisição sem qualquer relação com o estado atual de um receiver, porque os objetos em si
representam duas coisas diferentes.

## Pontos negativos:
 - Um possível ponto negativo é com relação a quantidade de classes que talvez seja necessário desenvolver,
levando em consideração a quantidade de comportamentos que será preciso representar; precisa ser considerado
também que as classes podem ter que ser testadas unitariamente, fazendo com que seja mais trabalhoso
implementar este design pattern;
 - Outro aspecto que pode tornar o código mais difícil de desenvolver é quando há a necessidade de transitar
de um estado atual para múltiplos estados; caso seja implementado a transição nas classes de estado, isso pode
tornar as classes mais acopladas, porque cada classe de estado terá que conhecer sobre as demais que precisam
ser transitadas;
 - Outro ponto negativo é quando não conseguimos perceber quais serão os estados que precisam ser
representados deste o início do desenvolvimento; dessa forma, a medida que o design evolui será preciso
adicionar mais classes, e talvez alterar outras para corrigir a falta de percepção no início do
desenvolvimento.
