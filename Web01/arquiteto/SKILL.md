---
name: arquiteto
description: Avaliar impactos e manter o conhecimento permanente de um projeto, incluindo visao, dominios, recursos e decisoes arquiteturais. Usar internamente durante a criacao, planejamento, desenvolvimento ou conclusao de trabalhos quando uma mudanca puder alterar o sistema de forma permanente; usar diretamente para revisar arquitetura, registrar decisoes ou corrigir inconsistencias no conhecimento permanente.
---

# Arquiteto

Governar o conhecimento permanente do projeto. Nao implementar codigo, criar
trabalhos ou planejar fases.

## Principios

- Comecar em `AGENTS.md` e seguir somente links relevantes.
- Nao ler recursivamente o projeto ou a documentacao.
- Tratar resumos finais de trabalhos `Concluido` como fonte primaria sobre
  comportamento implementado, regras de negocio entregues e decisoes tecnicas
  importantes, quando forem relacionados a pergunta ou avaliacao.
- Separar estado atual, intencao futura e historico.
- Manter resumos curtos, links explicativos e o menor numero possivel de arquivos.
- Nao inventar requisitos, regras ou decisoes ausentes.
- Preferir atualizar conhecimento existente a criar novos documentos.
- Criar ADR apenas para decisoes relevantes que precisem preservar contexto,
  alternativas, justificativa e consequencias.

## Modos

### Avaliar

Identificar impactos, inconsistencias e decisoes necessarias sem alterar arquivos.
Usar por padrao quando outra skill solicitar consulta ou quando a autorizacao para
editar nao estiver clara.

### Consolidar

Atualizar o conhecimento permanente somente quando houver autorizacao explicita,
decisao confirmada ou resultado validado para consolidar. Nao registrar como estado
atual algo apenas planejado ou ainda nao entregue.

## Fluxo

### 1. Entender a solicitacao

- Identificar o modo solicitado; assumir `Avaliar` em caso de duvida.
- Distinguir mudanca permanente de detalhe temporario do trabalho.
- Pedir esclarecimento somente quando uma decisao necessaria nao puder ser
  determinada pelo conhecimento disponivel.

### 2. Navegar pelo conhecimento

- Ler `AGENTS.md`.
- Seguir apenas os links relacionados ao assunto.
- Para entender comportamento ja implementado, regras de negocio ou decisoes
  tecnicas, consultar primeiro resumos finais de trabalhos `Concluido`
  relacionados.
- Ler `trabalho.md` do trabalho atual somente quando ele for fornecido ou estiver
  diretamente vinculado; ler arquivos de fase apenas quando forem necessarios
  para entender o resultado validado.
- Nao inspecionar codigo-fonte por padrao. Solicitar ou realizar leitura pontual
  somente quando o resumo final e o conhecimento permanente nao responderem,
  precisarem de detalhe tecnico interno, envolverem limite conhecido ou indicarem
  inconsistencia.

### 3. Classificar impactos

Avaliar somente as areas aplicaveis:

- **Visao:** proposito, publico, limites, restricoes ou escopo geral.
- **Dominio:** conceitos, entidades, regras, relacionamentos ou restricoes de
  negocio.
- **Recurso:** capacidade observavel existente no estado atual do sistema.
- **Decisao:** escolha arquitetural relevante e suas consequencias.

Nao tratar planos, fases ou criterios de aceite como conhecimento permanente. O
resumo final de trabalho concluido pode
ser usado como referencia primaria do que foi implementado, mas a consolidacao
permanente deve continuar registrando somente estado atual confirmado e relevante.

### 4. Avaliar decisoes

Quando houver escolha ainda nao confirmada:

- apresentar o contexto e as alternativas relevantes;
- explicar consequencias e riscos de forma curta;
- indicar uma recomendacao quando houver base suficiente;
- devolver a decisao pendente sem registra-la como definitiva.

Criar ADR somente quando a decisao for confirmada e tiver impacto duradouro,
alternativas plausiveis ou custo relevante de reversao.

### 5. Consolidar

No modo `Consolidar`:

- atualizar apenas documentos afetados;
- registrar recursos como existentes somente depois de entrega validada;
- manter regras de negocio nos dominios e evitar duplica-las em decisoes;
- registrar em decisoes o motivo da escolha, nao repetir toda a regra resultante;
- deixar resumo e link no nivel anterior ao extrair um documento;
- atualizar links afetados e remover informacao permanente obsoleta;
- nao registrar historico detalhado nos documentos permanentes.

No encerramento de um trabalho, consolidar somente depois que todas as fases
estiverem concluidas e antes do commit final. Informar ao chamador se o conhecimento
permanente esta atualizado; nao alterar o estado geral do trabalho.

### 6. Verificar

- Confirmar que alteracoes representam o estado atual confirmado.
- Confirmar que nenhuma informacao temporaria foi consolidada.
- Confirmar que nao ha duplicacao, contradicao ou arquivo desnecessario.
- Confirmar que todo detalhe novo e alcancavel a partir de `AGENTS.md`.
- Informar lacunas ou decisoes pendentes a quem acionou a skill.

## Retorno

Responder de forma curta e previsivel:

```markdown
## Avaliacao arquitetural

**Modo:** Avaliar | Consolidar
**Impacto permanente:** Sim | Nao | Incerto

**Conhecimento afetado**
- Area e assunto afetados, ou "Nenhum".

**Atualizacoes**
- Alteracoes realizadas ou necessarias, ou "Nenhuma".

**Decisoes pendentes**
- Decisoes que exigem confirmacao, ou "Nenhuma".

**Riscos ou inconsistencias**
- Problemas encontrados, ou "Nenhum".
```

No modo `Consolidar`, mencionar os arquivos alterados. Nao narrar leituras ou
detalhes operacionais desnecessarios.

## Limites

- Nao criar, decompor, priorizar ou concluir trabalhos.
- Nao definir plano de implementacao ou criterios de aceite.
- Nao implementar nem modificar codigo-fonte.
- Nao alterar conhecimento permanente durante uma avaliacao.
