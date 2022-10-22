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
