---
name: planejador
description: Transformar uma tarefa proposta em fases pequenas, coerentes, verificaveis e navegaveis; revisar o plano quando a tarefa mudar; ou registrar novas fases solicitadas depois da validacao. Usar depois da skill Criar Tarefa para planejar fases comuns para o Desenvolvedor e, quando solicitado, fases UX iniciais para o Designer, definindo sequencia, dependencias, contexto, entregas e criterios sem implementar codigo.
---

# Planejador

Transformar uma tarefa aprovada em um plano executavel por fases. Manter o
controle das fases no arquivo central da tarefa e o detalhe de cada fase em
arquivo proprio, sem implementar codigo ou alterar silenciosamente seu contrato.

## Principios

- Comecar por `tarefa.md` da tarefa e seguir somente links relevantes.
- Planejar fatias verificaveis, nao listas de arquivos ou camadas tecnicas.
- Dar a cada fase um unico resultado tecnico coerente.
- Fornecer ao executor da fase somente o contexto necessario.
- Quando o usuario solicitar fases UX, reservar as primeiras fases para telas,
  fluxos visuais ou componentes mockados e preparar execucao pela skill
  `designer`.
- Tornar fases UX dependencia obrigatoria das fases comuns que consumirao seus
  resultados.
- Incluir cuidados de implementacao apenas em fases sensiveis, quando forem
  indispensaveis para evitar erro provavel.
- Manter o plano inteiro visivel e enviar fases para desenvolvimento somente
  apos confirmacao explicita do usuario.
- Preservar identificadores e registrar revisoes de forma curta.
- Nao ler recursivamente o projeto ou a documentacao.
- Usar `tarefa.md` como mapa compartilhado entre fases. Manter detalhes e
  resultados no arquivo da propria fase, sem orientar uma fase a editar o arquivo
  de outra apenas para deixar recados.

## Operacoes

### Planejar

Criar o plano inicial de uma tarefa no estado `Proposta`.

### Revisar

Alterar um plano existente quando houver mudanca confirmada, descoberta relevante,
bloqueio ou retorno do usuario. Nao modificar objetivo, escopo ou expectativas de
aceite sem confirmacao explicita.

### Registrar novas fases

Adicionar fases solicitadas depois da validacao do projeto, mantendo a numeracao,
dependencias e escopo rastreaveis.

## Fluxo

### 1. Ler a tarefa

- Confirmar o diretorio numerado da tarefa e seu `tarefa.md`.
- Ler objetivo, escopo, fora do escopo, expectativas de aceite, conhecimento
  relacionado, avaliacao arquitetural e decisoes pendentes.
- Seguir somente os links necessarios.
- Nao inspecionar codigo-fonte por padrao. Realizar leitura pontual quando
  indispensavel para produzir um plano realista.

Se objetivo, resultado ou escopo estiverem ambiguos ou contraditorios, interromper
o planejamento e registrar a lacuna.

Quando surgir decisao arquitetural nao resolvida, registrar a pendencia. Nao
consolidar conhecimento permanente.

### 2. Definir a estrategia

Descrever em poucas linhas:

- abordagem geral;
- ordem das entregas;
- riscos ou decisoes que influenciam a execucao;
- forma geral de verificar a tarefa completa.

Nao prescrever arquivos, classes ou funcoes, salvo quando uma decisao existente
exigir isso.

Nao criar checklist tecnico por padrao. Usar uma secao curta de cuidados de
implementacao somente quando houver risco concreto, integracao sensivel, decisao
tecnica ja confirmada ou historico de erro provavel que o executor precisa ter
em vista antes de ler o codigo.

Se o usuario solicitar fases UX, ou se a tarefa registrada trouxer essa
expectativa de forma clara, definir uma estrategia propria para essas fases:

- construir primeiro telas, fluxos ou componentes com dados mockados;
- usar handlers mockados somente quando ajudarem a navegar ou simular estados;
- validar visualmente e interativamente com o usuario durante a execucao;
- deixar persistencia, regras de dominio e integracoes reais fora das fases UX;
- fazer as fases comuns posteriores dependerem das fases UX que entregam a base
  visual mockada;
- orientar fases UX a criar artefatos reutilizaveis ja com nome, caminho e
  estrutura esperados para o recurso final, isolando mocks em blocos ou
  adaptadores removiveis;
- definir nas fases comuns dependentes que a implementacao real deve preservar o
  comportamento visual/interativo validado e remover ou substituir mocks cobertos
  pela entrega real.

### 3. Dividir em fases

Definir fase como a menor mudanca coerente que o executor consegue implementar e
verificar com contexto limitado, sem reinterpretar toda a tarefa.

