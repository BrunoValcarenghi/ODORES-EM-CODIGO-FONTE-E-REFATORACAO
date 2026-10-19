# ODORES EM CÓDIGO-FONTE E REFATORAÇÃO

### Integrantes do grupo:
- **Bruno Fetzer** - 202511362
- **Bruno Machado** - 202411968
- **Davi** - 202410357
- **Frederico** - 202411092

---

# 🎓 Plano de Aula: Odores em Código-Fonte e Refatoração

## 📌 PARTE 1: O que é Odor de Código? (~10 Slides)
**Objetivo:** Apresentar o conceito central, alinhar conceitos de Engenharia de Software e diferenciar erros de sintaxe/bugs de odores estruturais[cite: 2].

- **Slide 1:** Capa da Apresentação (Título, Disciplina, Autores/Professor)[cite: 1]
- **Slide 2:** Visão Geral da Aula e Objetivos
- **Slide 3:** O que é um Software Profissional? (Código + Documentação + Evolução)[cite: 2]
- **Slide 4:** Qualidade de Software segundo Sommerville (Manutenibilidade, Confiabilidade e Usabilidade)[cite: 2]
- **Slide 5:** Definição Formal de *Code Smell* (Odor de Código)[cite: 2]
- **Slide 6:** Sintomas Superficiais: Por que o código funciona, mas "cheira mal"?[cite: 2]
- **Slide 7:** Odor de Código $\neq$ Bug ou Erro de Compilação
- **Slide 8:** O Impacto dos Odores no Custo de Manutenção e Evolução[cite: 2]
- **Slide 9:** Investigação e Contexto: Quando um odor exige ação e quando pode ser mantido?[cite: 2]
- **Slide 10:** Resumo da Parte 1 & Pergunta para Reflexão da Turma

---

## 📜 PARTE 2: História e Filosofia (~10 Slides)
**Objetivo:** Explicar as origens do termo, os principais autores que fundamentaram a prática e os princípios da Orientação a Objetos envolvidos[cite: 3, 5].

- **Slide 11:** Origem do Termo: Kent Beck e a Metáfora ("Se está cheirando mal, troque-o")[cite: 3]
- **Slide 12:** Consolidação Teórica: Martin Fowler e o Livro *Refactoring*[cite: 2, 12]
- **Slide 13:** A Filosofia da Orientação a Objetos segundo Manzano (Filosofia vs. Ferramenta)[cite: 5]
- **Slide 14:** Princípios de Design Limpo e SOLID (Breve Panorama)
- **Slide 15:** O Custo do *Overhead* Histórico vs. Compiladores Modernos[cite: 3]
- **Slide 16:** A Plataforma *Refactoring.Guru* e a Taxonomia dos Odores[cite: 3]
- **Slide 17:** As 5 Categorias Principais de Odores (Visão Geral):[cite: 3]
  - Bloaters (Inchaço)[cite: 3]
  - Object-Orientation Abusers (Abusadores da OO)[cite: 3, 5]
  - Change Preventers (Prevenção de Mudanças)[cite: 3, 7]
  - Dispensables (Dispensáveis)[cite: 3, 8]
  - Couplers (Acopladores)[cite: 3, 10]
- **Slide 18:** Por que os odores surgem de forma gradual? (Evolução contínua vs. Prazos)[cite: 3, 9]
- **Slide 19:** O Efeito Dominó: Como um odor acarreta outros odores[cite: 11]
- **Slide 20:** Resumo da Parte 2

---

## ☣️ PARTE 3: Exemplos de Odores em Código (~30 a 35 Slides)
**Objetivo:** Detalhar os 23 odores de código da taxonomia do Refactoring.Guru, organizados pelas 5 categorias, apresentando definições e diagramas/código para cada um[cite: 3, 11].

### Categoria 1: Bloaters (Inchaço) (~8 slides)[cite: 3]
- **Slide 21:** Categoria Bloaters: O que é e como se forma[cite: 3]
- **Slide 22:** *Long Method* (Método Longo) — Definição e indícios (uso de comentários internos)[cite: 3]
- **Slide 23:** *Large Class* (Classe Grande) — Excesso de campos e responsabilidades[cite: 3, 4]
- **Slide 24:** *Primitive Obsession* (Obsessão Primitiva) — Uso exagerado de tipos primitivos para dados do domínio[cite: 4]
- **Slide 25:** *Long Parameter List* (Lista Longa de Parâmetros) — Dificuldade de legibilidade e uso[cite: 4]
- **Slide 26:** *Data Clumps* (Agrupamentos de Dados) — Variáveis que sempre andam juntas[cite: 4, 5]
- **Slide 27:** Estudo de Caso / Exemplo Prático: Bloaters
- **Slide 28:** Quiz Rápido / Discussão sobre Bloaters

