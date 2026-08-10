# Progresso — Optimization and Linear Algebra for Machine Learning

Estrutura conforme `CLAUDE.md`: `index.md` é o planejamento do semestre
(formatado para Hugo, com link de cada aula pronta); cada aula é
`aulaNN/` com `00-plano-aula.md`, `01-fontes.md`, `02-aula.qmd`. Fontes em
`fontes/`: `mathml.pdf` (Deisenroth, Faisal & Ong — *Mathematics for
Machine Learning*, 2024), `copt.pdf` (Boyd & Vandenberghe — *Convex
Optimization*), `optml.pdf` (Wright & Recht — *Optimization for Data
Analysis*) — os dois últimos reservados para a Parte 2/3 do curso
(Aulas 6+), ainda não usados.

## Aula 1 — Vector Spaces, Norms, Inner Products, and Metrics

O `02-aula.qmd` já vinha pronto ("já está boa", nas palavras do usuário) —
esta sessão construiu a estrutura de apoio em volta dele, não reescreveu o
conteúdo, exceto por uma correção matemática pontual.

- [x] `00-plano-aula.md` — reconstruído a partir do `plan.md` anterior
      (que era uma colagem de conversa de chat, não um plano de aula) mais
      leitura completa do `.qmd` real. 6 blocos, ~125 min (acima da
      estimativa original de 90–120 min do `plan.md`, por causa de conteúdo
      que o plano não previa: prova da métrica do cosseno, Swiss Roll,
      duas luas, fechamento com RAG).
- [x] `01-fontes.md` — 7 fontes do `mathml.pdf`, todas com trecho literal
      já extraído (offset confirmado: **+6** entre página impressa e PDF,
      diferente do +20 usado nos livros de `supervised`). $k$-NN,
      variedades/manifolds e RAG não têm lastro no MathML — são
      contribuições de ML da própria aula, sinalizado explicitamente no
      arquivo, não fabricado como citação.
- [x] `02-aula.qmd` — **um erro matemático real corrigido nesta sessão**:
      a prova de que a distância do cosseno ($d_{\cos}=1-\cos\theta$)
      satisfaz a desigualdade triangular tinha um passo inválido (elevar
      ao quadrado uma desigualdade de raízes e concluir a versão não
      elevada). Contraexemplo verificado numericamente (vetores a
      $0°,90°,135°$): a desigualdade falha de fato. Corrigido para a
      conclusão certa — $\sqrt{2\,d_{\cos}}$ (distância cordal) é métrica;
      $d_{\cos}$ em si não é, em geral. Também removido um artefato de
      geração (`[cite: 3]` solto no texto). YAML corrigido: tinha
      `output-dir: "aula1"` por formato, que conflitava com a convenção do
      projeto (`_quarto.yml` já define `output-dir`/`output-file` no nível
      do projeto) — removido, mais `date`/`lang` adicionados para
      consistência com `supervised`. Validado com `quarto render --to html`
      e `--to revealjs`, sem erro.

**Pendências registradas em `01-fontes.md`** (não bloqueiam a aprovação,
mas valem revisão): produto interno usado no Bloco 5 sem definição formal
prévia no Bloco 4 (a Fonte 5, MathML §3.2.2, cobre isso mas ainda não foi
citada no texto); $L_\infty$ sem exemplo nomeado localizado no MathML.

## Etapa 5 — index.md

Link da Aula 1 corrigido: apontava para `../../algebra/aula1/livro.html`
(disciplina, pasta e nome de arquivo antigos/errados) — agora
`../../algebra_opt/aula01/notas.html` (+ Slides), mesmo padrão do
`supervised`. Mostrado no chat antes de aplicar.

## Aulas 2–15

Não iniciadas.
