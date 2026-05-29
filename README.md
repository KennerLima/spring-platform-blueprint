# Platform Engineering Workspace

Workspace de aprendizado e implementação da plataforma de commons libs Java 21 + Spring.

---

## Filosofia deste workspace

**Você implementa tudo.** O Copilot analisa, questiona, revisa e orienta — nunca implementa por você.

O objetivo não é ter o código mais rápido.  
O objetivo é entender profundamente cada decisão arquitetural.

---

## Fluxo de trabalho

### 1. Antes de implementar qualquer módulo

```
/plan-module → análise arquitetural completa (15 dimensões)
```

Use este prompt para entender profundamente o módulo antes de escrever uma linha.

### 2. Quando quiser aprender um conceito

```
/learn → modo socrático — você constrói o entendimento por perguntas
```

### 3. Durante ou após implementar

```
/review-code     → revisão arquitetural crítica
/review-structure → validação de pacotes e dependências
```

### 4. Para garantir que arquitetura não degrada

```
/archunit-rules → gera regras de enforcement automatizado
```

---

## Ordem de implementação (fases)

> Não pule fases. A sequência existe por motivo arquitetural.

| Fase | O que implementar | Por que primeiro |
|------|-------------------|-----------------|
| **0** | Convenções, estrutura Maven, ADR inicial | Base que tudo usa |
| **1** | `platform-domain`, `platform-application`, `platform-exceptions` | Núcleo sem dependências externas |
| **2** | `platform-architecture-rules` (ArchUnit) | Impede degradação desde o início |
| **3** | `platform-observability` | Sem isso, debugging é cego |
| **4** | `platform-web`, `platform-validation` | APIs só após núcleo sólido |
| **5** | `platform-jpa` | Persistência após contratos definidos |
| **6** | `platform-events`, `platform-messaging` | Eventos após domínio estável |
| **7** | `platform-security` | Auth após fluxos definidos |
| **8** | `platform-starters` | Produtividade após maturidade |
| **9** | Annotation processors, OpenRewrite, CLI | Só com plataforma madura |

---

## Regras que nunca mudam

```
platform-domain     →  zero Spring, zero JPA, zero HTTP
platform-application → depende apenas de platform-domain  
Domínio             →  nunca conhece infraestrutura
Abstração           →  nasce da dor real, nunca antecipada
```

---

## Documentação

```
docs/
├── architecture/       → ADRs (decisões arquiteturais)
│   └── ADR-TEMPLATE.md
└── modules/            → documentação de cada módulo
    └── MODULE-TEMPLATE.md
```

### Convenções e decisões iniciais

- Convenções arquiteturais e de nomenclatura: `docs/architecture/CONVENTIONS.md`
- ADR inicial do monorepo: `docs/architecture/ADR-001-monorepo.md`
- Guia de branch protection para `main`: `docs/architecture/BRANCH-PROTECTION.md`

**Para cada módulo implementado:**
1. Crie `docs/modules/platform-xxx.md` (baseado no template)
2. Crie um ADR para cada decisão não óbvia

---

## Prompts disponíveis

| Prompt | Quando usar |
|--------|-------------|
| `/plan-module` | Antes de qualquer implementação |
| `/learn` | Para aprender um conceito profundamente |
| `/review-code` | Para revisar código implementado |
| `/review-structure` | Para validar estrutura de pacotes |
| `/archunit-rules` | Para criar regras de enforcement |

---

## Fontes de aprendizado

### Livros referência

- **Clean Architecture** — Robert C. Martin
- **Domain-Driven Design** — Eric Evans
- **Implementing DDD** — Vaughn Vernon
- **Building Evolutionary Architectures** — Ford, Parsons, Kua
- **Software Architecture: The Hard Parts** — Ford, Richards et al.

### Tecnologias para dominar

- [Spring Boot](https://spring.io/projects/spring-boot)
- [Spring Modulith](https://spring.io/projects/spring-modulith)
- [ArchUnit](https://www.archunit.org)
- [Micrometer](https://micrometer.io)
- [OpenTelemetry](https://opentelemetry.io)
- [Testcontainers](https://testcontainers.com)
- [Resilience4j](https://resilience4j.readme.io)
- [MapStruct](https://mapstruct.org)
- [OpenRewrite](https://openrewrite.org)

---

## Pergunta que sempre vale fazer antes de implementar

> *"Se eu remover esta abstração daqui a 2 anos, o que quebra?"*

Se a resposta for "nada importante" — talvez a abstração não deva existir.
