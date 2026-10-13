
# Bloasters

## Long Method
Antes:
```java 
public void processarPedido(Pedido pedido) {
    // Calcula o valor total
    double total = 0;

    for (Produto produto : pedido.getProdutos()) {
        total += produto.getPreco() * produto.getQuantidade();
    }

    // Aplica desconto
    if (total > 500) {
        total *= 0.90;
    }

    // Calcula o frete
    double frete = total > 200 ? 0 : 25;

    // Calcula o valor final
    double valorFinal = total + frete;

    // Exibe o resumo do pedido
    System.out.println("Subtotal com desconto: " + total);
    System.out.println("Frete: " + frete);
    System.out.println("Total: " + valorFinal);
}
```

Depois:
```java 
public void processarPedido(Pedido pedido) {
    double subtotal = calcularSubtotal(pedido);
    double subtotalComDesconto = aplicarDesconto(subtotal);
    double frete = calcularFrete(subtotalComDesconto);
    exibirResumo(subtotalComDesconto, frete);
}

private double calcularSubtotal(Pedido pedido) {
    double total = 0;

    for (Produto produto : pedido.getProdutos()) {
        total += produto.getPreco() * produto.getQuantidade();
    }

    return total;
}

private double aplicarDesconto(double total) {
    return total > 500 ? total * 0.90 : total;
}

private double calcularFrete(double total) {
    return total > 200 ? 0 : 25;
}

private void exibirResumo(double subtotal, double frete) {
    System.out.println("Subtotal com desconto: " + subtotal);
    System.out.println("Frete: " + frete);
    System.out.println("Total: " + (subtotal + frete));
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | Todas as etapas do processamento do pedido estão concentradas em um único método. | O processamento é dividido em métodos menores, cada um responsável por uma etapa. |
| Legibilidade | É necessário analisar todo o método para compreender as etapas do cálculo. | Os nomes dos métodos ajudam a identificar a finalidade de cada etapa. |
| Manutenção | Alterações em uma etapa podem exigir a análise de um método extenso. | As etapas podem ser modificadas separadamente, facilitando a manutenção. |

## Large Class
Antes:
```java 
public class Funcionario {
    private String nome;
    private String cpf;
    private String telefone;

    private double salario;
    private double bonus;

    public void cadastrar() {
        System.out.println("Cadastrando funcionário...");
    }

    public void atualizarDados() {
        System.out.println("Atualizando dados...");
    }

    public double calcularSalario() {
        return salario + bonus;
    }

    public void gerarFolhaPagamento() {
        System.out.println("Gerando folha...");
    }

    public void enviarEmailCobranca() {
        System.out.println("Enviando e-mail...");
    }
}
```
Depois:
```java 
public class Funcionario {
    private String nome;
    private String cpf;
    private String telefone;

    public void cadastrar() {
        System.out.println("Cadastrando funcionário...");
    }

    public void atualizarDados() {
        System.out.println("Atualizando dados...");
    }
}

public class FolhaPagamento {
    public double calcularSalario(double salario, double bonus) {
        return salario + bonus;
    }

    public void gerarFolha() {
        System.out.println("Gerando folha...");
    }
}

