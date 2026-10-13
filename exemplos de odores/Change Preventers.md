# Change Preventers

## Divergent Change

Antes: 
```java
public class Funcionario {
    private String nome;
    private double salario;

    public double calcularSalario(double bonus) {
        return salario + bonus;
    }

    public String gerarRelatorio() {
        return "Funcionário: " + nome
             + "\nSalário: " + salario;
    }
}
```

Depois: 
```java
public class Funcionario {
    private String nome;
    private double salario;

    public double calcularSalario(double bonus) {
        return salario + bonus;
    }

    public String getNome() {
        return nome;
    }

    public double getSalario() {
        return salario;
    }
}

public class RelatorioFuncionario {
    public String gerar(Funcionario funcionario) {
        return "Funcionário: " + funcionario.getNome()
             + "\nSalário: " + funcionario.getSalario();
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | A classe `Funcionario` concentra o cálculo salarial e a geração de relatórios. | As responsabilidades são separadas entre as classes `Funcionario` e `RelatorioFuncionario`. |
| Responsabilidades | A mesma classe precisa ser modificada por motivos diferentes. | Cada classe possui uma responsabilidade mais específica. |
| Manutenção | Alterações no cálculo salarial ou no formato do relatório exigem modificações na mesma classe. | As alterações no relatório podem ser realizadas separadamente, sem modificar diretamente a classe `Funcionario`. |

## Shotgun Surgery

Antes: 
```java
public class Compra {
    public double calcularTotal(double valor) {
        return valor - valor * 0.10;
    }
}

public class NotaFiscal {
    public double calcularValor(double valor) {
        return valor - valor * 0.10;
    }
}

public class RelatorioVendas {
    public double calcularValorVenda(double valor) {
        return valor - valor * 0.10;
    }
}
```

Depois: 
```java
public class CalculadoraDesconto {
    public double aplicarDesconto(double valor) {
        return valor - valor * 0.15;
    }
}

public class Compra {
    private CalculadoraDesconto calculadora =
        new CalculadoraDesconto();

    public double calcularTotal(double valor) {
        return calculadora.aplicarDesconto(valor);
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | A regra de desconto está repetida nas classes `Compra`, `NotaFiscal` e `RelatorioVendas`. | A regra de desconto é centralizada na classe `CalculadoraDesconto`. |
| Repetição | O mesmo cálculo precisa ser implementado em diferentes classes. | As classes utilizam uma implementação compartilhada do cálculo. |
| Manutenção | Uma alteração no percentual de desconto exige modificações em vários pontos do sistema. | A alteração do cálculo pode ser realizada na classe `CalculadoraDesconto`, reduzindo a necessidade de modificar outras classes. |

## Parallel Inheritance Hierarchies

Antes: 
```java
class Funcionario {
}

class FuncionarioCLT extends Funcionario {
}

class FuncionarioPJ extends Funcionario {
}

class RelatorioFuncionario {
}

class RelatorioCLT extends RelatorioFuncionario {
}

class RelatorioPJ extends RelatorioFuncionario {
}
```

Depois: 
```java
interface GeradorRelatorio {
    String gerar();
}

class RelatorioCLT implements GeradorRelatorio {
    public String gerar() {
        return "Relatório de funcionário CLT";
    }
}

class RelatorioPJ implements GeradorRelatorio {
    public String gerar() {
        return "Relatório de funcionário PJ";
    }
}

class Funcionario {
    private GeradorRelatorio geradorRelatorio;

    public Funcionario(GeradorRelatorio geradorRelatorio) {
        this.geradorRelatorio = geradorRelatorio;
    }

    public String gerarRelatorio() {
        return geradorRelatorio.gerar();
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | Existem hierarquias separadas para funcionários e seus respectivos relatórios. | A geração de relatórios utiliza a interface `GeradorRelatorio`, permitindo associar diferentes implementações aos funcionários. |
| Dependência | A criação de um novo tipo de funcionário exige uma classe correspondente na hierarquia de relatórios. | Um funcionário pode utilizar um gerador de relatório apropriado sem exigir uma subclasse correspondente em outra hierarquia. |
| Manutenção | As duas hierarquias precisam evoluir em conjunto, aumentando o esforço de manutenção. | A implementação dos relatórios pode ser modificada ou ampliada de forma mais independente da hierarquia de funcionários. |