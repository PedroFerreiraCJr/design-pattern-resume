# Bridge:
 - Usando a herança da maneira convencional abstração e implementação normalmente ficam muito acopladas;
através do uso deste design pattern é possível desacoplar essas classes para que ambas possam variar sem
afetar uma a outra; nós alcançamos essa capacidade através da criação de duas hierarquias de herança
separadas, uma para a implementação e outra para a abstração; 
 - Este design pattern cria uma hierarquia de herança para a abstração, que é usada pelo código da classe
cliente; então o código cliente usa uma classe das abstração; essas hierarquias estão conectadas através
do conceito de composição de classes, da Programação Orientada à Objetos.

## Principais papéis:
 - Abstraction: classe/interface que define a API da abstração; possui uma referência para a implementação;
o código cliente usa a classe/interface que define a abstração;
 - Refined Abstraction: classe derivada que especializa a abstração;
 - Implementor: classe/interface base para classes de implementação, que fornece métodos que são
esperados pela classe Abstraction; métodos não estão relacionados a Abstraction, e tipicamente
representam pequenos passos necessários; é possível que essa classe/interfae tenha métodos que realizam
pequenas tarefas, que são necessárias para a classe Abstraction; então é relevante notar que esta classe
não possui métodos que não tem um relacionamento direto com os métodos fornecidos pela classe Abstraction;
 - Concrete Implementor: classe que realiza as operações da classe Implementor;

## Passos de implementação:
 - O primeiro passo é definir os métodos da classe/interface Abstraction, que é usada pela classe Client;
é possível ter uma classe derivada que especializa o comportamento definido em Abstraction, mas essa
especialização é opcional; Abstraction não necessariamente precisa ser uma classe abstrata; a questão é
que, por ser uma abstração, deve possuir método que abstraem as complexidades ou implementações
da classe Client;
 - Posteriormente, definimos um ou mais Implementor; por ser uma classe separada, é possível definí-la
como uma interface;
 - Uma instância da classe Abstraction é criada através da composição dela com uma classe concreta de
Implementor, que é necessária para fornecer as operações da Abstraction;

## A implementação de exemplo:
 - Neste exemplo de implementação do design pattern Bridge, temos uma classe Client que precisa de
uma coleção que implemente o algoritmo FIFO; a classe que representa a abstração é a classe
`FifoCollection`, e possui os métodos `offer(E e)`, e `poll()`; neste exemplo será usado uma classe
especializada desta abstração, chamada de `Queue`, que por sua vez, possui os métodos `offer(E e)`,
e `poll()`; o método `offer(E e)`, insere o argumento recebido no final coleção; já o método `poll()`,
remove o primeiro elemento da coleção;
 - A classe para representar o Implementor que será usada neste exemplo, é a classe `LinkedList`, que possui
os métodos `addFirst(E e)`, `removeFirst()`, `addLast(E e)`, `removeLast()`, e que não tem um correlaçao
direta com nenhum dos métodos da classe `FifoCollection`, mas que podem ser usados para fornecer a realização
do algoritmo desejado pela classe Client; essa classe tem duas subclasses, a classe `SinglyLinkedList`, e
`ArrayLinkedList`; que por serem subclasses possuem os mesmos métodos mencionados acima; a primeira subclasse
utiliza uma estrutura de node para organizar os elementos da coleção; a outra classe - `ArrayLinkedList`,
usa uma estrutura de array para armazenar os elementos da coleção;
 - A classe `FifoCollection`, que faz o papel de Abstraction, tem uma referência para a classe `LinkedList`,
que por sua vez, faz o papel de Implementor;
 - Quanto a hierarquia de abstração, é possível adicionar mais métodos a classe `FifoCollection`, assim como,
adicionar novas classes através da herança de classes; isso faz com que seja possível alterar a abstração
sem que seja necessário alterar a implementação (Implementor); por outro lado, é possível adicionar métodos
a classe Implementor, sem que seja necessário alterar a classe que faz o papel de Abstraction; ou seja, podem
variar independentemente;

## Considerações de implementação:
 - A classe de abstração pode decidir por conta própria qual implementação de Implementor usar em
seu construtor, ou podemos delegar essa decisão para uma classe de terceiro; nesta última abordagem a
classe Abstraction permanece sem saber das implementações de Implementor, pois há um desacoplamento entre
as classes, onde a Abstraction recebe somente uma interface ou classe abstrata do Implementor;

## Considerações de design:
 - O design pattern Bridge fornece uma ótima extensibilidade pois nos permite alterar a abstração Abstraction
e o Implementor de maneira independente;
 - Através do uso do design pattern Abstract Factory para criar os objetos Abstraction com a implementação
correta, é possível desacoplar os Implementors concretos da abstração;

## Exemplos do padrão:
 - Um exemplo deste padrão é encontrado na API JDBC, mais especificamente a classe `DriverManager`, e a
interface `Driver`, que formam o uso deste design;
 - Outro exemplo frequente do design pattern Bridge, é o método `Collections.newSetFromMap()`; este método
retorna uma instância da interface `Set`, que é baseada no argumento do tipo `Map` passado para este
método;
 - Um aspecto a se notar, é que este design pattern é similar ao design pattern Adapter; mas tem intenções
diferentes porque o Adapter é aplicado a necessidade de adaptar uma classe existente para uma outra
interface; enquanto o design pattern Bridge, é mais considerado uma decisão de design, pois é considerado
seu uso na criação de uma nova classe;

## Comparação de padrões:
 - Bridge vs Adapter: estes design são muito semelhantes estruturalmente, pois mantem uma referência
para uma classe que deve executar as operações; mas a intenção do design pattern Bridge é permitir
a Abstraction e Implementor variarem independentemente; por sua vez, o design pattern Adapter tem por
objetivo fazer com que classes não relacionadas trabalhem conjuntamente;
 - O design pattern Bridge tem que ser projetado desde o início, somente então podemos ter a variação
da abstração e implementação; o Adapter tem sua real utilização tipicamente onde um sistema legado tem
que ser integrado com um código novo;

## Pontos negativos:
 - É considerado um pouco complexo entender e implementar o design pattern Bridge;
 - É preciso ter um bom entendimento de todas as classes que podem estar relacionadas para que possa ser
tomada a decisão de implementar este design pattern;
 - O design pattern Bridge precisa ser considerado deste início do projeto. Adicionar o Bridge a um código
legado é difícil; até mesmo em um projeto que esteja em andamento e considerar o uso do design pattern
Bridge posteriormete, pode requerer um considerável montante de retrabalho;
