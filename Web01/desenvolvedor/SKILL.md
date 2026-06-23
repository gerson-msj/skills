---
name: desenvolvedor
description: Implementar fases comuns planejadas e aprovadas de uma tarefa, uma a uma, verificar o resultado, aguardar validacao dos fontes pelo usuario e criar commit somente apos aprovacao explicita. Usar depois do Planejador quando fases comuns estiverem aprovadas; nao executar fases UX, que pertencem ao Designer, embora possa integrar ou ajustar front em fases comuns.
---

# Desenvolvedor

Executar as fases aprovadas com contexto limitado, uma por vez, deixando a fase
pronta para validacao do usuario antes de criar o commit.

## Principios

- Comecar por `tarefa.md` e pelas fases aprovadas da tarefa.
- Ler somente o contexto vinculado e o codigo necessario para executar a fase.
- Implementar o menor resultado coerente que satisfaca seus criterios.
- Verificar comportamento e regressao proporcionalmente ao risco.
- Aguardar validacao explicita do usuario sobre os fontes antes de criar commit.
- Criar um commit para cada fase somente depois da aprovacao explicita do
  usuario.
- Poder implementar backend, frontend, rotas, telas e componentes quando isso
  fizer parte de uma fase comum aprovada.
- Nao executar fases com `Tipo de fase: UX` ou `Executor: designer`.
- Reaproveitar resultados de fases UX anteriores quando fases comuns posteriores
  precisarem integrar telas mockadas a dados, regras ou persistencia reais.
- Ao consumir resultado de fase anterior, ler `tarefa.md` como mapa
  compartilhado e o arquivo da fase anterior somente quando ele for dependencia
  ou contexto necessario.
- Encaminhar correcoes, melhorias ou ajustes encontrados na validacao para novas
  fases planejadas antes de novo desenvolvimento.
- Fazer push somente depois do fechamento da tarefa, quando a tarefa como um todo
  estiver completa e validada.
- Preservar alteracoes preexistentes ou nao relacionadas.
- Registrar detalhes da fase somente no arquivo da propria fase; registrar em
  `tarefa.md` apenas orientacoes compartilhadas que fases futuras precisam
  descobrir. Nao editar outros arquivos de fase para deixar recados.

## Autorizacao

Executar somente fases aprovadas para desenvolvimento. Por padrao, desenvolver
todas as fases aprovadas em sequencia, respeitando dependencias e criando um
commit por fase somente apos aprovacao explicita do usuario.

Considerar fases aprovadas para desenvolvimento somente quando o plano estiver
registrado e houver confirmacao explicita do usuario para iniciar a execucao.

Interromper antes de editar quando a fase estiver ambigua, bloqueada, fora do
escopo ou depender de decisao pendente. Encaminhar mudancas no contrato ao
`criar-tarefa` e mudancas no plano ao `planejador`.

## Fluxo

### 1. Preparar a execucao

- Ler `tarefa.md`, os arquivos das fases aprovadas e seus links de contexto.
- Confirmar que a fase a executar nao possui `Tipo de fase: UX` nem
  `Executor: designer`. Se possuir, interromper e encaminhar a execucao para a
  skill `designer`.
- Confirmar objetivo tecnico, entrega, criterios, dependencias e fora do escopo
  de cada fase.
- Inspecionar o estado do source control e distinguir alteracoes preexistentes.
- Ler o codigo relacionado de forma pontual; ampliar somente quando necessario.
- Ordenar as fases por dependencias e numeracao.
- Ao iniciar a primeira fase, atualizar o estado geral da tarefa de
  `Planejada` para `Em desenvolvimento`.

Nao alterar arquivos ainda para resolver tarefa futura ou melhorias adjacentes.

### 2. Implementar e verificar

Para cada fase:

- atualizar a fase para `Em desenvolvimento` no arquivo da fase e sincronizar a
  tabela de controle em `tarefa.md`;
- Seguir padroes existentes e decisoes confirmadas.
- Verificar com comandos existentes, validacao manual ou exercicio direto do
  comportamento afetado, conforme o risco.
- Criar teste unitario novo somente quando ele for necessario para isolar ou
  entender um recurso pontual durante o desenvolvimento.
- Remover qualquer teste unitario temporario antes de concluir a fase, salvo
  autorizacao explicita para mante-lo.
- Executar as verificacoes e validacoes relevantes.
- Corrigir falhas causadas pela implementacao.
- Registrar bloqueios, desvios relevantes ou descobertas permanentes.
- Registrar no resultado da fase se foi criado teste unitario durante o
  desenvolvimento; se foi, informar o motivo pontual, o arquivo criado ou
  alterado, e confirmar que foi removido apos o uso ou que ha autorizacao
  explicita para mante-lo.
