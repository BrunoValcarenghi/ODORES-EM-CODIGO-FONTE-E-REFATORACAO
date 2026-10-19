# Couplers 

## Feature Envy

Antes:
```java
public class Produto {
    private double preco;
    private double desconto;

    public double getPreco() {
        return preco;
    }

    public double getDesconto() {
        return desconto;
    }
}

public class CalculadoraPedido {
    public double calcularPrecoFinal(Produto produto) {
        return produto.getPreco()
                - (produto.getPreco() * produto.getDesconto());
    }
}
```

Depois:
```java
public class Produto {
    private double preco;
    private double desconto;

    public double getPreco() {
        return preco;
    }

    public double getDesconto() {
        return desconto;
    }

    public double calcularPrecoFinal() {
        return preco - (preco * desconto);
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | A classe `CalculadoraPedido` acessa os dados de `Produto` para calcular o preço final. | O cálculo do preço final é realizado diretamente pela classe `Produto`. |
| Responsabilidades | A lógica de cálculo está em uma classe que depende dos dados de outra. | O comportamento relacionado ao preço fica junto dos dados utilizados no cálculo. |
| Manutenção | Alterações na regra de cálculo podem exigir modificações na classe `CalculadoraPedido`. | A regra de cálculo pode ser modificada diretamente na classe `Produto`. |

## Inappropriate Intimacy

Antes:
```java
public class ContaBancaria {
    public double saldo;
}

public class OperacaoBancaria {
    public void depositar(ContaBancaria conta, double valor) {
        conta.saldo = conta.saldo + valor;
    }
}
```

Depois:
```java
public class ContaBancaria {
    private double saldo;

    public void depositar(double valor) {
        if (valor > 0) {
            saldo += valor;
        }
    }

    public double getSaldo() {
        return saldo;
    }
}

public class OperacaoBancaria {
    public void depositar(ContaBancaria conta, double valor) {
        conta.depositar(valor);
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Encapsulamento | O saldo da conta é público e pode ser alterado diretamente por outras classes. | O saldo é privado e só pode ser modificado por meio dos métodos da classe `ContaBancaria`. |
| Dependência | `OperacaoBancaria` conhece e modifica diretamente um atributo interno de `ContaBancaria`. | `OperacaoBancaria` solicita o depósito por meio de um método público. |
| Manutenção | Alterações na representação interna do saldo podem afetar as classes que o acessam diretamente. | As regras de depósito ficam centralizadas em `ContaBancaria`, facilitando a manutenção. |

## Incomplete Library Class

Uma classe de biblioteca incompleta ocorre quando uma biblioteca externa é útil, mas não oferece uma operação necessária. Como não é possível modificar diretamente o código da biblioteca, a funcionalidade ausente acaba sendo repetida ou espalhada pelo sistema.

Antes:
```java
import java.time.LocalDate;

public class RelatorioVendas {
    public boolean ocorreuNoFimDeSemana(LocalDate data) {
        int dia = data.getDayOfWeek().getValue();
        return dia == 6 || dia == 7;
    }
}

public class AgendaEntrega {
    public boolean ocorreuNoFimDeSemana(LocalDate data) {
        int dia = data.getDayOfWeek().getValue();
        return dia == 6 || dia == 7;
    }
}
```

Depois, usando *Introduce Foreign Method*:
```java
import java.time.LocalDate;

public final class Datas {
    private Datas() {
    }

    public static boolean ocorreuNoFimDeSemana(LocalDate data) {
        int dia = data.getDayOfWeek().getValue();
        return dia == 6 || dia == 7;
    }
}

public class RelatorioVendas {
    public boolean ocorreuNoFimDeSemana(LocalDate data) {
        return Datas.ocorreuNoFimDeSemana(data);
    }
}

public class AgendaEntrega {
    public boolean ocorreuNoFimDeSemana(LocalDate data) {
        return Datas.ocorreuNoFimDeSemana(data);
    }
}
```

| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Limitação da biblioteca | `LocalDate` não possui a operação específica esperada pela aplicação. | A operação complementar fica disponível em uma classe local. |
| Repetição | Cada classe implementa novamente a mesma verificação. | A regra fica centralizada em `Datas.ocorreuNoFimDeSemana()`. |
| Manutenção | Uma mudança na regra precisa ser repetida em todos os consumidores. | A regra pode ser alterada em um único ponto sem modificar a biblioteca externa. |
| Técnica | A funcionalidade ausente é recriada em diferentes classes. | Foi aplicado *Introduce Foreign Method*; para várias operações relacionadas, pode-se considerar *Introduce Local Extension*. |

## Message Chains

Antes:
```java
public class Cidade {
    public String getNome() {
        return "Santa Maria";
    }
}

public class Endereco {
    private Cidade cidade = new Cidade();

    public Cidade getCidade() {
        return cidade;
    }
}

public class Cliente {
    private Endereco endereco = new Endereco();

    public Endereco getEndereco() {
        return endereco;
    }
}

Cliente cliente = new Cliente();
System.out.println(
    cliente.getEndereco().getCidade().getNome()
);
```

Depois:
```java
public class Cidade {
    public String getNome() {
        return "Santa Maria";
    }
}

public class Endereco {
    private Cidade cidade = new Cidade();

    public String getNomeCidade() {
        return cidade.getNome();
    }
}

public class Cliente {
    private Endereco endereco = new Endereco();

    public String getNomeCidade() {
        return endereco.getNomeCidade();
    }
}

Cliente cliente = new Cliente();
System.out.println(cliente.getNomeCidade());
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Chamadas | O código acessa o nome da cidade por meio de uma sequência de chamadas entre objetos. | O nome da cidade é obtido por meio do método `getNomeCidade()` de `Cliente`. |
| Acoplamento | O código depende da estrutura de navegação entre `Cliente`, `Endereco` e `Cidade`. | A sequência de chamadas fica encapsulada nas classes envolvidas. |
| Manutenção | Alterações nos relacionamentos entre os objetos podem exigir modificações no código cliente. | O código cliente não precisa conhecer toda a sequência de objetos para obter o nome da cidade. |

## Middle Man

Antes:
```java
public class Telefone {
    public void ligar(String numero) {
        System.out.println("Ligando para " + numero);
    }
}

public class GerenciadorTelefone {
    private Telefone telefone = new Telefone();

    public void ligar(String numero) {
        telefone.ligar(numero);
    }
}

public class Aplicativo {
    public void realizarLigacao() {
        GerenciadorTelefone gerenciador =
                new GerenciadorTelefone();

        gerenciador.ligar("99999-9999");
    }
}
```

Depois:
```java
public class Telefone {
    public void ligar(String numero) {
        System.out.println("Ligando para " + numero);
    }
}

public class Aplicativo {
    public void realizarLigacao() {
        Telefone telefone = new Telefone();

        telefone.ligar("99999-9999");
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | A classe `GerenciadorTelefone` apenas encaminha a chamada para `Telefone`. | A classe `Aplicativo` utiliza diretamente `Telefone`. |
| Delegação | Existe uma classe intermediária que não acrescenta comportamento relevante à operação. | A chamada é realizada diretamente, eliminando a delegação desnecessária. |
| Manutenção | A existência de uma classe adicional aumenta a quantidade de código envolvida na operação. | A estrutura fica mais simples, com menos métodos intermediários. |
