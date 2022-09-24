# Template Method:
 - Usando o design pattern Template Method é definido um método que pode conter uma série de passos; essa
série de passos devem ser implementadas como métodos abstratos que por sua vez devem ser implementados
pelas subclasses concretas;
 - Também é possível utilizar o reproveitamento de métodos definidos na superclasse, ou caso necessário,
podem ser sobrescritos;
 - Os métodos definidos como abstratos são conhecidos como hooks, e muitas vezes são invocados em métodos
da superclasse, o que possibilita nas subclasses o reaproveitamento do algoritmo que foi definido na
superclasse; as subclasses devem implementar os passos que são abstratos;
 - Este design pattern também é um exemplo de inversão de controle (conhecido também como princípio de Hollywood).

## Principais papéis:
 - Abstract Class (Template Method): classe que define o algoritmo principal, assim como, os métodos
 abstratos (hooks) que são usados no algoritmo principal, e que devem ser implmentados pelas subclasses
para preencher as lacunas no algoritmo com código específico da implementação (subclasse concreta);
 - Concrete Class: as classes que derivam da implementação do design pattern Template Method devem
descrever a partir da implementação dos métodos abstratos (hooks) da superclasse, como os passos definidos
no algoritmo principal da superclasse são executados quando invocados nas implementações concretas do
Template Method.

## Passos de implementação:
 - Começamos definindo o método que será o template method; deve ser feito a quebra do método principal em
métodos abstratos, que serão implementados pelas subclasses;
 - Uma coisa a se notar, é que não se deve exagerar na quantidade de métodos para realização do algoritmo
como um todo, pois isso pode tornar a implementação pelas subclasses dificultosa;
 - Posteriormente a definição da superclasse (Template Method), é possível fazer a implementação das
subclasses.

## A implementação de exemplo:
 - Neste exemplo, para implementar o design pattern Template Method será usado um caso onde deve ser
possível criar diferentes formas de formatação da impressão de um objeto do tipo Order, em um arquivo.
A classe que faz o papel de implementar o design pattern Template Method é a classe OrderPrinter.
Nessa foi descrito um algoritmo principal, método público implementado nesta mesma classe, que é o
método que caracteriza este padrão de projeto. Este método possui hooks, métodos abstratos que são invocados por esta mesma classe com o objetivo de tornar possível a alternância de determinadas partes
do algoritmo principal de acordo com a implementação feita por suas subclasses;
 - Neste cenário, serão implementadas duas subclasses concretas. Uma para impressão no formato HTML, e
outra para impressão no formato textual;
 - Dessa forma, será preciso escolher qual forma de impressão é desejada, selecionando a subclasse que
deve desempenhar a execução do algoritmo principal. Isso pode ser feito de forma polimórfica, atribuindo
à superclasse uma instância da subclasse concreta, podendo assim, tornar o código menos acoplado a
determinada implementação concreta.

## Considerações de implementação:
 - Deve ser levado em consideração a granularidade dos métodos hook da classe Template Method para que haja
um equilíbrio na quantidade de métodos a serem implementados, porque caso sejam muitos métodos a serem
implementados, a criação de subclasses pode se tornar uma tarefa muito honesora e tediosa. É preciso ter
um equilíbrio pois caso sejam poucos muitos métodos, pode ser uma indicação de que os passos estão
desempenhando um papel muito primitivo; caso sejam poucos métodos, pode ser uma indicação de que as subclasses
estão não apenas implementando as lacunas no algoritmo principal, mas sim, fazendo por completo o algoritmo;
 - As subclasses devem ter pouco controle sobre o algoritmo principal, devendo apenas implementar pequenas
partes;
 - Também deve ser levado em consideração tornar o método principal da classe Template Method um método final,
para que o algoritmo principal não possa ser alterado por completo por subclasses.

## Considerações de design:
 - É possível utilizar a herança em subclasses que implementam os hooks da superclasse Template Method, com o
objetivo de reaproveitar essa implementação em outras classes derivadas; assim, somente alguns dos passos
terão que ser reimplementados;
 - O design pattern Factory Method usa este padrão de projeto.

## Exemplos do padrão:
 - As classes abstratas java.util.AbstractMap, e java.util.AbstractSet do framework de coleções do Java são
exemplos de classes que implementam o design pattern Template Method.

## Comparação de padrões:
 - No design pattern Template Method, todas as subclasses criadas são implementações de passos do mesmo
algoritmo;
 - No design pattern Strategy, cada classe representa um novo algoritmo, e que não tem relação com as demais
classes que implementam o Strategy;
 - No design pattern Template Method, o código cliente se baseia somente na herança para obter uma variação do
mesmo algoritmo;
 - No design pattern Strategy, o código cliente usa principalmente composição para configurar a classe
principal com um objeto strategy escolhido.

## Pontos negativos:
 - O rastreamento do código executado requer que seja analisado multiplas classes porque é usado tanto a
superclasse (Template Method) para realizar a tarefa, assim como subclasses que implementam os passos do
algoritmo principal;
 - As subclasses podem por si herdar diretamente de outras implementações para reaproveitar código de delas
que foram feitos e apenas customizar de acordo com a necessiadade.
