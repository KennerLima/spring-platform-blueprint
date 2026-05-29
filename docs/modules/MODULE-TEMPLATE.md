# platform-xxx — Nome do Módulo

## Objetivo

> Uma frase clara descrevendo qual problema este módulo resolve.

---

## Problema que resolve

Descreva a dor arquitetural que justifica a existência deste módulo.

**Sem este módulo, o que acontece?**
- Problema A se repete em cada projeto
- Padrão B é implementado de forma diferente por cada time
- Inconsistência C aparece em produção

---

## Responsabilidades

### ✅ Pertence a este módulo

- Responsabilidade 1
- Responsabilidade 2

### ❌ Não pertence a este módulo

- Responsabilidade X → vai em `platform-yyy`
- Responsabilidade Y → é responsabilidade do domínio do projeto

---

## Dependências

```
platform-xxx
├── depende de: platform-domain (contratos)
├── depende de: platform-exceptions (erros)
└── NÃO depende de: Spring Web, JPA, mensageria
```

---

## Estrutura de pacotes

```
com.company.platform.xxx/
├── domain/
│   └── (contratos puros, zero framework)
├── application/
│   └── (ports, use case abstractions)
├── infrastructure/
│   └── (implementações concretas)
└── config/
    └── (Spring AutoConfiguration)
```

---

## Uso rápido

```java
// Exemplo mínimo de uso correto
```

---

## Anti-patterns — O que evitar

### ❌ Anti-pattern 1 — Nome

```java
// Exemplo do que NÃO fazer
```

**Por que é ruim:** explicação

---

## Regras ArchUnit

Este módulo possui as seguintes regras arquiteturais automatizadas:

| Regra | O que valida | Severidade |
|-------|-------------|------------|
| `domainHasNoSpring` | Domínio não importa Spring | 🔴 Crítico |

---

## Decisões arquiteturais

- [ADR-001 — Decisão relevante](../architecture/ADR-001.md)

---

## Changelog

| Versão | Mudança |
|--------|---------|
| 1.0.0 | Criação inicial |
