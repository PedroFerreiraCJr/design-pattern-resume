# Strategy:
 - O Strategy permite encapsular um algoritmo em uma classe;
 - O algoritmo é utilizado na classe Context (principal) através do Strategy,
com o objetivo de alterar a maneira de operação da classe;
 - Este padrão é muito útil quando há diversas variações de um algoritmo, como por exemplo
algoritmos de busca; pois cada algoritmo desempenha a busca de maneira diferente;
 - Uma forma de verificar se existe como se beneficiar deste design é olhando para
o código e em casos onde é encontrado condicionais do tipo if/switch; essa é uma
oportunidade de usar este design;
 - As classes chamadas Strategy (variações concretas de determinado algoritmo), geralmente
são definidas a partir de uma interface ou hierarquia de herança, para que se possa
escolher qualquer uma das implementações.

## Principais papéis:
 - Context: classe principal onde a classe cliente interage; essa classe utiliza a composição
para manter uma referência para a classe Strategy;
 - Strategy: interface contendo a definição da API que será compartilhada por todos
os objetos dessa família de algoritmos;
 - Concrete Strategy: implementações concretas da interface Strategy contendo cada um
dos algoritmos;
 - Client: interage com a classe Context para usar suas funcionalidades, e é essa classe a 
responsável por selecionar o Concrete Strategy.

## Passos de implementação:
 - Primeiro, deve-se definir a interface para os algoritmos, a interface Strategy; geralmente
o Strategy não armazena nenhum estado dentro dele; a classe Context deve fornecer
ao Strategy todas as informações necessárias para o funcionamento dele;
 - O próximo passo é definir os algoritmos que implementam a interface Strategy; cada classe
representa uma variação do algoritmo;
 - A classe Context deve fornecer uma maneira de configurá-la com uma implementação do
Strategy concreta; deve haver uma forma de informar ao Context para usar determinada classe; Um 
aspecto importante a se notar é, que a classe concreta que implementa a interface Strategy
deve ser fornecida ou selecionada pela classe Client.

## A implementação de exemplo:
 - Nesta implementação de exemplo foi usado um programa de impressão de pedidos (Order).
Portanto, foi definida uma interface chamada OrderPrinter com um método a ser implementado
pelas formas concretas de fazer uma impressão de pedido (Order). Neste exemplo, foram implementadas
duas formas, a primeira é uma forma detalhada de impressão (DetailPrinter) e a outra forma
imprime um sumário do pedido (SummaryPrinter). Essas classes podem ser selecionadas pela
classe Client quando interagindo com a classe Context (PrintToFileService), que por ser a
classe Context, tem um relacionamento de composição com a classe OrderPrinter (que é a interface Strategy).
A interface OrderPrinter estabelece um único método, com a seguinte assinatura:
`public void print(List<Order> order)`.
Para tornar o exemplo mais didático foi usado uma classe User para representar um
usuário que faz determinado pedido (Order). O Client faz a solicitação de impressão através
da classe Context, no método:
`public void printOrders(List<Order> orders)`.
Este método é que faz a delegação para a instância concreta disponível no momento.

## Considerações de implementação:
 - É possível implementar a classe Context de uma forma na qual o Strategy seja opcional, dessa forma
as classes Client não precisam lidar diretamente com as implementações concretas do Strategy;
isso seria feito, por exemplo, com um algoritmo default, dessa forma não seria preciso configurar
um algoritmo logo de início;
 - Ao Strategy, deve ser dado todos os argumentos necessário para operar a funcionalidade concreta; em
casos onde o número de parâmetros seja numeroso, é possível estabelecer uma interface para obtenção
dos dados;
 - Os objetos Strategy concretos acabam por serem sem estado, pois os dados que eles precisam para executar a tarefa devem ser passados para o método, ou através de uma interface.

## Considerações de design:
 - As classes concretas do Strategy podem fazer uso de herança para mover uma parte comum do algoritmo
para a classe base, e dessa forma, tornar a implementação das classes concretas mais simples.

## Exemplos do padrão:
 - A interface java.util.Comparator é um ótimo exemplo do uso deste padrão. Somos capazes de criar múltiplas
implementações do comparator, cada um com um algoritmo diferente para executar a comparação e fornecer várias
formas de ordenação.

## Comparação de padrões:
 - Strategy vs State: No Strategy temos uma classe para cada algoritmo; no State temos uma classe por estado;
 - As implementações concretas do Strategy não precisam saber sobre a existência dos outros algoritmos; já
o State, as classes que represetam os estados, precisam saber sobre os demais pois estão relacionados no
momento de fazer a transição de estado, pois cada estado deve saber no mínimo quem é o próximo; ou seja,
se os estados são responsáveis por disparem a troca de estado, eles devem saber ao menos quem é o próximo
estado da transição.

## Pontos negativos:
 - Como a classe Client tem que configurar a classe Context (principal) com o Concrete Strategy, ela deve
saber sobre os algoritmos e, portanto, tem um forte acoplamento; caso seja preciso adicionar algum novo
algoritmo, a classe Client precisará ser alterada para dar suporte a nova classe.
