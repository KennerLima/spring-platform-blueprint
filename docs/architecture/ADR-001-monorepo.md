# ADR-001 - Monorepo para a plataforma de commons libs

**Data:** 2026-05-29  
**Status:** Aceita  
**Módulo:** plataforma (workspace raiz)  
**Autor:** equipe de plataforma

---

## Contexto

A plataforma sera composta por multiplos modulos compartilhados que evoluem em conjunto.

- Sem um repositorio unico, o versionamento entre modulos tende a divergir.
- A validacao arquitetural automatizada (ArchUnit + Maven reactor) precisa executar no conjunto completo.
- O onboarding de novos contribuidores fica mais caro quando cada modulo vive isolado.

---

## Decisao

Adotar monorepo Maven multi-modulo com um parent POM unico na raiz.

> Decidimos usar monorepo para garantir consistencia de versoes, visibilidade arquitetural e governanca centralizada desde o inicio.

---

## Consequencias

### Positivas
- Build unica para validar compatibilidade entre modulos.
- Governanca centralizada de Java, BOM, plugins e regras de qualidade.
- Evolucao sincronizada entre modulos de dominio, aplicacao e excecoes.

### Negativas
- Build inicial pode crescer com o numero de modulos.
- Mudancas em modulo central podem afetar o tempo de CI do workspace inteiro.

### Neutras
- O ciclo de release exige estrategia clara para publicacao seletiva de artefatos.

---

## Alternativas Consideradas

| Alternativa | Por que foi descartada |
|-------------|------------------------|
| Multirepo por modulo | Aumenta custo de governanca e risco de drift de versao |
| Monolito unico sem modulos Maven | Dificulta isolamento de responsabilidades e evolucao incremental |

---

## Enforcement

- [ ] Regra ArchUnit criada em `platform-architecture-rules`
- [ ] Teste de integracao cobrindo o contrato
- [x] Documentado no README do modulo

---

## Referencias

- Domain-Driven Design (Eric Evans)
- Building Evolutionary Architectures (Ford, Parsons, Kua)
- Software Architecture: The Hard Parts (Ford, Richards et al.)
