# Object-Orientation Abusers

## Switch Statements
Antes:
```java
public class Ingresso {

    public double calcularPreco(String tipo) {
        switch (tipo) {
            case "COMUM":
                return 30.0;

            case "ESTUDANTE":
                return 15.0;

            case "VIP":
                return 60.0;

            default:
                throw new IllegalArgumentException(
                    "Tipo de ingresso inválido"
                );
        }
    }
}
```

Depois:
```java
abstract class Ingresso {

    public abstract double calcularPreco();
}

class IngressoComum extends Ingresso {

    @Override
    public double calcularPreco() {
        return 30.0;
    }
}

class IngressoEstudante extends Ingresso {

    @Override
    public double calcularPreco() {
        return 15.0;
    }
}

class IngressoVIP extends Ingresso {

    @Override
    public double calcularPreco() {
        return 60.0;
    }
}

public class Main {

    public static void main(String[] args) {

        Ingresso ingresso = new IngressoVIP();

        System.out.println(
            ingresso.calcularPreco()
        );
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | O método utiliza uma estrutura `switch` para identificar o tipo de ingresso e calcular seu preço. | Cada classe de ingresso implementa seu próprio método de cálculo. |
| Inclusão de novos tipos | É necessário adicionar uma nova condição ao `switch` para cada tipo de ingresso. | É possível criar uma nova subclasse com seu próprio comportamento. |
| Responsabilidades | A classe concentra a lógica de cálculo dos diferentes tipos de ingresso. | A lógica de cálculo fica distribuída entre as classes específicas. |

## Temporary Field
Antes:
```java
public class CalculadoraImposto {

    private double valorBase;
    private double taxaImposto;

    public double calcularImposto(
        double valor, double taxa
    ) {
        this.valorBase = valor;
        this.taxaImposto = taxa;

        return valorBase * taxaImposto;
    }
}
```

Depois:
```java
public class CalculadoraImposto {

    public double calcularImposto(
        double valorBase, double taxaImposto
    ) {
        return valorBase * taxaImposto;
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Armazenamento dos dados | `valorBase` e `taxaImposto` são armazenados como atributos da classe. | Os valores são recebidos como parâmetros do método. |
| Estado do objeto | O objeto mantém atributos que são necessários apenas durante o cálculo. | O cálculo não depende de atributos adicionais armazenados no objeto. |
| Organização | Os dados do cálculo ficam definidos no escopo da classe. | Os dados ficam restritos ao método que precisa deles. |

## Refused Bequest 
Antes:
```java
class Animal {

    public void andar() {
        System.out.println("O animal está andando.");
    }

    public void voar() {
        System.out.println("O animal está voando.");
    }
}

class Cachorro extends Animal {

    @Override
    public void voar() {
        throw new UnsupportedOperationException(
            "Cachorros não podem voar!"
        );
    }
}
```
Depois:
```java
class Animal {

    public void andar() {
        System.out.println("O animal está andando.");
    }
}

interface Voador {

    void voar();
}

class Cachorro extends Animal {
    // Cachorros podem andar, mas não voar.
}

class Aguia extends Animal implements Voador {

    @Override
    public void voar() {
        System.out.println("A águia está voando.");
    }
}
```

| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Herança | `Cachorro` herda um método incompatível com sua natureza. | Cada classe possui apenas os comportamentos apropriados. |
| Métodos desnecessários | É necessário sobrescrever `voar()` para lançar uma exceção. | `Cachorro` não possui o método `voar()`. |
| Organização | A classe pai reúne comportamentos que não servem a todos os animais. | Os comportamentos são organizados conforme as capacidades dos animais. |

## Alternative Classes with Different Interfaces
Antes:
```java
class Pix {
    public void pagarPix(double valor) {
        System.out.println("Pagamento via Pix: " + valor);
    }
}

class Cartao {
    public void realizarPagamento(double valor) {
        System.out.println("Pagamento via cartão: " + valor);
    }
}
```
Depois:
```java
interface Pagamento {
    void pagar(double valor);
}

class Pix implements Pagamento {
    @Override
    public void pagar(double valor) {
        System.out.println("Pagamento via Pix: " + valor);
    }
}

class Cartao implements Pagamento {
    @Override
    public void pagar(double valor) {
        System.out.println("Pagamento via cartão: " + valor);
    }
}

public class ProcessadorPagamento {
    public void processarPagamento(Pagamento pagamento) {
        pagamento.pagar(100.0);
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Interface | As classes possuem métodos com nomes diferentes para realizar pagamentos. | Ambas implementam a interface `Pagamento` e utilizam o método `pagar()`. |
| Reutilização | O código precisa conhecer o método específico de cada implementação. | O código pode utilizar qualquer implementação de `Pagamento` sem conhecer seus detalhes internos. |
| Manutenção | A inclusão de novas formas de pagamento pode exigir adaptações no código que as utiliza. | Novas formas de pagamento podem implementar a interface `Pagamento`, facilitando sua integração. |
