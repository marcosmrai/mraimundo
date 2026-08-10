# Progresso — Supervised Learning

Estrutura conforme o `CLAUDE.md` atualizado em 2026-08-09: `index.md` é o
planejamento do semestre (formatado para Hugo); cada aula é `aulaNN/` com
`00-plano-aula.md` (resumo + plano de blocos), `01-fontes.md` (fontes com
trecho citado literalmente) e `02-aula.qmd` (aula final, dupla saída
HTML/RevealJS via `_quarto.yml`, que já define `output-file: notas.html` /
`slides.html` no nível do projeto). Fontes bibliográficas em `fontes/`:
`prml.pdf`, `dlfc.pdf`, `esl.pdf` (links simbólicos, já colocados pelo
usuário), mais `exemplos-estilo/exemplo.qmd` (symlink para `aula01/02-aula.qmd`,
aprovada, como referência de tom/estilo para novas aulas).

**Aprovado pelo usuário:** aulas podem ser mais longas que os 100 min de
referência — não é mais um item pendente de decisão, é o padrão aceito.

## Aula 1 — Data, Distributions, and Anomaly Detection

- [x] `00-plano-aula.md` — funde o antigo `resumo.md` + `plan.md`. Duas
      rodadas de ajuste já incorporadas (catálogo cortado, Beta
      simplificada, Blocos 6–7 fundidos, decisão ampliada). ~130 min.
- [x] `01-fontes.md` — 10 fontes, **todos os trechos preenchidos** com
      citação literal extraída de `prml.pdf`/`dlfc.pdf` (offset página
      impressa → PDF: **+20** para os dois livros, confirmado nos
      capítulos usados).
- [x] `02-aula.qmd` — revisado em 2026-08-09 (3 correções: texto vazado da
      geração, referência errada à Aula 4, mistura linear/quadrático no
      gradiente do outlier); depois reescrito para bater com o plano
      reconciliado. Validado com `quarto render --to html` e `--to
      revealjs`, sem erro. Backup do estado pré-revisão em `aula01/backup.md`.
- [x] Servindo de `fontes/exemplos-estilo/exemplo.qmd` (symlink).

## Aula 2 — Conditional Distributions and Generative Models

Reiniciada do zero nesta rodada (`02-aula.qmd`, `00-plano-aula.md` e
`01-fontes.md` anteriores descartados a pedido do usuário; o `index.qmd`
antigo continua recuperável do histórico do git, commit `a66e239`, se algum
dia necessário — não foi restaurado).

- [x] `00-plano-aula.md` — resumo + plano num único arquivo (formato pedido
      pelo usuário para esta aula). Blocos 5+6 do rascunho original foram
      fundidos durante o planejamento (razão de verossimilhanças e teoria
      da decisão são o mesmo objeto — percebido pelo usuário). ~130 min
      final (estimativa original de ~105 min não se sustentou).
- [x] `01-fontes.md` — 10 fontes obrigatórias + 1 opcional (grafo Naive
      Bayes), **todos os trechos preenchidos**. Achado não planejado: a
      Fonte 11 (PRML §8.2.2, p. 381) contém uma frase do próprio PRML que
      sustenta o argumento "classifica bem, estima mal" do Bloco 4 — a
      fonte externa Domingos & Pazzani (1997), que tinha sido descartada,
      acabou substituída por uma citação literal do PRML — **já inserida**
      no `02-aula.qmd`, ao final do Bloco 4.
- [x] `02-aula.qmd` — escrito nesta sessão. Matemática do Bloco 4 (condição
      de coincidência de fronteiras naive/plena) verificada numericamente
      antes de escrever o texto (cos exato = 1.0 no caso alinhado, ≈0.68
      no genérico; acurácia 0.8455 vs. 0.8443 vs. 0.993 vs. 0.892). Validado
      com `quarto render --to html` e `--to revealjs`, sem erro.

## Aula 3 — Decision Trees — Greedy Partitioning

- [ ] `00-plano-aula.md`
- [ ] `01-fontes.md`
- [ ] `02-aula.qmd`

Fonte adicional já disponível: `fontes/esl.pdf` (ESL) foi linkado pelo
usuário — cobre CART com mais profundidade que o PRML §14.4 (breve).
Ainda não decidido se ESL entra como leitura obrigatória ou só de apoio.

## Pendências gerais

- **Resolvido:** Etapa 5 feita para as Aulas 1 e 2 — `index.md` agora linka
  `../../supervised/aula01/notas.html` (+ Slides) e
  `../../supervised/aula02/notas.html` (+ Slides), no formato exigido pelo
  `CLAUDE.md`, com profundidade de caminho confirmada contra um exemplo já
  funcionando em `algebra_opt/index.md`. Trecho mostrado no chat antes de
  aplicar.
- **Resolvido:** pastas órfãs removidas — `content/teaching/supervised/aula1/`,
  `aula2/` (nomes antigos, pré-rename) e `static/supervised/aula1/`,
  `aula2/` (output antigo, incluindo um diretório `aula2/` com arquivos
  nunca rastreados pelo git). O output atual vive em
  `static/supervised/aula01/` e `aula02/`, cada um com `02-aula_files/`
  (nome derivado de `02-aula.qmd`, não mais `index_files/`).
- **Resolvido:** citação do PRML p. 381 adicionada ao final do Bloco 4 de
  `aula02/02-aula.qmd`; ambas as aulas re-renderizadas (`--to html` e
  `--to revealjs`) depois da mudança, sem erro.
- Formato do `00-plano-aula.md`: mantido mais elaborado que o esqueleto
  mínimo do `CLAUDE.md` (subseções, notas de reconciliação), por decisão
  explícita do usuário — não é uma divergência a corrigir.
- `fontes/exemplos-estilo/` resolvido com um symlink para `aula01/02-aula.qmd`
  — se a Aula 1 for revisada de novo, o exemplo atualiza automaticamente
  (é link, não cópia).
