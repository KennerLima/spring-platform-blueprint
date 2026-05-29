# Guia de Branch Protection para main

## Objetivo

Impedir que alteracoes quebrem a arquitetura silenciosamente e garantir fluxo de PR.

## Configuracao recomendada no GitHub

1. Acesse Settings > Branches > Add rule.
2. Branch name pattern: `main`.
3. Habilite `Require a pull request before merging`.
4. Habilite `Require status checks to pass before merging`.
5. Marque o check da pipeline de CI (`CI - verify`).
6. Habilite `Require branches to be up to date before merging`.
7. Opcional recomendado: `Require conversation resolution before merging`.

## Resultado esperado

- Ninguem faz push direto em `main` sem PR.
- Merges so ocorrem quando `mvn verify` passa.
- A arquitetura ganha trilha auditavel de revisao.
