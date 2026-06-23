# Skills

Este repositorio mantem conjuntos de skills para modelos de linguagem. Cada
diretorio de primeiro nivel representa um conjunto independente de skills, com
objetivo, fluxo e limites proprios.

Hoje o repositorio contem:

- [Web01](Web01/README.md): metodologia para conduzir mudancas em projetos web
  por tarefas, fases, validacoes e consolidacao de conhecimento permanente.

## Como usar um conjunto de skills

Para disponibilizar um conjunto ao modelo, crie uma juncao de diretorio dentro
do diretorio global de skills do modelo apontando para o diretorio do conjunto
neste repositorio.

No Windows, use `mklink /J` em um Prompt de Comando com permissao adequada:

```cmd
mklink /J "<diretorio-global-de-skills-do-modelo>\<nome-do-conjunto>" "<diretorio-do-repositorio-das-skills>\<nome-do-conjunto>"
```

Exemplo:

```cmd
mklink /J "C:\Users\<usuario>\.codex\skills\Web01" "C:\Users\<usuario>\Projetos\Skills\Web01"
```

Para usar mais de um conjunto, crie uma juncao separada para cada diretorio de
conjunto:

```cmd
mklink /J "<diretorio-global-de-skills-do-modelo>\Web01" "<diretorio-do-repositorio-das-skills>\Web01"
mklink /J "<diretorio-global-de-skills-do-modelo>\<OutroConjunto>" "<diretorio-do-repositorio-das-skills>\<OutroConjunto>"
```

O primeiro caminho e o link que sera criado no diretorio global de skills do
modelo. O segundo caminho e o diretorio real mantido neste repositorio.

## Contribuicoes

Pull requests podem ser propostos. Para facilitar a analise, descreva com
detalhe:

- qual conjunto de skills foi alterado;
- qual problema a mudanca resolve;
- quais arquivos ou fluxos foram impactados;
- quais comportamentos ou limites foram adicionados, removidos ou ajustados.

As contribuicoes serao avaliadas desde que preservem o objetivo do conjunto de
skills alterado. Se a proposta mudar demais a finalidade, a metodologia ou o
publico de um conjunto existente, o caminho recomendado e criar um novo conjunto
de skills em outro diretorio.
