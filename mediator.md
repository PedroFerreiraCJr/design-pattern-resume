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
o mediator precisará ser alterado com a adição do novo tipo de objeto;

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
método em específico de cada Concrete Colleague;