### Categoria 2: Object-Orientation Abusers (Abusadores da OO) (~7 slides)[cite: 5]
- **Slide 29:** Categoria OO Abusers: Aplicação incorreta dos conceitos de OO[cite: 5]
- **Slide 30:** *Switch Statements* (Instruções Switch) — Ausência de Polimorfismo e fragilidade[cite: 5, 6]
- **Slide 31:** *Temporary Field* (Campo Temporário) — Atributos usados apenas em momentos isolados[cite: 6]
- **Slide 32:** *Refused Bequest* (Herança Recusada) — Subclasses que ignoram a interface do pai[cite: 6]
- **Slide 33:** *Alternative Classes with Different Interfaces* — Classes similares sem padronização[cite: 6, 7]
- **Slide 34:** Estudo de Caso / Exemplo Prático: Polimorfismo vs. Switch[cite: 5, 6]
- **Slide 35:** Quiz Rápido / Discussão sobre OO Abusers

### Categoria 3: Change Preventers (Prevenção de Mudanças) (~5 slides)[cite: 7]
- **Slide 36:** Categoria Change Preventers: A má distribuição de responsabilidades[cite: 7]
- **Slide 37:** *Divergent Change* (Mudança Divergente) — 1 Classe mudando por múltiplos motivos[cite: 7]
- **Slide 38:** *Shotgun Surgery* (Cirurgia de Espingarda) — 1 Mudança afetando várias classes[cite: 7]
- **Slide 39:** *Parallel Inheritance Hierarchies* — Criar subclasses em cadeia[cite: 7, 8]
- **Slide 40:** Comparativo: Divergent Change vs. Shotgun Surgery[cite: 7]

### Categoria 4: Dispensables (Dispensáveis) (~8 slides)[cite: 8]
- **Slide 41:** Categoria Dispensables: Elementos redundantes e desnecessários[cite: 8]
- **Slide 42:** *Comments* (Comentários) — O "desodorante" do código vs. uso legítimo[cite: 8]
- **Slide 43:** *Duplicate Code* (Código Duplicado) — Duplicação explícita vs. duplicação sutil[cite: 8, 9]
- **Slide 44:** *Lazy Class* (Classe Preguiçosa) — Classes com pouca ou nenhuma utilidade[cite: 9]
- **Slide 45:** *Data Class* (Classe de Dados) — "Dados burros" sem comportamento[cite: 9]
- **Slide 46:** *Dead Code* (Código Morto) — Trechos e variáveis inacessíveis[cite: 9, 10]
- **Slide 47:** *Speculative Generality* (Generalidade Especulativa) — Código para o futuro que nunca chega[cite: 10]
- **Slide 48:** Estudo de Caso: Limpeza de Código Dispensável[cite: 8]

### Categoria 5: Couplers (Acopladores) (~6 slides)[cite: 10]
- **Slide 49:** Categoria Couplers: O risco do acoplamento excessivo[cite: 10]
- **Slide 50:** *Feature Envy* (Inveja de Recurso) — Regra: "Colocar junto o que muda junto"[cite: 10]
- **Slide 51:** *Inappropriate Intimacy* (Intimidade Inapropriada) — Violação do Encapsulamento[cite: 10, 11]
- **Slide 52:** *Incomplete Library Class* (Classe de Biblioteca Incompleta) — Quando uma biblioteca não oferece uma operação necessária
- **Slide 53:** *Message Chains* (Cadeias de Mensagens) e *Middle Man* (Intermediário) — O equilíbrio entre acoplamento e delegação[cite: 11]
- **Slide 54:** Resumo dos 23 Odores e das 5 categorias[cite: 3, 11]

### Ligação entre odores e técnicas de refatoração

As técnicas abaixo são possibilidades de tratamento, e não receitas universais. Antes de aplicá-las, é necessário confirmar o odor no contexto do projeto e preservar o comportamento observável por meio de testes.

