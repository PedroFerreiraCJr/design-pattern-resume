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
 - ;

