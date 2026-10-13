# Dispensables

## Comments

Antes:
```java
public class Pedido {
    private double valor;

    public double funcao() {
        // Multiplica o valor por 1.1 para adicionar 10% de taxa
        return valor * 1.1;
    }
}
```

Depois:
```java
public class Pedido {
    private double valor;

    public double calcularTotal() {
        return valor * 1.1;
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Comentários | O método possui um comentário que descreve a operação realizada pelo código. | O comentário redundante é removido. |
| Legibilidade | O comentário repete uma informação que pode ser compreendida pela leitura da operação. | O código fica mais enxuto, sem perder informações relevantes. |
| Manutenção | Comentários redundantes podem precisar ser atualizados quando o código muda. | A remoção de comentários desnecessários evita inconsistências entre a explicação e a implementação. |

## Duplicate Code

Antes:
```java
public class Compra {
    public double calcularDesconto(double valor) {
        return valor * 0.10;
    }
}

public class Venda {
    public double calcularDesconto(double valor) {
        return valor * 0.10;
    }
}
```

Depois:
```java
public class CalculadoraDesconto {
    public double calcularDesconto(double valor) {
        return valor * 0.10;
    }
}

public class Compra {
    private CalculadoraDesconto calculadora = new CalculadoraDesconto();

    public double calcularDesconto(double valor) {
        return calculadora.calcularDesconto(valor);
    }
}

public class Venda {
    private CalculadoraDesconto calculadora = new CalculadoraDesconto();

    public double calcularDesconto(double valor) {
        return calculadora.calcularDesconto(valor);
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | As classes `Compra` e `Venda` possuem implementações idênticas para calcular descontos. | O cálculo é centralizado na classe `CalculadoraDesconto`. |
| Repetição | A mesma regra de desconto está implementada em duas classes diferentes. | As duas classes utilizam uma implementação compartilhada. |
| Manutenção | Alterações na regra de desconto precisam ser realizadas em diferentes pontos do sistema. | A regra pode ser modificada diretamente na classe `CalculadoraDesconto`. |

## Lazy Class

Antes:
```java
public class ConversorMoeda {
    public double converterParaReal(double valor) {
        return valor;
    }
}

public class Produto {
    private double preco;
    private ConversorMoeda conversor = new ConversorMoeda();

    public double getPreco() {
        return conversor.converterParaReal(preco);
    }
}
```

Depois:
```java
public class Produto {
    private double preco;

    public double getPreco() {
        return preco;
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | A classe `ConversorMoeda` existe apenas para retornar o mesmo valor recebido. | A classe desnecessária é removida. |
| Responsabilidades | A conversão não realiza nenhuma operação efetiva, acrescentando uma camada desnecessária. | A classe `Produto` retorna diretamente o preço armazenado. |
| Manutenção | A existência de uma classe sem funcionalidade relevante aumenta a complexidade do sistema. | A estrutura é simplificada, reduzindo o número de classes desnecessárias. |

## Data Class

Antes:
```java
public class Produto {
    private String nome;
    private double preco;

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public double getPreco() {
        return preco;
    }

    public void setPreco(double preco) {
        this.preco = preco;
    }
}

public class Loja {
    public double calcularPrecoComDesconto(Produto produto) {
        return produto.getPreco() * 0.90;
    }
}
```

Depois:
```java
public class Produto {
    private String nome;
    private double preco;

    public Produto(String nome, double preco) {
        this.nome = nome;
        this.preco = preco;
    }

    public String getNome() {
        return nome;
    }

    public double calcularPrecoComDesconto() {
        return preco * 0.90;
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | A classe `Produto` armazena os dados, enquanto a classe `Loja` realiza o cálculo do desconto. | O cálculo do desconto é transferido para a classe `Produto`. |
| Responsabilidades | Os dados e o comportamento relacionado ao preço estão separados. | O comportamento relacionado ao preço fica junto dos dados correspondentes. |
| Manutenção | Alterações nas regras de cálculo podem exigir modificações em classes que utilizam `Produto`. | A regra de desconto pode ser mantida diretamente na classe `Produto`, quando essa responsabilidade fizer sentido para o domínio. |

## Dead Code

Antes:
```java
public class Calculadora {
    public int somar(int a, int b) {
        return a + b;
    }

    public int multiplicar(int a, int b) {
        return a * b;
    }

    public int subtrair(int a, int b) {
        return a - b;
    }
}
```

Depois:
```java
public class Calculadora {
    public int somar(int a, int b) {
        return a + b;
    }

    public int multiplicar(int a, int b) {
        return a * b;
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Métodos | A classe `Calculadora` possui os métodos `somar`, `multiplicar` e `subtrair`, embora `subtrair` não seja utilizado. | O método `subtrair` é removido após a confirmação de que não possui uso. |
| Organização | O código contém um método sem utilidade para o sistema. | Permanecem apenas os métodos necessários. |
| Manutenção | Código inutilizado aumenta o volume que precisa ser analisado durante a manutenção. | A remoção do código morto simplifica a compreensão da classe. |

## Speculative Generality

Antes:
```java
public class Relatorio {
    public void gerarRelatorio(String formato) {
        if (formato.equals("PDF")) {
            System.out.println("Gerando relatório PDF");
        } else if (formato.equals("CSV")) {
            System.out.println("Gerando relatório CSV");
        } else if (formato.equals("XML")) {
            System.out.println("Gerando relatório XML");
        }
    }
}
```

Depois:
```java
public class Relatorio {
    public void gerarRelatorio() {
        System.out.println("Gerando relatório PDF");
    }
}
```

| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Funcionalidades | A classe `Relatorio` permite gerar relatórios em PDF, CSV e XML, embora apenas PDF seja uma necessidade real do sistema. | A classe oferece somente a geração de relatórios em PDF. |
| Complexidade | O código contém condições e caminhos de execução para formatos que não são necessários. | A implementação fica mais simples, atendendo à necessidade atual. |
| Manutenção | A existência de funcionalidades especulativas aumenta a quantidade de código que precisa ser compreendida e mantida. | A remoção das funcionalidades desnecessárias reduz a complexidade do sistema. |