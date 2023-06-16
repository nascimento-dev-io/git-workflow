## Workflow GitFlow

O Gitflow é um modelo alternativo de ramificação do Git que envolve o uso de ramificações de recursos e várias ramificações primárias.

Algumas informações importantes sobre o Gitflow são:

- O fluxo de trabalho é ótimo para um fluxo de trabalho de software baseado em versão.
- O Gitflow oferece um canal dedicado para hotfixes para produção.

### O fluxo geral do Gitflow é:

1. Uma ramificação `develop` é criada a partir `main`.
2. Uma ramificação `release` é criada a partir `develop`.
3. `Feature` branchs são criados a partir `develop`
4. Quando a `feature` está completo, ele é mesclado na ramificação `develop`.
5. Quando a ramificação `release` é concluída, ela é mesclada na `develop` e `main`.
6. Se um problema `main` for detectado, uma ramificação `hotfix` será criada a partir `main`.
7. Uma vez `hotfix` concluído, ele é mesclado a ambos `develop` e `main`.

> Maiores detalhes [Fluxo de trabalho do Gitflow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow)
