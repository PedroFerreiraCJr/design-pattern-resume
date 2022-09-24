# Visitor:
 - Este design pattern permite definir novas operações em um objeto, sem ter que alterar a definição da classe
do objeto;
 - Pense neste design pattern como um objeto ("visitor") que visita todos os nós de uma estrutura de objeto.
Toda vez que nosso visitor visita um objeto em particular da estrutura de objetos, aquele objeto chama um
método específico no visitor, passando ele mesmo como um argumento;
 - O objeto visitor tem métodos definidos que são específicos a uma classe em particular;
 - Toda vez que é preciso criar uma nova operação ou uma nova funcionalidade em nosso objeto existente, nós
iremos criar uma subclasse do visitor, e fornecer a implementação da nova operação naquela classe e visitamos
a estrutura de objetos usando a nova subclasse criada;
 - Os objetos somente implementam um método "accept" onde o visitor é passado como argumento. Os objetos
sabem sobre o método no visitor criado especificamente para ele e invocam aquele método dentro do método
"accept", passando o próprio objeto como argumento;

## Principais papéis:
 - Client: O cliente usa a implementação do Visitor e aplica ela à estrutura de objetos;
 - Visitor: Interface que define uma operação de visita para cada classe Concrete Element; É preciso definir
um método específico para cada classe Concrete Element, ou seja, para cada classe concreta que implementa a
interface Element;
 - Concrete Visitor: Cada implementação da interface Visitor que define uma operação em particular para os
objetos concretos definidos nos métodos da interface implementada (Visitor); Cada implementação executa um
conjunto de operações em particular, dado a interface Visitor implementada;
 - Object Structure: Uma estrutura de objetos que possa enumerar os objetos que implementam a interface
 Element, para que o visitor possa visitá-los um a um;
 - Element: Interface que define o método "accept" que recebe o visitor para executar determinada operação
sobre o objeto visitado; dentro do método "accept" dessa interface, cada objeto que implementa essa interface
chama um método em específico do visitor que foi recebido como argumento;
 - Concrete Element: Classes de implementação concretas da interface Element que definem os objetos que
recebem a visita do objeto que implementa a interface Visitor; chama o método que foi definido
específicamente para esta Concrete Element no objeto visitor (implementação da interface Visitor)
recebido como argumento; a implementação do método "accept" é bem trivial, porque apenas é necessário
invocar o método do objeto argumento visitor passando o argumento "this" para o método do visitor;

## Passos de implementação:
 - Começamos criando a interface que representará o Visitor, que define os métodos de visita para cada classe
Concrete Element que o visitor suporta executar uma operação;
 - O método definido conforme explicação anterior, deve receber como argumento uma referência a objeto de
acordo com a classe Concrete Element que deve ser suportada; sendo comum essa interface ter multiplos métodos
com o prefixo "visit", completando com o nome específico da classe Concrete Element suportada e um parâmetro
do mesmo tipo; mas também é possível usar sobrecarga de método para essa finalidade;
 - As classes onde é preciso suportar uma nova operação (Concrete Element), precisam implementar uma
interface (neste exemplo, chamada de Element), que aceita como parâmetro uma referência a objeto de uma classe
que implemente a interface Visitor;
 - Geralmente o método declarado na interface Element se chama "accept", e declara um parâmetro do tipo da
interface Visitor, então é possível passar qualquer classe que implemente esta interface;
 - É notável que também é possível declarar o método mencionado acima diretamente nas classes concretas sem
o intermédio de uma interface; assim, somente é preciso declarar o parâmetro Visitor, conforme já mencioado;
 - Nos métodos "accept" da interface Element, a implementação irá invocar o método com o prefixo "visit"
particular a classe que implementa a interface Element, e que está declarado na interface Visitor, passando
como argumento o valor "this", referência para a instância do objeto corrente;
 - Posteriormente, é implementado a interface Visitor que tem os métodos com prefixo "visit", que devem
suportar as classes Concrete Element; cada implementação fornece uma funcionalidade específica para uma classe
Concrete Element em particular;

## A implementação de exemplo:
 - Neste exemplo de implementação do design pattern Visitor, nós temos uma interface chamada Employee que faz