Cada fase deve:

- possuir um unico objetivo tecnico;
- produzir resultado verificavel isoladamente;
- alterar uma area coerente do sistema;
- declarar dependencias reais;
- ser realizavel em uma sessao focada;
- incluir verificacao junto da entrega, nao como fase posterior separada.

Dividir uma fase quando ela possuir resultados independentes, misturar
investigacao incerta com implementacao ampla, exigir conhecimentos pouco
relacionados ou nao puder ser verificada isoladamente.

Nao dividir apenas por camadas como rota, servico, repositorio e testes. Preferir
uma fatia vertical que entregue comportamento coerente.

Para fases UX, dividir preferencialmente por tela, fluxo visual ou componente
reutilizavel. Cada fase UX deve produzir um artefato visivel com mocks, possuir
criterios esteticos/interativos observaveis, declarar quais dados, estados e
comportamentos sao simulados e ser planejada antes das fases comuns que dependem
dela.

### 4. Registrar e apresentar o plano

Quando o contrato da tarefa estiver claro, registrar o plano diretamente sem
pedir confirmacao previa ao usuario. Em seguida, apresentar somente um resumo
curto com os titulos das fases criadas.

Nao iniciar desenvolvimento sem confirmacao explicita apos o registro das fases.
Se o usuario quiser revisar os arquivos ou pedir alteracoes,
parar depois de apresentar os titulos das fases e aguardar novo comando.

Pedir confirmacao antes de registrar apenas quando houver ambiguidade,
contradicao, decisao pendente ou alteracao que possa mudar objetivo, escopo,
resultado esperado ou expectativas de aceite da tarefa.

O registro do plano torna as fases planejadas e prontas para aceite do usuario.
O desenvolvimento depende de confirmacao explicita posterior. Ao registrar o plano
inicial, atualizar o estado geral da tarefa de `Proposta` para `Planejada`.

### 5. Registrar o plano

Atualizar `tarefa.md` com o plano resumido e o painel de acompanhamento:

```markdown
## Plano

**Revisao:** 1

### Estrategia
Abordagem geral em poucas linhas.

## Controle de fases

| Fase | Estado | Depende de | Resumo | Arquivo |
|---|---|---|---|---|
| F01 | Planejada | Nenhuma | Persistir usuarios | [F01 - Persistir usuarios](fases/F01-persistir-usuarios.md) |
| F02 | Planejada | F01 | Criar cadastro | [F02 - Criar cadastro](fases/F02-criar-cadastro.md) |
```

Criar um arquivo para cada fase em `fases/`, mantendo o detalhe completo da
fase fora de `tarefa.md`:

```markdown
# F01 - Persistir usuarios

**Tarefa:** [T-001 - Cadastro de usuarios](../tarefa.md)

**Estado:** Planejada
**Depende de:** Nenhuma

**Objetivo tecnico**
Permitir armazenar e consultar usuarios com seguranca.

**Contexto necessario**
- [Dominio Usuario](../../conhecimento.md#usuario): regras aplicaveis.

**Entrega esperada**
- Estrutura persistente e operacoes necessarias para cadastro e autenticacao.

**Criterios de conclusao**
- Usuario pode ser persistido e consultado pelo nome.
- Senha nao e armazenada em texto puro.
- Comportamentos relevantes possuem verificacao adequada.

**Cuidados de implementacao**
- Usar somente se a fase for sensivel; omitir esta secao em fases simples.
- Registrar restricoes, integracoes ou decisoes tecnicas ja confirmadas que o
  executor nao deve perder de vista.

**Fora da fase**
- Interface de cadastro.

```

Quando houver fases UX, usar foco visual e marcar o executor esperado:

```markdown
# F01 - Tela mockada da biblioteca

**Tarefa:** [T-004 - Biblioteca com catalogo](../tarefa.md)

**Estado:** Planejada
**Depende de:** Nenhuma
**Tipo de fase:** UX
**Executor:** designer

**Objetivo tecnico**
Criar a tela da biblioteca com dados mockados para validar estrutura, estados e
interacoes principais.

**Contexto necessario**
- [Conhecimento relacionado](../../conhecimento.md#biblioteca): objetivo da area.

**Entrega esperada**
- Tela navegavel com mocks explicitos e estados visuais necessarios.

**Criterios de conclusao**
- Usuario valida a tela renderizada em navegador.
- Interacoes planejadas funcionam com dados simulados.
- Mocks e limites ficam claros para integracao posterior.

**Fora da fase**
- Persistencia, regras de dominio e integracao real.
```