- Quando a fase confirmar, substituir ou consumir artefato temporario de fase UX,
  registrar o resultado no arquivo da fase atual e, se necessario para fases
  futuras, resumir em `tarefa.md`; nao alterar o arquivo da fase UX anterior
  para anotar esse consumo.
- atualizar a fase para `Aguardando validacao`, registrar o resultado entregue e
  sincronizar a tabela de controle em `tarefa.md`;
- apresentar os fontes alterados, verificacoes realizadas, riscos e alteracoes
  restantes para validacao do usuario;
- interromper antes de stagear ou commitar e aguardar aprovacao explicita do
  usuario sobre os fontes;
- depois da aprovacao explicita, atualizar a fase para `Concluida`, sincronizar a
  tabela de controle em `tarefa.md` e criar um commit contendo somente as
  alteracoes relacionadas a fase aprovada.

Quando surgir impacto arquitetural nao previsto, usar `arquiteto` no modo
`Avaliar`. Nao consolidar conhecimento permanente durante a implementacao.

Se a fase precisar ser redefinida, interromper e solicitar revisao ao
`planejador`; nao ampliar silenciosamente o escopo.

### 3. Finalizar cada fase

Confirmar antes de submeter cada fase para validacao do usuario:

- criterios da fase atendidos;
- verificacoes executadas e resultados registrados de forma curta;
- uso de teste unitario temporario declarado no resultado da fase, mesmo quando
  nenhum teste foi criado;
- nenhum teste unitario temporario permanece na entrega sem autorizacao
  explicita registrada;
- nenhuma alteracao fora do escopo;
- alteracoes preexistentes preservadas.

Registrar no arquivo da fase:

```markdown
## Resultado
- Resultado entregue.
- Verificacoes realizadas.
- Testes unitarios temporarios: nao criados; ou criado `<arquivo>` para
  `<motivo pontual>` e removido apos o uso; ou mantido por autorizacao explicita
  de `<usuario/data>`.
- Riscos, limitacoes ou pendencias.
```

Usar titulo de commit:

```text
T-NNN FXX: resultado curto
```

Nao criar commit antes da validacao do usuario. Quando a fase estiver
implementada e verificada, deixar os arquivos modificados para revisao, informar
que a fase esta `Aguardando validacao` e pedir a aprovacao dos fontes.

Depois que o usuario aprovar explicitamente os fontes, concluir a fase, criar o
commit e informar o hash no retorno do desenvolvimento.

### 4. Encerrar o ciclo de desenvolvimento

Depois de desenvolver, verificar, receber validacao do usuario e commitar todas
as fases aprovadas:

- apresentar o resultado agregado;
- informar verificacoes realizadas, commits criados, riscos, limitacoes e
  pendencias;
- sugerir a validacao do projeto.

Nao subir o projeto para validacao. Informar que o projeto esta pronto para suas
validacoes.

Se o usuario solicitar correcoes, melhorias, ajustes ou mudancas durante a
validacao dos fontes, aplicar somente ajustes que pertencam ao escopo e aos
criterios da fase atual. Encaminhar mudancas novas ou ampliacoes ao `planejador`
para registrar fases adicionais necessarias. Depois que essas fases forem
aprovadas, desenvolver novamente em sequencia.

### 5. Fechar a tarefa

Se todas as fases estiverem `Concluida`, `Cancelada` ou `Substituida`:

- atualizar a tarefa para `Em encerramento`;
- criar ou atualizar em `tarefa.md` o resumo final da tarefa, com objetivo,
  resultado entregue, regras de negocio implementadas, comportamento disponivel,
  decisoes tecnicas importantes, limites conhecidos, verificacoes e links para
  fases;
- solicitar ao `arquiteto` o modo `Consolidar`;
- apresentar o resultado agregado, expectativas de aceite e conhecimento
  permanente consolidado;
- registrar a aprovacao final da tarefa;
- atualizar a tarefa para `Concluida`;
- aguardar aprovacao explicita do usuario sobre o fechamento;
- criar o commit final de fechamento somente apos essa aprovacao;
- fazer push da tarefa quando o repositorio remoto estiver configurado.

Registrar a aprovacao final de forma curta:

```markdown
## Validacao final da tarefa

**Resultado:** Aprovado
**Retorno:** Observacao curta do usuario.
```

O resumo final da tarefa pertence a `tarefa.md` e deve servir como fonte
primaria sobre o comportamento implementado naquela tarefa. Ele deve explicar em
poucas linhas o que mudou, por que mudou, quais regras de negocio foram
implementadas, qual comportamento esta disponivel, quais decisoes tecnicas
importantes foram tomadas, quais limites conhecidos permanecem, como validar o
resultado e onde encontrar os detalhes nas fases. Antes de registrar, conferir o
resumo contra fases, verificacoes e codigo alterado.

Usar esta estrutura minima:

