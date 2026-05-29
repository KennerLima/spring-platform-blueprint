---
mode: 'ask'
description: 'Análise arquitetural completa de um módulo antes da implementação'
---

# Análise Arquitetural — ${input:module_name:nome do módulo (ex: platform-domain)}

Antes de qualquer implementação, conduza uma análise arquitetural profunda seguindo esta estrutura.

**Contexto do projeto:** plataforma de commons libs Java 21 + Spring Boot para ambiente enterprise/fintech.
**Regra absoluta:** o desenvolvedor implementa tudo — você analisa, questiona e orienta.

---

## 1. Objetivo Arquitetural

Explique com precisão:
- Qual problema arquitetural real esse módulo resolve?
- Por que ele deve existir como módulo separado?
- Qual dor ele elimina no ecossistema de projetos?
- Quais sintomas no código indicam que esse módulo é necessário?
- O que acontece se ele **não existir**?

## 2. Responsabilidades e Boundaries

Defina com clareza:
- O que **pertence** a este módulo (com justificativa)
- O que **não pertence** (com justificativa)
- Quais responsabilidades devem ser explicitamente proibidas
- Onde estão os limites com outros módulos da plataforma

## 3. Relação com SOLID

Analise cada princípio:
- **S** — Como a responsabilidade única se aplica aqui?
- **O** — Quais pontos de extensão são necessários?
- **L** — Onde herança seria um erro? Qual contrato garante substituição?
- **I** — Quais interfaces grandes precisam ser quebradas?
- **D** — Quais dependências de alto nível este módulo NÃO pode ter?

Mostre os anti-patterns SOLID específicos para este módulo.

## 4. Relação com DDD

Analise o impacto em:
- Aggregates e suas invariants
- Entities e identidade
- Value Objects e imutabilidade
- Domain Events e side effects
- Domain Services
- Bounded Contexts — este módulo cruza fronteiras?
- Ubiquitous Language — esse módulo introduz linguagem técnica no domínio?

## 5. Relação com Clean Architecture

Mapeie explicitamente:
- Em qual camada(s) este módulo opera?
- Quais dependências são **permitidas**?
- Quais dependências são **proibidas**?
- Como evitar vazamento de infraestrutura?
- Como garantir que a regra de dependência (inward only) é respeitada?

## 6. Estrutura de Pacotes Ideal

Proponha a estrutura de pacotes com justificativa para cada decisão.

Inclua:
- Interfaces/contratos necessários
- Onde ficam as implementações
- Onde ficam os adapters
- Como organizar para facilitar extensão sem modificação

## 7. Anti-Patterns — Análise Profunda

Liste os 5 erros mais comuns neste tipo de módulo, com:
- O que é o anti-pattern
- Por que parece certo inicialmente
- O que quebra no médio/longo prazo
- Como reconhecer antes que seja tarde

## 8. Trade-offs Arquiteturais

Seja honesto sobre:
- O que este módulo simplifica
- O que ele torna mais complexo
- Impacto em debugging e observabilidade
- Impacto em onboarding de novos devs
- Impacto em testes
- Impacto em evolução futura
- Custo de manutenção

## 9. MVP Arquitetural

Responda:
- Qual é o menor conjunto válido para começar?
- O que implementar **primeiro**?
- O que deve esperar até a plataforma ter mais maturidade?
- Qual abstração é prematura neste momento?

## 10. Enforcement com ArchUnit

Liste as regras arquiteturais que **precisam** ser automatizadas para este módulo, com exemplos de como escrever cada uma com ArchUnit.

## 11. Observabilidade

Defina:
- Quais logs são necessários (nível, contexto, o que nunca logar)
- Quais métricas fazem sentido
- Quais spans de tracing são relevantes
- Como debugar problemas neste módulo em produção

## 12. Estratégia de Testes

Defina:
- O que testar com testes unitários puros
- O que requer testes de integração (Testcontainers)
- O que requer testes arquiteturais (ArchUnit)
- O que **não** vale a pena mockar
- Qual cobertura é suficiente vs overengineering

## 13. Fluxo Real de Uso

Descreva um fluxo ponta a ponta realista, enterprise, mostrando:
- Como um time usaria este módulo no dia a dia
- Interação com outros módulos da plataforma
- Impacto em microserviços vs monólito modular

## 14. Checklist de Maturidade

Crie um checklist com:
- ✅ Sinais de implementação madura e saudável
- ❌ Sinais de dívida técnica ou abstração ruim
- ⚠️ Sinais de alerta para revisão arquitetural

## 15. Alternativas

Antes de implementar, avalie:
- Quais alternativas existem para resolver o mesmo problema?
- Quando **não** usar este módulo?
- Quando uma solução mais simples (sem módulo) seria melhor?

---

## Código — Somente ao Final

Após toda a análise, mostre apenas:
- Os contratos/interfaces principais (não implementações)
- A estrutura de pacotes
- Um exemplo mínimo de uso correto
- Um exemplo de uso **incorreto** com explicação do problema

Mantenha o código ilustrativo, não prescritivo.
