---
name: criar-tarefa
description: Conversar com o usuario para compreender, organizar, melhorar e delimitar uma intencao de mudanca antes de registra-la como tarefa proposta, rastreavel e pronta para planejamento. Usar quando o usuario solicitar nova capacidade, alteracao, correcao, refatoracao, investigacao, documentacao ou infraestrutura que ainda precise ser discutida, refinada e preparada para fases.
---

# Criar Tarefa

Compreender, lapidar e registrar uma mudanca desejada como tarefa proposta.
Antes de escrever qualquer arquivo, conduzir uma conversa curta para entender a
intencao, sugerir complementos uteis, apontar simplificacoes possiveis e chegar
com o usuario a uma proposta limpa para o Planejador.

## Principios

- Comecar em `AGENTS.md` e seguir somente links relevantes.
- Fazer poucas perguntas por rodada e evitar detalhes tecnicos prematuros.
- Definir um resultado observavel, nao uma lista de atividades.
- Organizar a ideia do usuario antes de pedir confirmacao.
- Ajudar o usuario a melhorar a ideia antes do registro, oferecendo sugestoes
  explicitas de complemento e simplificacao.
- Separar sugestoes de complemento, simplificacao e duvidas reais.
- Manter cada tarefa em diretorio proprio, com um arquivo central curto e navegavel.
- Nao escrever arquivos antes de confirmacao explicita para registrar a tarefa.
- Usar links explicativos para o conhecimento relacionado.
- Nao ler recursivamente o projeto ou a documentacao.

## Fluxo

### 1. Conversar sobre a intencao

Identificar progressivamente:

1. Qual problema ou necessidade motivou a solicitacao?
2. Qual resultado observavel indicara que ela foi atendida?
3. O que deve fazer parte desta tarefa?
4. O que deve ficar explicitamente fora?

Nao exigir respostas sobre implementacao. Registrar duvidas ainda relevantes como
decisoes pendentes.

Classificar a tarefa como:

- nova capacidade;
- alteracao de comportamento;
- correcao;
- refatoracao;
- investigacao;
- documentacao ou infraestrutura.

### 2. Consultar o contexto minimo

- Ler `AGENTS.md`.
- Seguir somente links relacionados a solicitacao.
- Identificar visao, dominios, recursos e decisoes relevantes.
- Nao inspecionar codigo-fonte por padrao.

Quando houver possivel impacto permanente, registrar a avaliacao arquitetural
como `Incerta` ou descrever a pendencia. Nao consolidar conhecimento, pois uma
proposta ainda nao representa o estado atual do sistema.

### 3. Ajudar a lapidar a tarefa

Antes de propor o registro, devolver ao usuario uma leitura consultiva da ideia.
Esta etapa e obrigatoria mesmo quando a ideia parecer clara.

Usar uma estrutura curta com:

- entendimento atual em poucas linhas;
- ideia organizada: problema, objetivo, resultado observavel, escopo e fora do
  escopo provaveis;
- sugestoes de complemento: algo util que pode estar faltando para atingir melhor
  o objetivo, como regras, estados, casos de erro, dados, permissoes, validacao
  ou impactos permanentes;
- sugestoes de simplificacao: forma menor, mais direta ou menos arriscada de
  obter o resultado esperado, incluindo separar etapas, reduzir escopo inicial ou
  adiar detalhes;
- separacoes recomendadas quando a solicitacao misturar mudancas independentes;
- duvidas que realmente mudem objetivo, resultado ou escopo.

Quando nao houver complemento ou simplificacao util, dizer isso explicitamente e
explicar em uma frase. Nao omitir a categoria.

Tratar sugestoes como convite, nao como decisao. O usuario pode aceitar, recusar
ou pedir ajustes. Perguntar qual caminho o usuario prefere antes de registrar a
tarefa. Continuar a conversa ate que objetivo, resultado e escopo estejam
suficientemente claros.

Nao criar arquivos nesta etapa.

### 4. Fechar a proposta candidata

Preparar um resumo curto contendo:

- titulo curto;
- tipo;
- problema ou motivacao;
- objetivo;
- resultado esperado;
- escopo;
- fora do escopo;
- expectativas iniciais de aceite;
- links para conhecimento relacionado;
- impacto permanente identificado;
- decisoes pendentes.

As expectativas iniciais de aceite devem descrever sinais observaveis de sucesso,
sem detalhar testes ou solucao tecnica. O Planejador refinara criterios e fases.

