---
mode: 'ask'
description: 'Valida estrutura de pacotes e dependências entre módulos'
---

# Validação de Estrutura — ${input:module:módulo ou estrutura a validar}

---

## O que será validado

### 1. Estrutura de pacotes

Verifique se os pacotes seguem a convenção:

```
com.company.platform.<module>
├── domain/          → entidades, VOs, eventos, specs (zero frameworks)
├── application/     → use cases, commands, queries, ports
├── infrastructure/  → implementações de ports, adapters
└── config/          → Spring configuration (somente aqui)
```

Identifique:
- Pacotes em camada errada
- Classes com responsabilidade fora do pacote
- Nomes que violam ubiquitous language

### 2. Grafo de dependências

Para cada dependência declarada no módulo:

- É realmente necessária?
- Está no escopo correto (compile, runtime, test)?
- Cria acoplamento desnecessário?
- Viola a regra de dependência das camadas?

**Dependências proibidas por módulo:**

| Módulo | NÃO pode depender de |
|--------|----------------------|
| platform-domain | spring-*, jpa, kafka, http |
| platform-application | spring-web, jpa, kafka |
| platform-domain | platform-application |
| qualquer módulo | platform-starters (em compile) |

### 3. Interfaces e contratos

- Todo port tem sua interface no lado correto (application/domain)?
- Implementações estão apenas em infrastructure?
- Há implementações "vazando" para camadas superiores?

### 4. Nomenclatura

Valide naming conventions:
- [ ] Use Cases: `VerbNounUseCase` (ex: `CreateCustomerUseCase`)
- [ ] Commands: `VerbNounCommand` (ex: `CreateCustomerCommand`) — deve ser `record`
- [ ] Queries: `FindNounByXQuery` (ex: `FindCustomerByIdQuery`) — deve ser `record`
- [ ] Events: `NounVerbedEvent` (ex: `CustomerCreatedEvent`) — deve ser imutável
- [ ] Repositories: `NounRepository` — interface apenas, sem `Impl` no nome
- [ ] Adapters: `NounTechnologyAdapter` (ex: `CustomerJpaAdapter`)

### 5. Checklist final

- [ ] Módulo tem `README.md` com objetivo claro?
- [ ] Módulo tem testes arquiteturais (ArchUnit)?
- [ ] Módulo tem testes unitários do domínio sem Spring context?
- [ ] Módulo não tem dependências circulares?
- [ ] Módulo expõe apenas o que precisa (mínimo público)?

---

## Resultado esperado

Para cada problema encontrado:
1. Localização exata
2. Qual regra viola
3. Por que é um problema
4. Direção da correção (sem implementar)
