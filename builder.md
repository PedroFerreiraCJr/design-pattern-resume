# Builder:
 - O design pattern Builder, facilita o uso de construtores com muitos parâmetros;
 - Imagine que você tem duas classes, a classe Address e a classe User. O construtor da classe User
precisa de um objeto da classe Address, e também de uma lista de permissões que o usuário possui. Segue
exemplo do construtor da classe User:

```java
public class User {
    public User(String name, Address address, LocalDate birthday,
        List<Permission> permissions) {
        // ...
    }
}
```

 - É preciso perceber que existe uma ordem lógica para a instanciação de um objeto do tipo **User**, 
pois é preciso que seja fornecido vários argumentos no construtor desta classe. Portanto, é como se 
existesse uma ordem pre-estabelecida na criação deste objeto, ou seja, um conjunto de passos que 
devem ser seguidos para concluir a criação de uma instância da classe **User**. Desta forma, o design 
pattern **Builder** é muito útil nestas ocasiões;
 - Um aspecto bom, portanto, considerado um benefício deste padrão é que ele separa a lógica de criação 
de um objeto completo do código que realmente precisa do objeto complexo criado; Além do mais, este 
design pattern dá mais controle sobre o processo de criação do objeto complexo;
 - Outro aspecto que pode ser considerado um benefício, é que o design pattern **Builder** torna possível 
acabar com o uso direto de um construtor telescópio (que um um anti-padrão); implementando o design 
pattern **Builder** com uma classe interna estática, é possível ter acesso a um único construtor privado
que contenha os parâmetros que seja necessários na instanciação do objeto;

## Descrição Design Pattern Builder:
 - Quando existe um processo complexo de criação de um objeto envolvendo múltiplos passos, o builder 
pode ser usado nestes cassos;
 - Com o Builder nós removemos a lógica de criação de um objeto do "cliente" e colocamos em uma classe 
separada;

## Principais papéis:
 - Builder: O builder fornece as interfaces para criar os objetos "parte"; tem um método que cria o 
objeto desejado, geralmente, o método se chama: `public Product build()`;
 - ConcreteBuilder: Caso o builder seja uma interface ou classe abstrata, esta classe cria a 
implementação concreta que fornece os passos para criar o objeto desejado;
 - Product: Este é o objeto que desejamos criar, e que para ser criado é necessário executar alguns 
passos para concluir a criação do objeto; este é o produto final que desejamos criar;
 - Director: Geralmente o builder possui uma lógica para construtor o objeto desejado, como por exemplo,
ter que invocar os método do builder em determinada order; o Director sabe como usar o objeto builder 
construir novos objetos.

## Passos de implementação:
 - Começamos criando o builder através da identificação dos objetos parte que precisam ser criados antes
de poder instanciar o objeto criado pelo Builder;
 - Você deve fornecer um método para criar o objeto/produto desejado; desta forma este deve ser o método
de montagem do objeto final;
 - Outro passo para que define este padrão é a classe Director; o Director pode ser uma classe separada 
que faz o papel do cliente;

## A implementação de exemplo:
 - Neste exemplo de implementação do design pattern **Builder**, teremos uma classe **User** que faz o 
papel de uma entidade que precisa ser criada. Iremos usar este objeto para construir um objeto do tipo 
**DTO**. Temos também a classe **Address**, que é uma classe normal que armazena as informações de 
endereço de um usuário.
 - A classe **UserWebDTO** é uma classe que implementa a interface **UserDTO**. Portanto, nós iremos criar
classes deste tipo on **Builder**. Esta classe tem a seguinte assinatura no construtor principal:

```java
public class UserWebDTO extends UserDTO {
    public UserWebDTO(String name, String address, String age) {
        this.name = name;
        this.address = address;
        this.age = age;
    }
}
```

 - Nós temos a interface **UserDTOBuilder** que está declarada da seguinte maneira:
 ```java
public interface UserDTOBuilder {
    UserDTOBuilder withFirstName(String firstname);
    UserDTOBuilder withLastName(String lastname);
    UserDTOBuilder withBirthday(LocalDate birthday);
    UserDTOBuilder withAddress(Address address);
    UserDTO build();
}
```

 - Uma coisa a ser percebida é que, geralmente, na construção de um objeto através de um builder, o
