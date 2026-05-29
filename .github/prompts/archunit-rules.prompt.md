---
mode: 'ask'
description: 'Gera regras ArchUnit para enforcement arquitetural do módulo'
---

# Enforcement Arquitetural — ArchUnit

Módulo/contexto: ${input:context:descreva o módulo ou regra a validar}

---

## O que precisa ser gerado

Com base no contexto fornecido, crie regras ArchUnit que:

1. **Validem isolamento do domínio**
   - Domínio não depende de Spring, JPA, HTTP, mensageria
   - Aggregates não usam annotations de infraestrutura

2. **Validem separação de camadas**
   - Application não acessa Web/Infrastructure diretamente
   - Domain não conhece Application
   - Controllers não contêm lógica de negócio

3. **Validem naming conventions**
   - Use Cases terminam com `UseCase`
   - Commands terminam com `Command`
   - Events terminam com `Event`
   - Repositories terminam com `Repository`

4. **Validem estrutura de pacotes**
   - Cada camada no pacote correto
   - Sem dependências circulares entre módulos

5. **Validem contratos obrigatórios**
   - Todo Use Case implementa a interface correta
   - Todo Command é um record (imutável)
   - Todo Domain Event é imutável

---

## Formato esperado

Para cada regra:

**Nome da regra:** (descritivo)
**Por que existe:** (justificativa arquitetural)
**O que detecta:** (anti-pattern específico)
**Código ArchUnit:** (implementação)
**Onde adicionar:** (classe de teste e módulo)

---

## Regras base já definidas para a plataforma

```java
// Exemplo de estrutura esperada — adapte para o contexto
@AnalyzeClasses(packages = "com.company", importOptions = ImportOption.DoNotIncludeTests.class)
public class PlatformArchitectureTest {

    // Suas regras aqui
}
```

---

## Após gerar as regras

Explique:
- Quais dessas regras são **críticas** (falha = build quebra)
- Quais são **avisos** (falha = warning)
- Como evoluir essas regras conforme a plataforma cresce
- Quais regras adicionais devem ser criadas quando novos módulos forem adicionados
