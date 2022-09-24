# Iterator:
 - O design pattern Iterator permite uma forma de acessar os elementos/filhos de um objeto agregado em
sequência enquanto escondendo a estrutura de dados interna utilizada;
 - Um objeto agregado é um objeto que contem uma coleção como estado;
 - Este design pattern permite abstrair a estrutura de dados interna que o objeto agregado utiliza, tornando
possível acessar os elementos/filhos contidos no agregado;
 - O objeto agregado deve ser capaz de devolver um objeto iterator que possibilite ao cliente acessar os
elementos/filhos que ele possui;
 - Na linguagem Java os iterators são parte integral do framework de coleções e eles são implementações deste
design pattern;
 - Os iterators são stateful, isso significa que um objeto iterator lembra a sua posição enquanto iterando
os elementos da coleção;
 - Se a coleção subjacente se altera enquanto iterando sobre a coleção, então o iterator se torna inválido,
porque o iterator trabalha com a suposição que a coleção permanece constante;

## Principais papéis:
 - Agreggate: Interface que estabelece API para criar um objeto da interface Iterator; geralmente é um único
método que devolve uma instância de Iterator;
 - Concrete Agreggate: O objeto que representa este papel é que tem a coleção/estado internamente e que
implementa a interface Aggregate com o objetivo de retornar uma instância de Concrete Iterator;
 - Iterator: Interface que dá nome ao design pattern, e que serve para estabelecer a API de iteração pela
coleção/estado interno de um objeto Concrete Agreggate;
 - Concrete Iterator: É uma implementação da interface Iterator; geralmente tem o estado que permite saber
em qual posição da coleção está a iteração atual;
 - Client: Classe que tem acesso ao objeto Concrete Agreggate tornando possivel acessar através da API deste
objeto um Concrete Iterator que deve ser retornado como implementação da interface Iterator, declarada na API
da interface Agreggate;

## Passos de implementação:
 - Começamos definindo a interface Iterator; onde o código cliente terá acesso a ela para executar a obtenção
os respectivos valores em cada iteração;
 - O Iterator possui métodos para checar se há um próximo elemento na sequência, e um método para obter o
elemento;
 - Então definimos a implementação da interface Iterator, que geralmente é feita através de classes internas
em nossa classe Concrete Agreggate; tornando ela uma classe interna facilita o acesso a estrutura de dados
de coleção;
 - O Concrete Iterator precisa manter estado para informar sua posição na coleção do Concrete Agreggate; se a
coleção interna se altera, o Concrete Iterator pode lançar uma exceção para indicar o estado inválido; por
exemplo, caso tenha sido obtido um iterator e em determinado momento da iteração sobre ele, a coleção interna
for alterada, então o estado do iterator se torna inválido o que faria a exceção ser lançada;

## A implementação de exemplo:
 - Neste exemplo será estabelecido uma enumeração contendo algumas declarações de constantes; essa enumeração
é a ThemeColor que define um método para a obtenção de um Iterator para percorrer os valores das constantes
que foram definidas nesta enumeração; é preciso definir a interface Iterator, geralmente com os seguintes
métodos `public boolean hasNext();`, e `public ThemeColor next()`; para este exemplo será definido a classe
Concrete Iterator chamada ThemeColorIterator que implementa a interface Iterator; a classe que representa
o Concrete Iterator (ThemeColorIterator) será implementada como uma classe interna dentro da enumeração;

## Considerações de implementação:
 - A detecção de alterações na estrutura de dados subjacente no momento em que algum código está usando
o iterator é importante para notificador o cliente, porque dessa forma o iterator pode não funcionar corretamente;
 - Ter uma implementação de iterator como uma classe interna torna mais fácil acessar a coleção interna do
objeto agregado; dessa forma, não é preciso expor a estrutura de dados da coleção para que seja acessado
externamente por outras classes;

## Considerações de design:
 - Sempre de preferência a usar uma interface para definir o contrato do iterator, então você pode alterar
a implementação sem afetar o cliente; assim como, esconder a classe de implementação do código cliente; dessa
forma, é obtido uma flexibilidade pois poderá ser alterado a implementação do iterator sem afetar o cliente;
 - Iterator tem diversas aplicações onde uma coleção não é usada diretamente, mas nós ainda desejamos obter um
acesso sequencial a informação, para por exemplo, poder ler as linhas de um arquivo, através da rede;
 - Também é possível fornecer acesso a um recurso através da rede utilizando o design pattern Iterator;

## Exemplos do padrão:
 - As classes iterator no framework de coleções Java são ótimos exemplos de implementação do iterator; As
classes concretas são tipicamente classes internas em cada classe de coleção implementando a interface
`java.util.Iterator`;
 - A classe `java.util.Scanner` também é um exemplo de implementação do design pattern Iterator; essa classe
suporta `InputStream` e permite iterar sobre um stream;

## Pontos negativos:
 - Acesso ao index durante a iteração não está prontamente disponível como nós temos no loop for;
 - Fazer modificações a coleção enquanto alguém está usando um iterator frequentemente torna a instância do
iterator inválida, porque o estado pode não ser válido;
