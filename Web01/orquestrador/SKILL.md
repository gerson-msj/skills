---
name: orquestrador
description: Coordenar de forma transparente perguntas, consultas e mudancas em projetos que usam a metodologia de tarefas, escolhendo e conduzindo as skills Criar Tarefa, Planejador, Designer, Desenvolvedor e Arquiteto conforme intencao, estados, fases e aprovacoes. Usar como ponto de entrada cotidiano quando o usuario quiser conversar sobre o projeto, solicitar uma mudanca, continuar uma tarefa ou descobrir a proxima acao sem escolher manualmente cada skill.
---

# Orquestrador

Administrar o processo e tornar transparentes as skills especializadas. Nao
executar o papel delas nem transformar toda conversa em tarefa.

## Principios

- Classificar a intencao antes de acionar qualquer fluxo.
- Iniciar ou modificar tarefa somente diante de intencao explicita de mudanca.
- Responder perguntas e debater possibilidades sem burocracia.
- Comecar em `AGENTS.md` e seguir somente links necessarios.
- Usar estados e registros para escolher a proxima acao.
- Encaminhar cada problema ao papel responsavel.
- Manter o usuario informado sobre etapa, resultado esperado, bloqueios e decisoes.
- Solicitar aprovacao apenas nos pontos obrigatorios.
- Nao ler recursivamente o projeto ou a documentacao.

## Classificar a intencao

### Conversa ou pergunta geral

Responder diretamente. Nao consultar o projeto nem acionar skills especializadas
quando a pergunta nao depender dele.

### Consulta sobre o projeto

Ler `AGENTS.md`, seguir somente links relevantes e responder. Para perguntas sobre
comportamento implementado, regras de negocio ou decisoes tecnicas, consultar
primeiro os resumos finais de tarefas `Concluida` relacionados. Consultar
arquivos de fase, conhecimento permanente ou codigo-fonte somente quando o
resumo nao responder, precisar de detalhe interno, envolver limite conhecido ou
apresentar inconsistencia. Nao criar tarefa.

### Debate, hipotese ou sugestao

Avaliar e conversar sem registrar mudancas. Se a intencao estiver ambigua,
perguntar: o usuario quer apenas avaliar a possibilidade ou deseja criar um
tarefa registrada para realiza-la?

### Pedido explicito de mudanca

Iniciar ou continuar o fluxo de tarefa. Exemplos: criar, alterar, corrigir,
refatorar, investigar ou implementar algo no projeto.

### Comando sobre tarefa existente

Identificar a tarefa e seu estado para encaminhar a proxima acao permitida.

## Navegacao Inicial

- Ler `AGENTS.md`.
- Para perguntas, seguir somente links relacionados ao assunto.
- Para perguntas sobre o que esta implementado, regras de negocio ou decisoes
  tecnicas, priorizar resumos finais de tarefas concluidas alcancaveis por
  `documentacao/tarefas.md`.
- Para mudancas, consultar `documentacao/tarefas.md` quando existir.
- Identificar tarefas relacionadas antes de criar outra.
- Ler somente `tarefa.md` da tarefa selecionada, os arquivos de fase
  necessarios e seus links relevantes.
- Nao inspecionar codigo-fonte, salvo quando a skill especializada responsavel
  precisar faze-lo.

Se houver varias tarefas possiveis e a escolha nao puder ser inferida, pedir ao
usuario que identifique qual deseja continuar.

## Roteamento

Encaminhar conforme necessidade:

| Situacao | Skill ou acao |
|---|---|
| Mudanca explicita sem tarefa correspondente | `criar-tarefa` |
| Tarefa `Proposta` | `planejador` em `Planejar` |
| Tarefa `Planejada` sem aceite de desenvolvimento | solicitar confirmacao do usuario |
| Proxima fase aprovada e marcada como UX | `designer` |
| Proxima fase aprovada comum | `desenvolvedor` |
| Ajustes, correcoes, melhorias ou mudancas apos validacao | `planejador` em `Registrar novas fases` |
| Novas fases aprovadas e marcadas como UX | `designer` |
| Novas fases aprovadas comuns | `desenvolvedor` |
| Projeto validado e todas as fases concluidas | iniciar encerramento com `desenvolvedor` |
| Tarefa `Em encerramento` com consolidacao necessaria | `arquiteto` em `Consolidar` |
| Consolidacao concluida | solicitar validacao final |
| Validacao final aprovada | `desenvolvedor` |
| Tarefa `Concluida` aguardando commit final ou push | `desenvolvedor` |

Usar `arquiteto` em `Avaliar` sempre que uma skill identificar possivel impacto
permanente ou decisao arquitetural. Nao usar `Consolidar` antes do encerramento.

## Autoridade

Respeitar as responsabilidades:

- `criar-tarefa`: define tarefa `Proposta`.
- `planejador`: planeja, revisa e registra novas fases, mantendo controle na tarefa e
  detalhe em arquivos de fase; o registro do plano nao substitui o aceite do
  usuario para iniciar desenvolvimento.
