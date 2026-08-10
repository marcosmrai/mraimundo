# Progresso — Computing and Society

Estrutura conforme `CLAUDE.md`: `index.md` é o planejamento do semestre;
cada aula é `aulaNN/` com `00-plano-aula.md`, `01-fontes.md`, `02-aula.qmd`.
Fontes em `fontes/`: `CSV1.pdf`, `CSV2.pdf`, `CSV3.pdf` (Maciel & Viterbo,
2020, 3 volumes), `EthEng.pdf` (Van de Poel & Royakkers, 2011), `EthTech.pdf`
(Steen, 2022).

**Diferença estrutural desta disciplina:** é humanidades/ética, não STEM.
Por decisão do usuário, o `.qmd` não usa chunks de código Python/simulação
— só prosa (HTML/RevealJS via `content-visible`) e diagramas Mermaid para
modelos conceituais. Sem `exemplos-estilo/` ainda (as outras disciplinas
são todas STEM; não fazem sentido como referência de tom aqui — considerar
usar a própria Aula 1 como exemplo depois de aprovada, como já feito nas
outras disciplinas).

## Achado importante: citação quebrada no `index.md`

A leitura recomendada original de **três aulas** (1, 7, 13) citava "Maciel
& Viterbo (2020), Vol. 2, Capítulo 2: Análise Cultural de Sistemas
Computacionais" — **capítulo que não existe**. Confirmado pelo sumário
real dos dois volumes: o Vol. 2 não tem Capítulo 2 (a numeração continua
do Vol. 1, começa no Cap. 9); o Capítulo 2 do Vol. 1 é sobre pós-graduação,
sem relação com o tema.

- **Corrigido no `index.md`** (a pedido explícito do usuário, que também
  autorizou usar `EthTech.pdf` como suporte adicional): substituído pelo
  Cap. 10 real do Vol. 2 ("Cultura na Prática da Computação", Salgado &
  Leitão, pp. 46–80) — mais próximo tematicamente — e adicionado Steen
  (2022), Cap. 3 "Is Technology a Neutral Tool?" como leitura
  complementar à Aula 1.
- **Aulas 7 e 13:** mesma citação quebrada, corrigida também (mesmo
  substituto), mas **sem verificar se o Cap. 10 de fato serve para essas
  aulas** — só resolvido o erro factual, não a adequação de conteúdo.
- **Achado extra, ainda não corrigido:** a leitura de Steen citada na
  Aula 7 ("Chapter 2: Ethics of Consequences") também parece errada — o
  Cap. 2 real do EthTech é "What do we mean with ethics?"; o mais próximo
  do título citado é o Cap. 9 "Consequences and outcomes" (p. 67).
  Sinalizado no `index.md`, não resolvido — assunto de quando chegarmos
  na Aula 7.

## Aula 1 — Computing as a Socio-Technical System

- [x] `00-plano-aula.md` — 5 blocos, **50 min** (não ~105 min como no
      rascunho inicial — correção de orçamento de tempo feita pelo
      usuário na segunda rodada). Núcleo: o mapa de atores (Van de Poel &
      Royakkers §1.6) recebeu o maior bloco (15 min) por ser o que a
      competência esperada do `index.md` pede de fato.
- [x] `01-fontes.md` — 8 fontes (Van de Poel & Royakkers Cap. 1 + Steen
      Cap. 3), todas com trecho literal extraído e verificado (offset de
      página confirmado por leitura direta, não assumido: +14 no EthEng,
      +9 no EthTech a partir do Cap. 3 — **atenção**, o offset do EthTech
      não é constante no livro inteiro, há uma página de abertura de
      parte não numerada que desloca o offset em 4 páginas em algum ponto
      antes do Cap. 3). Maciel & Viterbo Cap. 10 está na leitura
      recomendada mas **não foi lido** — o plano se sustentou inteiramente
      nas outras duas fontes.
- [x] `02-aula.qmd` — escrito nesta sessão, sem código Python (só prosa +
      2 diagramas Mermaid: mapa de atores recriando a Figura 1.6 de Van
      de Poel & Royakkers, e o *feedback loop* de algoritmos de redes
      sociais). Validado com `quarto render --to html` e `--to revealjs`,
      sem erro.

## Etapa 5 — index.md

Link da Aula 1 adicionado (não existia nenhum antes). Mesmo padrão das
outras disciplinas: `../../society/aula01/notas.html` (+ Slides).

## Aulas 2–15

Não iniciadas.
