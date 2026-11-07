# Checklist de produção

Minimalista (80/20). `[x]` feito, `[ ]` lacuna, `n/a` não se aplica. Não há LLM no fluxo: os itens de IA ficam de fora.

## 1. Problema e requisitos

- [x] Problema, usuário e sucesso: sugerir o aporte mensal em FIIs rumo à `rendaAlvo` ([README](README.md)).
- n/a Orçamento de latência e custo: CLI local; Yahoo Finance não cobra nem pede chave.
- [x] Dados e aprovação humana: `carteira.json` fora do git; a ferramenta só sugere, a compra é do usuário.

## 2. Contexto e ferramentas

- [x] Só dependências necessárias: nenhuma em runtime (`fetch` nativo).

## 3. Evals e proteções

- [x] Testes representativos: `test/carteira.test.ts` (`node --test`).
- [x] Sem vazamento: `carteira.json` no `.gitignore`.
- [x] Fallback: ticker inexistente, HTTP com erro ou cotação ausente falham com erro que nomeia o ticker (`src/yahoo.ts`).

## 4. Confiabilidade e observabilidade

- [x] Entrada validada: `carteira.json` e o valor do aporte (`src/main.ts`); resposta do Yahoo checada antes do uso.
- [x] Timeout: 15 s por requisição ao Yahoo (`src/yahoo.ts`).
- [ ] Retry: uma falha transitória do Yahoo aborta a execução; avaliar 1 retry com backoff só se acontecer na prática.
- [ ] Falha real vira teste: resposta do Yahoo que quebrar o cálculo entra como fixture em `test/` com o fix.

## 5. Custo e desempenho

- n/a Baseline, cache e roteamento: poucas requisições por execução mensal.