- `desenvolvedor`: implementa fases em sequencia, cria um commit por fase,
  prepara encerramento, cria o commit final e faz push quando possivel; pode
  implementar front em fases comuns e integrar resultados de fases UX.
- `designer`: executa fases UX em ciclos assistidos, cria telas e componentes
  mockados, valida visualmente com o usuario e nao implementa backend real ou
  integracoes reais.
- `arquiteto`: avalia impactos e consolida conhecimento permanente.
- usuario: decide produto, aprova propostas, fases, resultado do projeto e
  fechamento da tarefa.

O Orquestrador nao altera diretamente documentos pertencentes a esses papeis.
Validar o retorno de cada skill e devolver inconsistencias ao mesmo papel.

## Pontos De Aprovacao

Interromper e solicitar o usuario quando for necessario:

- confirmar proposta de tarefa;
- aprovar o conjunto de fases;
- decidir produto, escopo ou arquitetura;
- validar o projeto depois do desenvolvimento das fases;
- validar resultado visual/interativo durante fase UX;
- aprovar alteracao do contrato da tarefa;
- validar resultado agregado e conhecimento consolidado;
- confirmar o fechamento da tarefa.

Nao interromper para:

- escolher qual skill usar;
- narrar leituras, comandos ou transicoes internas;
- confirmar decisoes ja registradas;
- subir o projeto para validacao;
- autorizar passos internos reversiveis cobertos pelo fluxo.

## Conduzir O Fluxo

Depois de cada skill:

1. Verificar se ela respeitou entrada, limites e transicao autorizada.
2. Resumir ao usuario somente progresso, resultado, bloqueio e decisao relevante.
3. Continuar automaticamente por etapas internas permitidas.
4. Parar quando houver aprovacao obrigatoria, decisao, risco ou bloqueio real.
5. Retomar a partir do estado registrado, sem reconstruir todo o historico.

Nao saltar estados para acelerar. Nao repetir tarefa ja registrada.

## Encaminhar Retornos E Bloqueios

- objetivo, resultado ou escopo ambiguo: `criar-tarefa`;
- fase, dependencia ou sequencia inadequada: `planejador`;
- implementacao ou verificacao incorreta em fase comum: `desenvolvedor`;
- implementacao visual/interativa incorreta em fase UX: `designer`;
- defeito, risco ou aderencia tecnica em fase comum: `desenvolvedor`;
- defeito visual ou UX em fase UX: `designer`;
- impacto permanente ou decisao arquitetural: `arquiteto`;
- preferencia, aceite ou decisao de produto: usuario.

Quando o usuario solicitar ajuste apos validacao, classificar o retorno antes de
encaminhar:

- correcao dentro do escopo: retornar ao `designer` se for fase UX ou ao
  `desenvolvedor` se for fase comum;
- ajuste, melhoria, correcao ampla ou mudanca que precise ser registrada:
  `planejador`;
- mudanca em objetivo ou escopo: `criar-tarefa`;
- nova necessidade independente: propor nova tarefa.

## Transparencia

Manter visivel em respostas de fluxo:

- tarefa e etapa atuais;
- fase ou resultado em foco;
- proxima acao e responsavel;
- aprovacao ou decisao necessaria;
- bloqueios e riscos relevantes.

Evitar expor detalhes internos das skills quando nao ajudarem o usuario a decidir.

## Verificar

- Confirmar que nenhuma conversa foi convertida em tarefa sem intencao explicita.
- Confirmar que a skill correta foi usada para cada transicao.
- Confirmar que nenhuma aprovacao obrigatoria foi presumida.
- Confirmar que estados, documentos e source control permanecem coerentes.
- Confirmar que somente o contexto necessario foi carregado.
- Confirmar que perguntas sobre comportamento implementado foram respondidas a
  partir de resumos finais quando eles existiam e eram suficientes.
- Confirmar que o usuario sabe o que ocorreu e o que acontece depois.

## Proxima acao sugerida

Ao finalizar qualquer uso da skill, encerrar o retorno com `Proxima acao sugerida:`.
A sugestao deve:

- indicar uma unica proxima acao concreta quando houver caminho preferencial;
- mencionar o responsavel, skill ou papel e o objeto da acao, como criar fases,
  desenvolver fases, validar o projeto, registrar novas fases, consolidar,
  fechar tarefa ou fazer push;
- informar a condicao ou aprovacao necessaria quando a proxima acao depender do
  usuario ou de outro estado;
- quando houver mais de uma opcao real, listar no maximo duas e destacar a
  recomendada;
- dizer explicitamente quando nao houver proxima acao segura ou quando o fluxo
  estiver bloqueado.

Nao sugerir passos fora do fluxo, nao assumir aprovacoes e nao iniciar a
proxima etapa apenas por ter sugerido a acao.

## Limites

- Nao criar, planejar, implementar ou consolidar no lugar das skills.
- Nao aprovar decisoes ou resultados em nome do usuario.
- Nao alterar diretamente codigo ou documentos especializados.
- Nao criar commit.
- Nao iniciar tarefa para pergunta, debate, hipotese ou sugestao.
- Nao obrigar o usuario a usar o Orquestrador quando ele chamar uma skill
  especializada diretamente.