builder devolve em cada invocação de método dele, ele devolve ele mesmo. Portanto, é possível notar
neste builder mencionado acima que os método dele, com exceção do método **build**, devolvem um 
**UserDTOBuilder**; e o que isso possibilida é o encadeamento de invocações de métodos, tornando a 
interface de programação do builder mais fluente;
 - O método **build()** é o método que instancia o objeto final desejado pelo cliente; ou seja, é ele
que **monta**, a partir dos valores recebidos nos outros método do builder, o objeto final;
 - No nosso exemplo, a classe concreta do builder será a classe **UserWebDTOBuilder**, segue a 
implementação da mesma;

```java
public class UserWebDTOBuilder implements UserDTOBuilder {

    private String firstname;
    private String lastname;
    private String age;
    private String address;
    
    @Override
    public UserDTOBuilder withFirstName(String firstname) {
        this.firstname = firstname;
        return this;
    }

    @Override
    public UserDTOBuilder withLastName(String lastname) {
        this.lastname = lastname;
        return this;
    }

    @Override
    public UserDTOBuilder withBirthday(LocalDate birthday) {
        Period years = Period.between(birthday, LocalDate.now());
        this.age = Integer.toString(years.getYears());
        return this;
    }

    @Override
    public UserDTOBuilder withAddress(Address address) {
        this.address = address.getHouseNumber() + ", " + address.getStreet() + "\n" + 
            address.getCity() + "\n" + address.getState() + " " + address.getZipcode();
        return this;
    }

    @Override
    public UserDTO build() {
        return new UserWebDTO(this.firstname + " " + this.lastname, this.address, this.age);
    }
}
```

 - Esta classe acima é uma implementação da interface **UserBuilder**. Para representar o papel da classe 
**Director** iremos utilizar um método; a implementação deste método segue abaixo:

```java
public static void main(String[] args) {
    UserDTOBuilder builder = new UserWebDTOBuilder();
    User user = createUser();

    UserDTO dto = directBuild(builder, user);
    System.out.println(dto);
}

private static UserDTO directBuild(UserDTOBuilder builder, User user) {
    return builder.withFirstName(user.getFirstName())
        .withLastName(user.getLastName())
        .withAddress(user.getAddress())
        .withBirthday(user.getBirthday())
        .build();
}
```

 - Uma variação deste design pattern é quando temos a classe **Builder** definida dentro da classe que 
queremos construir; portanto, usando uma classe interna estática é possível alcançar o mesmo objetivo; 
mas isto cria um namespace bem elegante para usar em nossas classes;
 - Para obter uma instância da classe **Builder** interna, basta criar um método estático que devolva uma 
instância desta classe, como o exemplo seguinte:

```java
public static UserDTOBuilder getBuilder() {
    return new UserDToBuilder();
}
```

## Considerações de implementação:
 - Você pode facilmente criar uma classe imutável criando uma implementação de builder que seja uma 
classe interna estática; você irá encontrar este tipo de implementação usado frequentemente até mesmo 
se não for o objetivo criar uma classe imutável;
 - Nem sempre é preciso criar um builder abstrato, pois nem sempre existe uma hierarquia na criação dos 
objetos "produto";

## Exemplos do padrão:
 - Um exemplo que pode ser considerado uma implementação do design pattern Builder é a classe 
StringBuilder do JDK;
 - No JDK a partir da versão 8, existe uma classe interna chamada de Builder na classe Calendar.

## Comparação de padrões:
 - Comparação do design pattern Builder com o Prototype; o design pattern **Builder** usa construtor da 
classe para instanciar o objeto que precisa ser criado, ao contrário do design pattern **Prototype** que 
usa o método clone da classe **Object** para criar um objeto a partir de um outro objeto já construído.

## Pontos negativos:
 - Considerando alguns aspectos relacionados a complexidade de um design pattern, considerando a maneira 
correta de uso, assim como uma implementação correta, este design pattern não possui tantas dificuldades 
de implementação ou tantos pontos negativos;
 - O que pode tornar um pouco dificil de entender é o que diz respeito a novos usuários da linguagem Java 
quanto ao encadeamento de método, isto pode tornar o entedimento um pouco complicado.










