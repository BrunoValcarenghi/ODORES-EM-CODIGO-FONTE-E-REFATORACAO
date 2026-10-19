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
**Objetivo:** Detalhar os 21 odores de código do documento, organizados pelas 5 categorias, apresentando definições e diagramas/código para cada um[cite: 3, 11].

### Categoria 1: Bloaters (Inchaço) (~8 slides)[cite: 3]
- **Slide 21:** Categoria Bloaters: O que é e como se forma[cite: 3]
- **Slide 22:** *Long Method* (Método Longo) — Definição e indícios (uso de comentários internos)[cite: 3]
- **Slide 23:** *Large Class* (Classe Grande) — Excesso de campos e responsabilidades[cite: 3, 4]
- **Slide 24:** *Primitive Obsession* (Obsessão Primitiva) — Uso exagerado de tipos primitivos para dados do domínio[cite: 4]
- **Slide 25:** *Long Parameter List*
