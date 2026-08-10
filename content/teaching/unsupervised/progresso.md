# Progresso — Unsupervised Learning

Estrutura conforme `CLAUDE.md`: `index.md` é o planejamento do semestre;
cada aula é `aulaNN/` com `00-plano-aula.md`, `01-fontes.md`, `02-aula.qmd`.
Fontes em `fontes/`: `prml.pdf`, `dlfc.pdf`, `esl.pdf` (mesmos links de
`supervised`), mais `exemplos-estilo/exemplo.qmd` (symlink para
`aula01/02-aula.qmd`).

## Aula 1 — Data Space, Parametric Generative Models, and Anomalies

Construída do zero nesta sessão — não havia nada além do `index.md`.

- [x] `00-plano-aula.md` — 7 blocos, ~120 min. O Bloco 6 foi reescrito a
      partir do feedback do usuário: o rascunho original só definia um
      limiar fixo (dentro/fora); a versão final trata o escore de anomalia
      como um **$p$-valor** (via $\chi^2_d$ da distância de Mahalanobis), e
      contrasta a versão conjunta com a versão por-dimensão sob suposição
      de independência (combinada pelo teste de Fisher, $\chi^2_{2d}$) — o
      mesmo trade-off do Naive Bayes, agora em teste de hipótese.
- [x] `01-fontes.md` — 7 fontes do PRML (Gaussiana multivariada,
      Mahalanobis, MLE, viés do estimador de covariância, restrição a
      $\Sigma$ diagonal), todas com trecho literal extraído e offset
      confirmado (+20). **DLFC não localizado** para os tópicos desta aula
      dentro do esforço da sessão — fica pendente se algum dia quiser o
      par completo. Dois resultados centrais do Bloco 6 (distribuição
      qui-quadrado da distância de Mahalanobis; teste combinado de Fisher)
      **não têm citação de livro** — são estatística multivariada clássica,
      derivados e verificados na sessão, não copiados de fonte alguma.
- [x] `02-aula.qmd` — escrito nesta sessão. Núcleo: dois pontos construídos
      via decomposição espectral de $\hat\Sigma$ (B: 2 desvios ao longo do
      autovetor de maior variância; C: 3 desvios ao longo do de menor
      variância) para ilustrar o contraste pedido pelo usuário — **B**
      tem $p$-valor conjunto alto (0,135) mas seria um falso alarme pelo
      teste por dimensão (Fisher $p=0{,}019$); **C** tem $p$-valor conjunto
      baixo (0,011, anomalia real) mas passaria batido pelo teste por
      dimensão ($p=0{,}539$). Verificado com um script Python independente
      antes de confiar no render, não só no código do próprio `.qmd`. Um
      bug de renderização corrigido: `\boldsymbol` dentro de `ax.text()` do
      matplotlib não é suportado pelo mathtext (diferente do MathJax usado
      no resto do documento) — trocado por `\hat\mu` simples nesse ponto
      específico. Validado com `quarto render --to html` e `--to
      revealjs`, sem erro; 2 diagramas Mermaid presentes no HTML final.

## Etapa 5 — index.md

Link da Aula 1 adicionado (não existia nenhum antes — só texto em negrito
sem link): `../../unsupervised/aula01/notas.html` (+ Slides), mesmo padrão
das outras disciplinas. Mostrado no chat antes de aplicar.

## Aulas 2–12

Não iniciadas.