public class ServicoEmail {
    public void enviarCobranca() {
        System.out.println("Enviando e-mail...");
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização | A classe `Funcionario` concentra dados pessoais, cálculo salarial, folha de pagamento e envio de e-mails. | As responsabilidades são distribuídas entre `Funcionario`, `FolhaPagamento` e `ServicoEmail`. |
| Responsabilidades | Uma única classe reúne funcionalidades distintas. | Cada classe possui responsabilidades mais específicas. |
| Manutenção | Alterações em diferentes funcionalidades podem exigir modificações na mesma classe. | As funcionalidades podem ser modificadas em suas respectivas classes, facilitando a manutenção. |

## Primitive Obsession
Antes:
```java 
public class Cliente {
    private String nome;
    private String telefone;

    public void definirTelefone(String telefone) {
        this.telefone = telefone;
    }

    public void exibirTelefone() {
        System.out.println(telefone);
    }
}
```
Depois:
```java 
public class Telefone {
    private final String numero;

    public Telefone(String numero) {
        if (numero == null || !numero.matches("\\+?[0-9]{10,15}")) {
            throw new IllegalArgumentException(
                "Número de telefone inválido"
            );
        }

        this.numero = numero;
    }

    public String getNumero() {
        return numero;
    }
}

public class Cliente {
    private String nome;
    private Telefone telefone;

    public void definirTelefone(Telefone telefone) {
        this.telefone = telefone;
    }

    public void exibirTelefone() {
        System.out.println(telefone.getNumero());
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Representação dos dados | O telefone é armazenado como uma `String`, sem validação própria. | O telefone é representado pela classe `Telefone`, que valida o número. |
| Regras de validação | Não existem regras específicas para verificar o formato do telefone. | A validação é centralizada no construtor da classe `Telefone`. |
| Organização | O telefone é tratado apenas como uma sequência de caracteres. | O telefone possui uma representação própria, com regras específicas para esse dado. |

## Long Parameter List
Antes:
```java 
public void gerarRelatorio(
    String dataInicio,
    String dataFim,
    String formato,
    boolean incluirInativos,
    String departamento,
    String ordenacao
) {
    System.out.println("Gerando relatório...");
}
```

Depois:
```java
public class OpcoesRelatorio {
    String dataInicio;
    String dataFim;
    String formato;
    boolean incluirInativos;
    String departamento;
    String ordenacao;
}

public void gerarRelatorio(OpcoesRelatorio opcoes) {
    System.out.println("Gerando relatório...");
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Parâmetros | O método recebe seis parâmetros individuais para configurar o relatório. | O método recebe um único objeto `OpcoesRelatorio`, que reúne as configurações. |
| Legibilidade | A chamada do método pode ficar extensa e dificultar a identificação da finalidade de cada argumento. | A chamada fica mais simples, agrupando as opções em um objeto específico. |
| Manutenção | A inclusão de novas opções pode aumentar ainda mais a lista de parâmetros. | Novas opções podem ser adicionadas à classe `OpcoesRelatorio`, evitando aumentar a lista de parâmetros do método. |

## Data Clumps
Antes:
```java 
public void cadastrarFuncionario(
    String rua,
    String numero,
    String bairro,
    String cep
) {
    System.out.println("Cadastrando funcionário...");
}

public void atualizarEndereco(
    String rua,
    String numero,
    String bairro,
    String cep
) {
    System.out.println("Atualizando endereço...");
}

public void validarEndereco(
    String rua,
    String numero,
    String bairro,
    String cep
) {
    System.out.println("Validando endereço...");
}
```
Depois:
```java
public class Endereco {
    private String rua;
    private String numero;
    private String bairro;
    private String cep;

    public Endereco(
        String rua,
        String numero,
        String bairro,
        String cep
    ) {
        this.rua = rua;
        this.numero = numero;
        this.bairro = bairro;
        this.cep = cep;
    }
}

public class Funcionario{
    public void cadastrarFuncionario(Endereco endereco) {
        System.out.println("Cadastrando funcionário...");
    }

    public void atualizarEndereco(Endereco endereco) {
        System.out.println("Atualizando endereço...");
    }

    public void validarEndereco(Endereco endereco) {
        System.out.println("Validando endereço...");
    }
}
```
| Aspecto | Antes da refatoração | Depois da refatoração |
|---|---|---|
| Organização dos dados | Rua, número, bairro e CEP são recebidos separadamente em diferentes métodos. | Os dados do endereço são agrupados na classe `Endereco`. |
| Repetição | O mesmo conjunto de parâmetros aparece em vários métodos. | Os métodos recebem um objeto `Endereco`, reduzindo a repetição dos parâmetros. |
| Manutenção | Alterações no conjunto de dados podem exigir modificações em diversas assinaturas de métodos. | Os dados do endereço são centralizados em uma classe, facilitando sua organização e evolução. |