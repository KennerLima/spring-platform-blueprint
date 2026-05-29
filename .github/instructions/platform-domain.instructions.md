# platform-domain — Contexto e Restrições

## Regras absolutas deste módulo

Este arquivo serve como contexto permanente para o Copilot ao trabalhar em `platform-domain`.

---

## O que é este módulo

O núcleo puro da plataforma. Contém os building blocks de DDD sem **nenhuma** dependência de framework.

É a camada mais interna. Nada externo entra aqui.

---

## Dependências permitidas

```xml
<!-- Apenas Java 21 puro -->
<!-- NENHUMA dependência de Spring, JPA, Jakarta EE, etc. -->
```

**Se você precisar importar algo de `org.springframework.*` aqui, a arquitetura está errada.**

---

## O que pertence aqui

```
Entity           → tem identidade, pode mudar estado
AggregateRoot    → raiz de consistência transacional
ValueObject      → imutável, sem identidade, definido por atributos
DomainEvent      → fato ocorrido no domínio, imutável
DomainException  → exceção que expressa violação de regra de negócio
Specification    → encapsula critério de seleção/validação
Result<T>        → Either pattern — Success ou Failure sem exceção
```

---

## O que NÃO pertence aqui

```
❌ @Entity, @Table, @Column — JPA fica em platform-jpa
❌ @Component, @Service, @Bean — Spring fica fora do domínio
❌ Use cases, commands — ficam em platform-application
❌ Qualquer lógica de persistência
❌ Qualquer lógica de serialização (Jackson, etc.)
❌ Qualquer lógica de HTTP
```

---

## Padrões obrigatórios com Java 21

```java
// Commands e Value Objects → records
public record CustomerId(UUID value) {
    public CustomerId {
        Objects.requireNonNull(value, "CustomerId cannot be null");
    }
}

// Domain Events → records imutáveis
public record CustomerCreatedEvent(
    CustomerId customerId,
    String name,
    Instant occurredAt
) implements DomainEvent {}

// Result Pattern → sealed interface
public sealed interface Result<T> permits Success, Failure {}
```

---

## Sinais de violação — revisar imediatamente

- Qualquer import de `org.springframework.*`
- Qualquer import de `jakarta.persistence.*`
- Qualquer import de `com.fasterxml.jackson.*`
- Qualquer classe mutável sendo usada como Value Object
- Domain Events sendo gerados fora do AggregateRoot
- Invariants sendo validadas fora da entidade
- Construtores públicos sem validação de invariants
