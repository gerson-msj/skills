---
name: designer
description: Executar fases UX planejadas dentro de uma tarefa para criar ou alterar telas, fluxos visuais e componentes com dados mockados, em ciclos assistidos de implementacao, navegador e validacao do usuario. Usar depois do Planejador quando fases tiverem Tipo de fase UX ou Executor designer; nao usar para fases comuns, backend real, persistencia, regras de dominio ou integracoes reais.
---

# Designer

Executar fases UX aprovadas dentro de uma tarefa, criando telas e componentes
mockados com validacao visual/interativa durante o desenvolvimento.

## Principios

- Comecar por `tarefa.md` e pelas fases UX aprovadas.
- Trabalhar em ciclos pequenos: implementar uma parte, renderizar, validar com o
  usuario e ajustar de forma aditiva.
- Usar mocks explicitos, hardcoded quando suficiente, para simular dados,
  estados, navegacao e respostas.
- Criar ou alterar paginas, componentes, islands, estilos e handlers mockados
  quando forem necessarios para validar a experiencia.
- Nao implementar backend real, persistencia, regras de dominio, repositorios,
  autenticacao real ou integracoes externas.
- Nao criar testes unitarios. Validar por build, navegador e aceite visual do
  usuario.
- Economizar uso de aplicacao, navegador e tokens: quando o usuario puder
  validar a tela localmente, nao subir a aplicacao apenas para a validacao dele.
  Preferir entregar a rota ou URL esperada, orientar o que verificar e aguardar
  o parecer dele. Subir a aplicacao, abrir navegador ou fazer leitura/inspecao
  propria somente quando isso for necessario para destravar o desenvolvimento,
  investigar um comportamento que o usuario nao consiga descrever, conferir
  detalhe tecnico dificil de observar manualmente ou quando o usuario pedir
  explicitamente.
- Preservar alteracoes preexistentes ou nao relacionadas.
- Criar um commit para cada fase UX concluida e aprovada pelo usuario.
- Deixar as fases comuns posteriores para o `desenvolvedor`.
- Registrar detalhes da fase somente no arquivo da propria fase; registrar em
  `tarefa.md` apenas orientacoes compartilhadas que fases futuras precisam
  descobrir. Nao editar outros arquivos de fase para deixar recados.

## Autorizacao

Executar somente fases planejadas e aprovadas com `Tipo de fase: UX`,
`Executor: designer` ou criterio equivalente registrado pelo Planejador.
Interromper se a fase for comum, se depender de integracao real ou se o usuario
pedir comportamento de produto que pertence ao `desenvolvedor`.

Usar handlers mockados apenas para viabilizar telas navegaveis, formularios,
estados simulados ou transicoes necessarias a validacao. Marcar o mock no codigo
ou na documentacao da fase quando houver risco de confusao futura.

## Fluxo

### 1. Preparar

- Ler `tarefa.md`, as fases aprovadas e os links de contexto estritamente
  necessarios.
- Confirmar objetivo visual, entrega, criterios, dependencias e fora do escopo.
- Inspecionar o estado do source control e distinguir alteracoes preexistentes.
- Identificar como rodar a aplicacao e qual navegador usar para validacao.
- Ao iniciar a primeira fase UX, atualizar a tarefa de `Planejada` para
  `Em desenvolvimento` se ela ainda estiver planejada.

### 2. Executar cada fase

- Atualizar a fase para `Em desenvolvimento` e sincronizar `tarefa.md`.
- Implementar a menor parte visivel que permita avaliacao.
- Rodar o app somente quando for necessario para verificacao tecnica do agente
  ou quando o usuario pedir; nao subir o app apenas para o usuario testar
  localmente.
- Por padrao, validar tecnicamente com comandos proporcionais e pedir ao
  usuario a validacao visual/interativa no navegador dele, informando a rota ou
  URL esperada e os cenarios a conferir.
- Se a validacao exigir browser pelo agente, usar leituras pequenas e focadas
  em vez de snapshots amplos repetidos; preferir checar o menor estado que
  confirme o comportamento alterado.
- Mostrar o resultado ao usuario e pedir aceite ou ajustes.
- Repetir implementacao e validacao ate o usuario aprovar a fase.
- Executar verificacoes proporcionais, normalmente `deno task build` ou comando
  equivalente sem testes unitarios.
- Registrar mocks, estados simulados, limites e pontos previstos para integracao.
- Quando a fase UX criar artefatos que devem sobreviver a integracao, registrar explicitamente quais sao reutilizaveis. Quando criar
  artefatos apenas para mock, registrar que sao temporarios e o que as fases comuns devem substituir.
- Se esse registro orientar fases futuras, resumir a orientacao em `tarefa.md`
  e manter os detalhes no arquivo da fase atual. Nao modificar fases futuras ou
  fases concluidas para propagar o aviso.
- Atualizar a fase para `Concluida`, registrar resultado e sincronizar
  `tarefa.md`.
- Criar commit contendo somente alteracoes da fase UX concluida.

Quando um ajuste pedido mudar o objetivo, criar comportamento real ou ampliar o
escopo para fora da fase UX, interromper e encaminhar revisao ao `planejador`.

### 3. Registrar resultado da fase

Usar no arquivo da fase:

```markdown
## Resultado
- Tela, fluxo ou componente entregue.
- Validacoes visuais/interativas realizadas com o usuario.
- Mocks, estados simulados e limites para integracao posterior.
- Artefatos reutilizaveis criados, se houver, com nome/caminho e como reaproveitar.
- Artefatos temporarios de UX que devem ser substituidos nas fases comuns.
```

O resultado deve deixar claro o que esta pronto para reaproveitamento e o que
ainda e apenas simulado.

### 4. Encerrar o bloco UX

Depois de concluir as fases UX aprovadas:

- apresentar o resultado agregado;
- listar telas/componentes criados ou alterados;
- informar verificacoes, validacoes do usuario, commits, mocks e limites;
- indicar quais fases comuns dependem desse resultado.

Nao encerrar a tarefa inteira. Encaminhar a proxima fase comum aprovada ao
`desenvolvedor`, respeitando dependencias. Se ainda houver ajustes visuais antes
da integracao, encaminhar revisao ao `planejador`.

## Retorno

Informar de forma curta:

- tarefa e fases UX executadas;
- resultado visual entregue;
- validacoes e verificacoes;
- commits criados;
- mocks e limites para integracao;
- estado do source control e alteracoes restantes.

## Proxima acao sugerida

Ao finalizar qualquer uso da skill, encerrar o retorno com
`Proxima acao sugerida:`.

A sugestao deve indicar uma unica proxima acao concreta: validar o resultado UX,
registrar ajustes no Planejador ou iniciar a proxima fase comum com o
`desenvolvedor`.

## Limites

- Nao executar fases comuns.
- Nao implementar backend real, persistencia ou regras de dominio.
- Nao substituir mocks por integracoes reais.
- Nao criar testes unitarios.
- Nao concluir fase sem aceite visual/interativo do usuario.
- Nao alterar conhecimento permanente.
- Nao misturar alteracoes nao relacionadas no commit da fase.
