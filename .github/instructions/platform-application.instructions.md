# platform-application — Contexto e Restrições

## Regras absolutas deste módulo

---

## O que é este módulo

Orquestra casos de uso. Faz a ponte entre o mundo externo e o domínio.

Não contém regra de negócio. Não contém infraestrutura.

---

## Dependências permitidas

```xml
<dependency>
    <groupId>com.company</groupId>
    <artifactId>platform-domain</artifactId>
</dependency>
<dependency>
    <groupId>com.company</groupId>
    <artifactId>platform-exceptions</artifactId>
</dependency>
```

**Spring pode aparecer aqui apenas como `@Transactional` e similares — nunca para lógica de negócio.**

---

## O que pertence aqui

```
UseCase<I, O>       → interface do caso de uso
Command             → input de escrita (record imutável)
Query               → input de leitura (record imutável)  
Port (interfaces)   → contratos para infraestrutura implementar
ApplicationService  → orquestração quando necessário (sem regra de negócio)
```

---

## O que NÃO pertence aqui

```
❌ Regras de negócio — ficam no domain
❌ Queries SQL, JPQL — ficam em platform-jpa
❌ Publicação de eventos Kafka — fica em platform-messaging
❌ Controllers, endpoints — ficam em platform-web
❌ @RestController, @RequestMapping
```

---

## Padrão obrigatório de Use Case

```java
// Interface — define o contrato
public interface UseCase<I, O> {
    O execute(I input);
}

// Command → sempre record
public record CreateCustomerCommand(String name, String email) {}

// Use Case implementation — somente orquestração
public class CreateCustomerUseCase implements UseCase<CreateCustomerCommand, CustomerId> {
    
    // Depende de INTERFACES (ports), nunca de implementações
    private final CustomerRepository customerRepository;        // port
    private final DomainEventPublisher eventPublisher;         // port
    
    @Override
    public CustomerId execute(CreateCustomerCommand command) {
        // 1. Cria o aggregate (regra de negócio no domínio)
        // 2. Persiste via port
        // 3. Publica evento via port
        // NÃO contém lógica de negócio aqui
    }
}
```

---

## Sinais de violação — revisar imediatamente

- Lógica de negócio no Use Case (if/else de regra de domínio)
- Importação de `@Repository`, `@Entity`
- Acesso direto a JPA EntityManager
- Use Case retornando entidade JPA ao invés de DTO/Value Object
- Port definido como classe concreta
