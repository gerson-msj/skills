# Skills

Este repositorio gerencia conjuntos de skills. Ele e um projeto meta: as skills
contidas aqui sao conteudo versionado, nao instrucoes operacionais para este
proprio repositorio.

## Regras para agentes

Ao trabalhar neste repositorio:

- nao acione skills globais instaladas que apontem para diretorios deste
  repositorio;
- nao acione skills locais presentes nos conjuntos versionados aqui, como
  `Web01`;
- leia arquivos de skill apenas como fonte, documentacao ou objeto de edicao;
- ao responder perguntas sobre skills, consulte os arquivos relevantes e trate-os
  como fonte da verdade;
- trate mudancas neste repositorio como manutencao de conteudo de skills;
- nao misture diretorios de conjuntos de skills; ao trabalhar em um conjunto,
  manipule somente esse diretorio e ignore os demais ate haver pedido explicito;
- ao alterar uma skill, verifique as demais skills do mesmo diretorio para manter
  coerencia de fluxo, limites, responsabilidades e terminologia;
- nao remende uma skill com excecoes acumuladas; apos cada alteracao, mantenha o
  texto simples, direto e consistente, como se tivesse sido recem criado;
- escreva para modelos, nao para pessoas: use diretivas claras, baixo consumo de
  tokens e pouca redundancia;
- ao concluir uma alteracao, verifique se o `README.md` do diretorio da skill
  tambem precisa ser atualizado.

Se uma solicitacao mencionar uma skill deste repositorio, interprete a mencao
como referencia ao arquivo ou conjunto a ser mantido, salvo se o usuario pedir
explicitamente para testar o comportamento dessa skill em outro projeto.
