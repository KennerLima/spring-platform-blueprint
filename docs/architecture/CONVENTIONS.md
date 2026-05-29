# Convencoes Arquiteturais e de Nomenclatura

## Estrutura de modulos

- Cada modulo da plataforma comeca com prefixo `platform-`.
- O parent POM na raiz e a fonte unica para versoes e plugins.
- Dependencias entre modulos devem respeitar Clean Architecture.

## Convencoes de pacotes

- Base de pacote: `com.kenner.platform.<modulo>`.
- Nomes de pacotes sempre em ingles, minusculo e sem abreviacoes ambiguas.
- Nao misturar termos de dominio e infraestrutura no mesmo pacote.

## Convencoes de codigo

- Identificadores de codigo em ingles.
- Comentarios e documentacao em portugues claro.
- Value Objects e Commands preferencialmente com `record` no Java 21.
- Evitar heranca por padrao; priorizar composicao.

## Convencoes de build

- Java 21 e obrigatorio.
- Maven 3.9.0+ e obrigatorio.
- CI deve executar `mvn -B verify` no workspace raiz.
- Regras de convergencia e dependencia circular devem falhar o build.

## Convencoes de governanca

- `main` protegida com PR obrigatorio.
- Workflow de CI obrigatorio para merge.
- Toda decisao arquitetural nao obvia deve virar ADR em `docs/architecture`.
