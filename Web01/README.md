# Web01

Web01 e um conjunto de skills para conduzir mudancas em projetos web com um
fluxo rastreavel: entender a intencao, registrar uma tarefa, planejar fases,
executar uma fase por vez, validar resultados, consolidar conhecimento
permanente e fechar a tarefa com commits controlados.

O conjunto foi desenhado para evitar que conversas, implementacao, UX,
arquitetura e historico se misturem. Cada skill tem um papel especifico e deve
atuar com o menor contexto necessario.

## Quando usar

Use o Web01 quando quiser que o modelo ajude a:

- conversar sobre uma mudanca antes de implementa-la;
- organizar uma demanda em tarefa rastreavel;
- transformar uma tarefa em fases pequenas e verificaveis;
- executar fases comuns de desenvolvimento;
- executar fases UX com telas ou componentes mockados;
- manter conhecimento permanente do projeto;
- coordenar o fluxo inteiro sem escolher manualmente cada skill.

## Guia rapido

Para o uso cotidiano, chame o `orquestrador`. Ele classifica a intencao e aciona
as demais skills quando necessario.

Fluxo comum:

1. Use `orquestrador` para conversar, consultar o projeto ou pedir uma mudanca.
2. Quando houver uma mudanca nova, `criar-tarefa` organiza a ideia e registra a
   tarefa somente depois de confirmacao do usuario.
3. Com a tarefa em estado `Proposta`, `planejador` cria fases pequenas,
   navegaveis e verificaveis.
4. Depois da aprovacao das fases, `designer` executa fases UX e
   `desenvolvedor` executa fases comuns, respeitando dependencias.
5. Ao final das fases, `desenvolvedor` prepara o encerramento da tarefa.
6. Quando houver conhecimento permanente a consolidar, `arquiteto` atualiza os
   documentos permanentes.

Estados principais de uma tarefa:

```text
Proposta -> Planejada -> Em desenvolvimento -> Em encerramento -> Concluida
```

Estados principais de uma fase:

```text
Planejada -> Em desenvolvimento -> Concluida
```

Tambem podem ser usados estados como `Bloqueada`, `Cancelada` ou `Substituida`
quando o fluxo exigir.

## Skills

### [orquestrador](orquestrador/SKILL.md)

Ponto de entrada recomendado para o uso diario. Classifica se o usuario esta
fazendo uma pergunta, debatendo uma possibilidade, solicitando uma mudanca ou
continuando uma tarefa existente.

Ele coordena as demais skills conforme o estado da tarefa e evita burocracia
quando a conversa nao precisa virar trabalho registrado.

Use quando:

- quiser pedir uma mudanca sem escolher a skill manualmente;
- quiser descobrir a proxima acao de uma tarefa;
- quiser consultar o projeto respeitando a documentacao existente;
- quiser continuar um fluxo ja iniciado.

### [criar-tarefa](criar-tarefa/SKILL.md)

Transforma uma intencao de mudanca em uma tarefa proposta, curta e rastreavel.
Antes de escrever arquivos, conversa com o usuario para entender problema,
objetivo, resultado observavel, escopo e fora do escopo.

Tambem sugere complementos, simplificacoes e separacoes quando a demanda mistura
assuntos independentes.

Use quando:

- houver uma nova capacidade, alteracao, correcao, refatoracao, investigacao,
  documentacao ou infraestrutura a registrar;
- a ideia ainda precisar ser lapidada antes do planejamento;
- for necessario criar uma tarefa em `documentacao/tarefas/`.

### [planejador](planejador/SKILL.md)

Converte uma tarefa `Proposta` em fases pequenas, coerentes e verificaveis. Ele
mantem o resumo do plano em `tarefa.md` e cria um arquivo proprio para cada
fase, com objetivo, contexto, entrega esperada e criterios de conclusao.

Nao implementa codigo. O planejamento registrado ainda precisa de aprovacao do
usuario antes do desenvolvimento.

Use quando:

- uma tarefa proposta estiver pronta para ser dividida em fases;
- uma tarefa planejada precisar de revisao;
- novas fases precisarem ser registradas apos validacao do projeto.

### [designer](designer/SKILL.md)

Executa fases UX aprovadas. Cria ou altera telas, fluxos visuais, componentes e
handlers mockados para validar experiencia com o usuario.

Nao implementa backend real, persistencia, regras de dominio, autenticacao real
ou integracoes externas. A validacao principal e visual/interativa.

Use quando:

- a fase tiver `Tipo de fase: UX` ou `Executor: designer`;
- for preciso validar tela, fluxo ou componente com dados simulados;
- fases comuns posteriores dependerem de uma base visual ja validada.

### [desenvolvedor](desenvolvedor/SKILL.md)

Executa fases comuns aprovadas, uma por vez, lendo apenas o contexto necessario.
Implementa o menor resultado coerente, verifica o comportamento e aguarda
validacao explicita do usuario antes de criar commit.

Tambem conduz o encerramento da tarefa depois que todas as fases foram
concluidas, preparando o resumo final, solicitando consolidacao arquitetural
quando necessario e criando o commit final somente apos aprovacao.

Use quando:

- fases comuns planejadas ja estiverem aprovadas para desenvolvimento;
- for preciso integrar resultados de fases UX a dados, regras ou persistencia
  reais;
- uma tarefa concluida nas fases precisar ser fechada.

### [arquiteto](arquiteto/SKILL.md)

Avalia impactos permanentes e mantem o conhecimento do projeto: visao, dominios,
recursos e decisoes arquiteturais.

No modo `Avaliar`, identifica impactos, riscos e decisoes pendentes sem alterar
arquivos. No modo `Consolidar`, atualiza conhecimento permanente somente quando
ha autorizacao, decisao confirmada ou resultado validado.

Use quando:

- uma mudanca puder alterar conhecimento permanente;
- houver decisao arquitetural relevante;
- for necessario consolidar o que uma tarefa concluida entregou.

### [inicializador](inicializador/SKILL.md)

Cria ou reorganiza a documentacao local minima de um projeto. Trata `AGENTS.md`
como porta de entrada e usa divulgacao progressiva: resumo primeiro, detalhes
somente quando necessario.

Use quando:

- um projeto precisa iniciar sua documentacao para pessoas e agentes;
- a documentacao existente esta espalhada demais;
- for necessario criar uma estrutura minima como `AGENTS.md` e
  `documentacao/conhecimento.md`.

## Responsabilidades resumidas

| Skill | Papel |
|---|---|
| `orquestrador` | Coordenar o fluxo e escolher a proxima skill |
| `criar-tarefa` | Conversar, lapidar e registrar tarefa proposta |
| `planejador` | Dividir tarefa aprovada em fases verificaveis |
| `designer` | Executar fases UX com mocks e validacao visual |
| `desenvolvedor` | Executar fases comuns, verificar e commitar apos aprovacao |
| `arquiteto` | Avaliar e consolidar conhecimento permanente |
| `inicializador` | Criar ou reorganizar documentacao minima do projeto |

## Cuidados de uso

- Comece pelo `orquestrador` quando nao souber qual skill usar.
- Use uma skill especializada diretamente quando o papel ja estiver claro.
- Nao pule aprovacoes: proposta, fases, validacao de fontes, validacao UX e
  fechamento existem para manter rastreabilidade.
- Fases UX pertencem ao `designer`; fases comuns pertencem ao `desenvolvedor`.
- Mudancas permanentes de conhecimento devem passar pelo `arquiteto`.
- Commits so devem acontecer apos aprovacao explicita do usuario, conforme o
  fluxo da fase ou do fechamento.