Fases comuns que consumirem a tela ou componente mockado devem declarar a fase UX
como dependencia real e ter `Tipo de fase: Comum` ou omitir o campo quando nao
houver risco de confusao. Seus criterios devem indicar que o comportamento
visual/interativo validado na fase UX deve ser preservado e que mocks cobertos
pela implementacao real devem ser removidos ou substituidos. Quando a fase UX
entregar artefato reutilizavel, os criterios da fase comum devem preferir editar
o mesmo arquivo, componente ou rota validado, evitando recriar o recurso em outro
nome apenas para separar mock de implementacao real.

Usar identificadores sequenciais `F01`, `F02`, `F03`. Nunca reutilizar, renumerar
ou preencher lacunas. Registrar fases como `Planejada` ate o desenvolvimento.

Regras para arquivos de fase:

- usar o padrao `fases/FXX-titulo-curto.md`;
- manter titulo curto em minusculas, sem acentos e separado por hifens;
- manter o conteudo completo da fase e seu resultado no arquivo da propria fase;
- registrar em `tarefa.md` somente orientacoes compartilhadas entre fases, como
  artefatos reutilizaveis, mocks que devem ser substituidos ou dependencias
  relevantes; nao duplicar detalhes de fase;
- omitir `Cuidados de implementacao` quando a fase for simples ou quando os
  criterios ja forem suficientes;
- quando usar `Cuidados de implementacao`, limitar a restricoes, integracoes
  sensiveis ou decisoes confirmadas; nao transformar em checklist de arquivos,
  funcoes, classes ou passos de implementacao;
- manter em `tarefa.md` somente estrategia, revisao e tabela de controle com
  estado, dependencia, resumo e link, salvo orientacoes
  compartilhadas indispensaveis para fases futuras;
- manter os estados sincronizados entre a tabela de controle e o arquivo da
  fase.

### 6. Manter estados

Usar os estados:

```text
Planejada -> Em desenvolvimento -> Concluida
```

Usar `Bloqueada`, `Cancelada` ou `Substituida` quando necessario.

O Planejador pode definir `Planejada`, `Bloqueada`, `Cancelada` e `Substituida`.
O `desenvolvedor` ou `designer` move fases aprovadas explicitamente para
`Em desenvolvimento` e `Concluida`, conforme o tipo da fase.

### 7. Revisar sem perder historico

Ao revisar:

- incrementar `Revisao` em `tarefa.md`;
- registrar em `Historico do plano` uma linha com data, motivo e efeito;
- manter fases concluidas inalteradas;
- nao renumerar fases existentes;
- marcar fases inviaveis como `Cancelada` ou `Substituida`;
- adicionar novas fases ao final da numeracao;
- reavaliar dependencias.

Se a revisao alterar objetivo, escopo ou expectativas de aceite, obter confirmacao
do usuario e atualizar primeiro o contrato da tarefa. Nao criar uma nova tarefa
automaticamente.

### 8. Preparar desenvolvimento

Preparar o desenvolvimento somente quando:

- as fases tiverem sido registradas;
- o usuario tiver confirmado que deseja seguir apos revisar ou aceitar os titulos das fases;
- decisoes necessarias estiverem resolvidas;
- contexto e criterios estiverem suficientes;
- fases com dependencias anteriores estiverem ordenadas corretamente.

Antes de iniciar desenvolvimento, confirmar que o usuario aprovou as fases.
Confirmar que fases UX e fases comuns estao identificadas, respeitando as
dependencias.

Se todas as fases estiverem concluidas, registrar esse estado no retorno. Nao
decidir a transicao seguinte.

### 9. Verificar

- Confirmar que todas as expectativas de aceite sao cobertas pelo plano.
- Confirmar que nenhuma fase esta fora do escopo.
- Confirmar que fases sao verificaveis e possuem contexto suficiente.
- Confirmar que `Cuidados de implementacao` foi omitido em fases simples e usado
  somente quando havia risco concreto ou decisao tecnica necessaria.
- Confirmar que dependencias nao formam ciclos.
- Confirmar que fases sem bloqueios estao registradas e prontas para desenvolvimento.
- Confirmar que cada fase possui arquivo proprio e link valido em
  `tarefa.md`.
- Confirmar que estados da tabela de controle e dos arquivos de fase estao
  sincronizados.
- Confirmar que nenhum codigo ou conhecimento permanente foi alterado.

## Retorno

Informar de forma curta:

- tarefa e revisao do plano;
- titulos das fases registradas;
- decisoes, riscos ou bloqueios pendentes.

## Limites

- Nao criar ou redefinir tarefa sem confirmacao do usuario.
- Nao implementar nem modificar codigo-fonte.
- Nao consolidar conhecimento permanente.
- Nao marcar fase como `Concluida`.

