---
mode: 'ask'
description: 'Revisão arquitetural de código já implementado'
---

# Revisão Arquitetural — ${input:context:descreva o que foi implementado}

Conduza uma revisão arquitetural crítica do código/estrutura apresentado.

**Lembrete:** O objetivo não é reescrever. É identificar riscos, violações e melhorias que o desenvolvedor deve implementar.

---

## 1. Primeira impressão — Leitura arquitetural

Antes de detalhar, responda:
- O que este código está tentando fazer?
- Está na camada correta?
- A intenção é clara sem precisar ler a implementação?

## 2. Violações de Clean Architecture

Verifique explicitamente:
- [ ] O domínio tem dependência de Spring, JPA, Kafka ou qualquer framework?
- [ ] A camada de application acessa infraestrutura diretamente?
- [ ] Há lógica de negócio em controllers ou adapters?
- [ ] Há acoplamento entre módulos que não deveriam se conhecer?
- [ ] Alguma annotation de infraestrutura está em entidade de domínio?

Para cada violação encontrada:
- Explique **por que** é um problema
- Explique o impacto de longo prazo
- Sugira a direção correta (sem implementar por ele)

## 3. Violações de SOLID

Analise cada princípio:
- **SRP:** Alguma classe tem mais de uma razão para mudar?
- **OCP:** Adicionar comportamento novo exige modificar código existente?
- **LSP:** Há herança que força comportamento inválido em subtipos?
- **ISP:** Alguma interface força implementação de métodos irrelevantes?
- **DIP:** Algum componente de alto nível depende de detalhe de implementação?

## 4. Violações de DDD

Verifique:
- [ ] Aggregates expõem estado interno diretamente?
- [ ] Invariants de negócio estão fora do domínio?
- [ ] Domain Events são gerados fora do aggregate?
- [ ] Value Objects têm identidade quando não deveriam?
- [ ] O código usa linguagem técnica onde deveria usar linguagem do domínio?

## 5. Anti-patterns identificados

Liste cada anti-pattern encontrado:
- Nome do anti-pattern
- Onde ocorre no código
- Por que é problemático
- Consequência se não corrigido

## 6. Acoplamento e Coesão

- Qual é o nível de acoplamento afferente (quem depende deste componente)?
- Qual é o nível de acoplamento eferente (do que este componente depende)?
- A coesão está alta? As responsabilidades são relacionadas?
- Há algum "God Class" ou "Blob"?

## 7. Observabilidade e Debugging

- Este código é rastreável em produção?
- Os erros têm contexto suficiente para debugging?
- Há logs onde são necessários?
- Há algum "swallow exception" ou falha silenciosa?

## 8. Testabilidade

- Este código é testável de forma isolada?
- Há acoplamento que dificulta mock/stub?
- Há lógica misturada com I/O que impede teste unitário?

## 9. Riscos identificados

Liste riscos em ordem de severidade:
- 🔴 **Crítico** — viola fundamentos, precisa corrigir agora
- 🟡 **Importante** — cria dívida técnica relevante
- 🔵 **Melhoria** — não é urgente mas vale endereçar

## 10. Perguntas para o desenvolvedor

Formule perguntas que forcem reflexão arquitetural:
- Sobre decisões de design tomadas
- Sobre trade-offs que podem não ter sido considerados
- Sobre evolução futura desta implementação

## 11. Próximos passos sugeridos

Liste ações concretas em ordem de prioridade, sem implementar por ele:
1. O que corrigir primeiro (e por quê)
2. O que refatorar no médio prazo
3. O que monitorar para evitar degradação futura

---

**Lembrete final:** Não reescreva o código. Aponte o caminho. O aprendizado vem da implementação.
