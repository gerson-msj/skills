---
name: inicializador
description: Inicializar ou reorganizar a documentacao local de um projeto para pessoas e agentes, usando divulgacao progressiva, resumos navegaveis, links explicativos e o menor numero possivel de arquivos. Usar ao iniciar um projeto, implantar a metodologia de orquestracao, criar o ponto central AGENTS.md ou reduzir documentacao pulverizada.
---

# Inicializador

Criar uma documentacao local pequena, navegavel e suficiente. Tratar `AGENTS.md`
como porta de entrada para pessoas e agentes. Nao ler o projeto inteiro nem criar
arquivos preventivamente.

## Principios

- Comecar pelo resumo e aprofundar somente quando necessario.
- Otimizar para a menor leitura necessaria, nao para o maior detalhamento.
- Comecar com poucos arquivos; dividir apenas quando isso melhorar a navegacao.
- Usar links relativos e explicativos. Ninguem deve precisar explorar pastas para
  encontrar conhecimento importante.
- Manter conhecimento permanente separado do trabalho temporario.
- Registrar o estado atual nos documentos permanentes, sem transforma-los em
  historicos extensos.
- Escrever para um leitor sem contexto previo, com frases curtas e concretas.

## Fluxo

### 1. Confirmar o escopo

- Identificar se o projeto e novo ou se a documentacao existente sera reorganizada.
- Nao inspecionar codigo-fonte sem autorizacao do usuario.
- Se houver documentacao existente, preserva-la e propor mudancas antes de
  substituir ou mover arquivos.

### 2. Entrevistar progressivamente

Fazer poucas perguntas por rodada. Comecar pelo essencial:

1. O que e o sistema, para quem existe e qual problema resolve?
2. Quais sao os principais conceitos ou areas de negocio?
3. O que o sistema oferece ou pretende oferecer primeiro?
4. Existe alguma decisao importante ja tomada?

Resumir as respostas e confirmar o entendimento antes de criar a estrutura.
Nao exigir respostas para assuntos ainda desconhecidos; registrar lacunas de forma
breve.

### 3. Criar a estrutura minima

Usar como ponto de partida, adaptando ao que realmente existe:

```text
/
|-- AGENTS.md
`-- documentacao/
    `-- conhecimento.md
```

Criar pastas ou arquivos adicionais somente quando um conteudo precisar ser
consultado ou alterado independentemente.

### 4. Escrever o ponto de entrada

Manter `AGENTS.md` curto. Incluir:

- resumo do sistema em poucas linhas;
- regra de navegacao: ler resumos e seguir somente links relevantes;
- links explicativos para o conhecimento local;
- instrucoes essenciais que se aplicam a qualquer agente.

Nao duplicar detalhes presentes nos documentos vinculados.

### 5. Escrever o conhecimento local

Comecar `documentacao/conhecimento.md` com um resumo e links para qualquer conteudo
que tenha sido extraido. Manter, enquanto forem pequenos, estes assuntos no mesmo
arquivo:

- **Visao:** proposito, publico, problema, limites e restricoes.
- **Dominios:** conceitos, entidades, regras e relacionamentos.
- **Recursos:** capacidades atuais do sistema, nao planos de implementacao.
- **Decisoes:** decisoes relevantes, contexto e consequencias.

Extrair uma secao para arquivo proprio apenas quando ela:

- crescer a ponto de dificultar a leitura do restante;
- for consultada ou alterada independentemente;
- tiver ritmo de mudanca diferente;
- reduzir significativamente a leitura necessaria para fases comuns.

Ao extrair, deixar no arquivo anterior um resumo curto com link explicativo. Todo
arquivo detalhado deve comecar com resumo e ser alcancavel a partir de `AGENTS.md`.

### 6. Verificar antes de concluir

- Confirmar que nenhum arquivo desnecessario foi criado.
- Confirmar que todos os links funcionam e possuem descricao curta.
- Confirmar que cada detalhe e alcancavel partindo de `AGENTS.md`.
- Confirmar que os resumos permitem decidir se vale aprofundar a leitura.
- Confirmar que nao ha duplicacao relevante.
- Confirmar que nenhum trabalho foi criado ou planejado.
- Apresentar ao usuario a estrutura criada e as lacunas que ainda precisam de
  resposta.

## Proxima acao sugerida

Ao finalizar qualquer uso da skill, encerrar o retorno com `Proxima acao sugerida:`.
A sugestao deve:

- indicar uma unica proxima acao concreta quando houver caminho preferencial;
- mencionar o responsavel, skill ou papel e o objeto da acao, como criar fases,
  desenvolver fases, validar o projeto, registrar novas fases, consolidar,
  fechar trabalho ou fazer push;
- informar a condicao ou aprovacao necessaria quando a proxima acao depender do
  usuario ou de outro estado;
- quando houver mais de uma opcao real, listar no maximo duas e destacar a
  recomendada;
- dizer explicitamente quando nao houver proxima acao segura ou quando o fluxo
  estiver bloqueado.

Nao sugerir passos fora do fluxo, nao assumir aprovacoes e nao iniciar a
proxima etapa apenas por ter sugerido a acao.
## Regra fundamental

Nunca ler recursivamente toda a documentacao como procedimento padrao. Ler
`AGENTS.md`, classificar a necessidade, seguir apenas os links relevantes e parar
quando houver contexto suficiente para agir.