o papel da interface Element; este tipo declara um método chamado "accept" que recebe como parâmetro uma
implementação da interface Visitor; para poder reaproveitar código nas implementações de Employee, foi definido
o tipo AbstractEmployee, que por sua vez realiza a interface Employee, possuindo as definições que podem ser
reaproveitadas nas subclasses especializadas de AbstractEmployee;
 - As subclasses: Programmer, ProjectLead, Manager, e VicePresident representam os papéis em uma organização;
 - Então teremos os programadores que reportam para os lideres de projeto; os lideres de projeto reportando
para os gerentes; e por fim, os gerentes reportando aos vice-presidentes; vamos construir uma estrutura de
árvore usando essas classes; então teremos um único vice-presidente representando um departamento, e os
diferentes papéis abaixo dele; agora, digamos que tendo essa estrutura de classes é necessário adicionar
uma nova funcionalidade a essas classes; então, sem modificar essas classes devemos adicionar essa nova 
funcionalidade, sendo possível fazer isso através do design pattern Visitor;
 - Neste exemplo, teremos duas implementações da interface Visitor; a primeira delas é para imprimir algumas
informações sobre os papéis que foram criados; a segunda implementação da interface Visitor, é uma classe que
deve percorrer a estrutura com o objetivo de aplicar uma avaliação (appraisal);
 - Como é de se esperar, a interface Visitor define métodos em sua API para aceitar as classes concretas que
foram criadas: Programmer, ProjectLead, Manager, VicePresident;

## Considerações de implementação:
 - Não é necessário que haja uma classe base ou interface comun aos objetos que o Visitor suporta; neste
exemplo, foi usado uma abstração para todas as classes, mas não é requerido para que o design pattern Visitor
funcione corretamente; mas o código que utiliza o Visitor, e que mantem acesso a estrutura de objetos precisa
estar ciente das classes individuais existentes;
 - Frequentemente a classe que representa o objeto visitor precisa ter acesso ao estado interno dos objetos
no qual operada para que possa efeturar determinado operação; dessa forma, é preciso expor esse estado interno
através de métodos getter/setter;

## Considerações de design:
 - Um efeito deste design pattern é que a funcionalidade relacionada é agrupada em uma única classe visitor
ao invés de espalhada por múltiplas classes; então a adição de novas funcionalidades é tão simples quanto
adicionar uma nova classe visitor; caso não estivessemos usando esse design pattern, a funcionalidade, por
exemplo, neste caso de uso, estaria espalhada por múltiplas classes; assim, a classe Programmer teria que
implementar um novo método para realizar essa operação; as outras classes também precisariam passar por esta
mesma alteração;
 - Uma realização da interface Visitor, também pode acumular estado enquanto percorrendo a estrutura de
objetos; então, assim como comportamento é possível ter estado em nosso objeto visitor; nós não temos que
adicionar um novo estado nos objetos para um comportamento definido no objeto visitor;
 - O visitor pode ser usado para adicionar nova funcionalidade a estrutura de objetos implementada usando
composite, ou pode ser usado para fazer interpretação no design pattern Interpreter;

## Exemplos do padrão:
 - A biblioteca dom4j utiliza este padrão para processar uma estrutura de objetos de uma árvore de nós XML;
 - Outro exemplo de implementação desse design pattern pode ser encontrado no pacote NIO da biblioteca padrão
do Java; a interface que implementa este design pattern é a FileVisitor, tendo como uma implementação a classe
SimpleFileVisitor;

## Comparação de padrões:
 - Visitor: todas as subclasses possivelmente fornecem uma funcionalidade diferente das demais;
 - Strategy: neste design pattern cada subclasse representa um algoritmo separado para resolver o mesmo
problema;
 - Então tendo duas subclasses de visitor é muito provável que elas forneçam implementações de determinada
funcionalidade de maneira diferente;
 - No design pattern Strategy também temos subclasses, no entanto, cada subclasse representa um algoritmo
diferente que resolve o mesmo problema;

## Pontos negativos:
 - Frequentemente a implementação do visitor precisa acessar o estado do objeto em que vai executar
determinada operação; então acabamos fornecendo métodos getter, enfraquecendo o encapsulamento;
 - O suporte a uma nova classe em nosso visitor requer alteração em todas as implementações do visitor, porque
é necessário a definição de um novo método da interface do visitor;
 - Se as classes que o visitor suporta forem alteradas, todas as implementações de visitor também terão que
ser alteradas para trabalhar com as classes alteradas;