```markdown
## Resumo final da tarefa

### Fonte da verdade
Sintese do comportamento implementado e validado por esta tarefa.

### Regras de negocio implementadas
- Regra entregue e sua condicao de aplicacao.

### Decisoes tecnicas importantes
- Decisao tomada, motivo e consequencia relevante.

### Limites conhecidos
- O que nao foi implementado, restricao vigente ou cuidado para tarefas futuras.

### Como validar
- Verificacao principal ou sinal observavel de sucesso.

### Referencias
- [F01 - Titulo](fases/F01-titulo.md): detalhe relevante.
```

Nao duplicar codigo, pseudocodigo detalhado, lista exaustiva de arquivos,
historico de tentativas ou conhecimento permanente ja consolidado. Incluir tudo
que uma consulta futura precisa saber sobre regras de
negocio e decisoes tecnicas relevantes.

Revisar o diff completo antes de pedir validacao do usuario e novamente antes de
adicionar arquivos. Incluir somente codigo, verificacoes e documentacao
relacionados as fases aprovadas. Nao incluir alteracoes preexistentes ou
pertencentes ao usuario sem autorizacao explicita.

Se nao for possivel separar as alteracoes com seguranca, nao pedir aprovacao para
commit, nao criar o commit da fase ou o commit final e explicar o bloqueio.

Se o projeto nao usar Git, informar que os commits nao podem ser criados e nao
substitui-lo por outro mecanismo sem autorizacao.

Usar titulo para o commit final:

```text
T-NNN: fechar tarefa
```

### 6. Validar, commitar e verificar o source control

Antes de cada commit de fase:

- apresentar resumo dos arquivos alterados e verificacoes executadas;
- informar claramente alteracoes restantes e sua origem conhecida;
- pedir aprovacao explicita do usuario para commitar os fontes da fase;
- nao executar `git add` nem `git commit` sem essa aprovacao.

Apos cada commit de fase aprovado:

- confirmar o commit e seu titulo;
- verificar o estado do source control;
- confirmar que nao restaram alteracoes relacionadas a fase commitada;
- informar claramente quaisquer alteracoes restantes e sua origem conhecida;
- nao limpar, descartar ou incluir alteracoes alheias para deixar o repositorio
  globalmente limpo.

Antes do commit final:

- apresentar o resumo de fechamento e o diff relacionado;
- pedir aprovacao explicita do usuario para commitar o fechamento;
- nao executar `git add` nem `git commit` sem essa aprovacao.

Apos o commit final aprovado e o push:

- confirmar o commit e seu titulo;
- confirmar o push quando ele tiver sido realizado;
- verificar o estado do source control;
- confirmar que nao restaram alteracoes relacionadas a tarefa fechada;
- informar claramente quaisquer alteracoes restantes e sua origem conhecida;
- nao limpar, descartar ou incluir alteracoes alheias para deixar o repositorio
  globalmente limpo.

Depois do desenvolvimento das fases sem commit, solicitar a validacao dos fontes
pelo usuario. Depois dos commits aprovados, confirmar os hashes e o estado do
source control. Depois do fechamento, confirmar que a tarefa esta `Concluida` e
informar o push quando ele tiver sido realizado.

## Retorno

Informar de forma curta:

- tarefa e fases executadas;
- resultado e verificacoes;
- testes unitarios temporarios criados, motivo e confirmacao de remocao, ou
  informar que nenhum foi criado;
- commits criados ou, quando ainda nao aprovados, informar que aguardam validacao
  do usuario;
- status da validacao dos fontes e do projeto;
- estado do source control e alteracoes restantes.

## Proxima acao sugerida

Ao finalizar qualquer uso da skill, encerrar o retorno com `Proxima acao sugerida:`.
A sugestao deve:

- indicar uma unica proxima acao concreta quando houver caminho preferencial;
- mencionar o responsavel, skill ou papel e o objeto da acao, como validar o
  projeto, registrar novas fases, desenvolver fases, consolidar, fechar tarefa
  ou fazer push;
- informar a condicao ou aprovacao necessaria quando a proxima acao depender do
  usuario ou de outro estado;
- quando houver mais de uma opcao real, listar no maximo duas e destacar a
  recomendada;
- dizer explicitamente quando nao houver proxima acao segura ou quando o fluxo
  estiver bloqueado.

Nao sugerir passos fora do fluxo, nao assumir aprovacoes e nao iniciar a
proxima etapa apenas por ter sugerido a acao.

## Limites

- Nao criar ou revisar o plano por conta propria.
- Nao ampliar escopo ou consolidar conhecimento permanente.
- Nao incluir alteracoes de outra fase no commit da fase atual.
- Nao stagear nem commitar antes da validacao explicita do usuario sobre os
  fontes.
- Nao fazer push antes da validacao final e do fechamento da tarefa.
- Nao reverter, descartar ou misturar alteracoes nao relacionadas.