| Categoria | Odor | Principais refatorações relacionadas |
|---|---|---|
| Bloaters | *Long Method* | *Extract Method*, *Replace Temp with Query*, *Replace Method with Method Object* |
| Bloaters | *Large Class* | *Extract Class*, *Extract Subclass*, *Extract Interface* |
| Bloaters | *Primitive Obsession* | *Replace Data Value with Object*, *Replace Type Code with Class*, *Replace Type Code with Subclasses/State/Strategy* |
| Bloaters | *Long Parameter List* | *Introduce Parameter Object*, *Preserve Whole Object*, *Replace Parameter with Method Call* |
| Bloaters | *Data Clumps* | *Extract Class*, *Introduce Parameter Object*, *Preserve Whole Object* |
| Object-Orientation Abusers | *Switch Statements* | *Replace Conditional with Polymorphism*, *Replace Type Code with Subclasses/State/Strategy*, *Replace Parameter with Explicit Methods* |
| Object-Orientation Abusers | *Temporary Field* | *Extract Class*, *Replace Method with Method Object*, *Introduce Null Object* |
| Object-Orientation Abusers | *Refused Bequest* | *Replace Inheritance with Delegation*, *Push Down Method*, *Push Down Field* |
| Object-Orientation Abusers | *Alternative Classes with Different Interfaces* | *Rename Method*, *Move Method*, *Extract Superclass* |
| Change Preventers | *Divergent Change* | *Extract Class*, *Extract Superclass*, *Extract Subclass* |
| Change Preventers | *Shotgun Surgery* | *Move Method*, *Move Field*, *Inline Class* |
| Change Preventers | *Parallel Inheritance Hierarchies* | *Move Method*, *Move Field* |
| Dispensables | *Comments* | *Extract Method*, *Rename Method*, *Introduce Assertion* |
| Dispensables | *Duplicate Code* | *Extract Method*, *Pull Up Method*, *Form Template Method*, *Substitute Algorithm* |
| Dispensables | *Lazy Class* | *Inline Class*, *Collapse Hierarchy* |
| Dispensables | *Data Class* | *Encapsulate Field*, *Encapsulate Collection*, *Move Method*, *Extract Method* |
| Dispensables | *Dead Code* | *Inline Class*, *Collapse Hierarchy*, *Remove Parameter* |
| Dispensables | *Speculative Generality* | *Collapse Hierarchy*, *Inline Class*, *Remove Parameter* |
| Couplers | *Feature Envy* | *Move Method*, *Extract Method* |
| Couplers | *Inappropriate Intimacy* | *Move Method*, *Move Field*, *Encapsulate Field*, *Change Bidirectional Association to Unidirectional* |
| Couplers | *Incomplete Library Class* | *Introduce Foreign Method*, *Introduce Local Extension* |
| Couplers | *Message Chains* | *Hide Delegate* |
| Couplers | *Middle Man* | *Remove Middle Man*, *Inline Method*, *Replace Delegation with Inheritance* |

---

## 🛠️ PARTE 4: Refatoração, Ferramentas e Boas Práticas (Fechamento) (~12 a 15 Slides)
**Objetivo:** Apresentar as soluções, a técnica de refatoração, o ecossistema de ferramentas automatizadas e a conclusão do estudo[cite: 2, 11].

- **Slide 55:** Definição Formal de Refatoração (Modificar a estrutura interna mantendo o comportamento externo)[cite: 2]
- **Slide 56:** O Processo Incremental: Pequenas alterações acompanhadas de testes[cite: 2]
- **Slide 57:** O Papel Crucial dos Testes Automatizados na Refatoração[cite: 2]
- **Slide 58:** Quando Refatorar vs. Quando Reescrever do Zero[cite: 2]
- **Slide 59:** Principais Técnicas de Refatoração:
  - Extract Method (Extrair Método)[cite: 3]
  - Extract Class (Extrair Classe)[cite: 4]
  - Replace Conditional with Polymorphism (Substituir Condicional por Polimorfismo)[cite: 5, 6]
- **Slide 60:** Ferramentas Automatizadas de Análise Estática de Código (IDE Linters, SonarQube, PMD, ESLint)
- **Slide 61:** Refatoração Automatizada nas IDEs (VS Code, IntelliJ, Eclipse)
- **Slide 62:** Boas Práticas no Ciclo de Desenvolvimento (Code Review, Pair Programming, TDD)
- **Slide 63:** Conclusão: "Nenhuma técnica de refatoração é universal"[cite: 11]
- **Slide 64:** Checklist do Desenvolvedor Limpo
- **Slide 65:** Referências Bibliográficas (Fowler, Sommerville, Refactoring.Guru, Cagnini, Manzano)[cite: 12]
- **Slide 66:** Pergunta Final / Espaço para Dúvidas e Discussão
