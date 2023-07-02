# Simple Factory:
 - O objetivo deste padrão de projeto é separar a lógica de instanciação de um objeto para uma classe 
que contém um método em particular, que geralmente é estático;
 - Algumas pessoas não consideram o design pattern **Simple Factory** como sendo um design pattern, porquê
ele é constituído de apenas um método; e que não tem nenhum código complexo;
 - Este design é comumente confundido com o design pattern **Factory Method**;
 - Tipicamente usamos este design pattern quando nós temos algumas classes que podem ser instanciadas, e
onde precisam ser escolhidas de acordo com determinado critério; onde esta instaciação é baseada em uma 
comparação simples de uma variável;

## Principais papéis:
 - **Client**: ;
 - **SimpleFactory**: Geralmente é uma classe que possui um método estático e que fornece uma instância 
da classe relacionada a **Product** baseado em um parâmetro do próprio método de fábrica; fornece um método 
estático para obter uma instância da classe **Product**;
 - **Product**: Interface ou uma classe abstrata que é instanciada de acordo com um determinado critério;
 - **ProductA**, **ProductB**: Implementação da interface ou classe abstrata que possui a lógica que é 
usada pela classe **Client**.