Se a solicitacao contiver mudancas independentes, propor separa-las antes de
registrar. Nao criar varias tarefas sem confirmacao.

### 5. Confirmar com o usuario

Apresentar a proposta candidata de forma compacta e perguntar se o usuario quer:

- ajustar a proposta;
- aceitar a proposta e registrar a tarefa;
- cancelar ou deixar para depois.

Criar a tarefa apenas depois de confirmacao explicita do usuario. Registrar
decisoes ainda abertas como pendencias; nao bloquear a criacao por detalhes que
pertencem ao planejamento.

### 6. Numerar e registrar

Usar esta estrutura:

```text
documentacao/
|-- tarefas.md
`-- tarefas/
    `-- NNN-titulo-curto/
        |-- tarefa.md
        `-- fases/
```

Regras de identificacao:

- usar numero sequencial com pelo menos tres digitos: `001`, `002`, `003`;
- determinar o proximo numero pelo maior identificador entre todos os diretorios
  e arquivos existentes em `documentacao/tarefas/`;
- nunca reutilizar, renumerar ou preencher lacunas antigas;
- usar titulo curto em minusculas, sem acentos e separado por hifens;
- manter o titulo legivel completo dentro de `tarefa.md`.

Exemplo: `documentacao/tarefas/003-avaliar-livros/tarefa.md`.

Criar ou atualizar `documentacao/tarefas.md` como indice curto. Manter nele
somente um resumo da finalidade da area e links explicativos para as tarefas.
Quando for a primeira tarefa, adicionar em `AGENTS.md` um link explicativo para o
indice. Nao listar todas as tarefas diretamente em `AGENTS.md`.

Registrar a nova tarefa com estado `Proposta` em `tarefa.md`:

```markdown
# T-003 - Avaliar livros

**Estado:** Proposta
**Tipo:** Nova capacidade

## Resumo
Problema, objetivo e resultado esperado em poucas linhas.

## Escopo
- O que pertence a tarefa.

## Fora do escopo
- O que nao pertence a tarefa.

## Expectativas de aceite
- Resultado observavel esperado.

## Conhecimento relacionado
- [Assunto](../conhecimento.md#assunto): motivo da relacao.

## Avaliacao arquitetural
Impacto permanente e atualizacoes possivelmente necessarias.

## Decisoes pendentes
- Decisoes ainda abertas, ou `Nenhuma`.

## Controle de fases
Nenhuma fase planejada ainda.

## Resumo final da tarefa
Aguardando encerramento.

### Fonte da verdade
Aguardando encerramento.
```

Adaptar secoes ao contexto, mas nao adicionar plano detalhado, fases ou validacao
da implementacao. A secao `Controle de fases` deve existir como
painel de acompanhamento e sera preenchida pelo Planejador. A secao `Resumo final
da tarefa` deve existir como marcador para uma sintese historica curta apos a
conclusao.

O estado geral da tarefa seguira este ciclo nas skills posteriores:

```text
Proposta -> Planejada -> Em desenvolvimento -> Em encerramento -> Concluida
```

Usar `Bloqueada` ou `Cancelada` quando necessario. Criar Tarefa define somente o
estado `Proposta`.

### 7. Verificar

- Confirmar que houve conversa antes de qualquer escrita.
- Confirmar que complementos e simplificacoes foram oferecidos ou explicitamente
  considerados desnecessarios.
- Confirmar que o usuario aprovou o registro da proposta.
- Confirmar que o identificador e unico e sequencial.
- Confirmar que o indice e `AGENTS.md` permitem alcancar a tarefa.
- Confirmar que links sao relativos, explicativos e validos.
- Confirmar que o arquivo contem apenas informacao necessaria para planejar.
- Confirmar que nenhum codigo, conhecimento permanente ou commit foi realizado.

## Retorno

Informar de forma curta:

- tarefa criada e seu link;
- identificador, titulo e estado;
- decisoes pendentes;
- se esta pronto para a criacao das fases ou qual lacuna impede o planejamento.

## Limites

- Nao criar fases tecnicas ou plano de implementacao.
- Nao implementar nem modificar codigo-fonte.
- Nao consolidar visao, dominios, recursos ou decisoes.
- Nao concluir tarefas.
- Nao registrar tarefa sem confirmacao explicita do usuario.
- Nao criar commit.
