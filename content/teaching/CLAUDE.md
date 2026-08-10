# Fluxo de trabalho — geração de aulas

Este projeto é a pasta `teaching/`, que contém MÚLTIPLAS disciplinas,
cada uma em sua própria subpasta na raiz (ex: `supervised/`,
`algebra_opt/`). Este `CLAUDE.md` vale para todas elas.

Este projeto segue um processo de checkpoints POR AULA, com aprovação
humana obrigatória em cada etapa. NUNCA pule uma etapa, NUNCA gere a
etapa seguinte sem que o usuário tenha sinalizado aprovação explícita
(ex: "pode seguir", "próxima etapa", "ok").

O planejamento do semestre (`<disciplina>/planejamento-semestre.md`) é
FIXO. Use-o apenas como referência para identificar tema, objetivos de
aprendizagem e carga horária de cada aula — não proponha alterações nele.

---

## Estrutura de pastas

```
teaching/
├── CLAUDE.md
├── supervised/
│   ├── index.md
│   ├── fontes/
│   │   └── exemplos-estilo/
│   ├── progresso.md
│   ├── aula01/
│   │   ├── 00-plano-aula.md
│   │   ├── 01-fontes.md
│   │   └── 02-aula.qmd
│   ├── aula02/
│   └── ...
├── algebra_opt/
│   ├── index.md
│   ├── fontes/
│   ├── progresso.md
│   ├── aula01/
│   └── ...
└── ...
```

Cada disciplina é autocontida na sua subpasta da raiz. Cada aula é uma
subpasta própria dentro da disciplina, nomeada `aulaNN` (`aula01`,
`aula02`, ...). O arquivo index.md tem o planejamento do semestre em md (formatado para hugo).

---

## Etapa 0 — Identificar a disciplina (OBRIGATÓRIA, toda sessão)

Antes de ler, editar ou gerar qualquer arquivo, é preciso saber em qual
subpasta de disciplina trabalhar nesta sessão.

- Se o usuário já declarou a disciplina na mensagem (ex: "Disciplina:
  supervised" ou "trabalhando em algebra_opt"), usar essa subpasta e
  confirmar em uma linha antes de prosseguir.
- Se não declarou e houver mais de uma subpasta de disciplina na raiz,
  **perguntar qual é a disciplina da sessão** antes de qualquer outra
  ação. Não adivinhar pela última disciplina usada em sessões
  anteriores — o estado pode ter mudado.
- Se o workspace aberto já é a subpasta de uma única disciplina (ex:
  VS Code aberto direto em `supervised/`, não em `teaching/`), essa é
  a disciplina — não perguntar.

Todos os caminhos de arquivo nas etapas abaixo (`index.md`,
`fontes/`, `aulaNN/`, `progresso.md`) são relativos à subpasta da
disciplina identificada nesta etapa, não à raiz `teaching/`.

---

## Formato do arquivo de aula

Cada aula é um **único arquivo `.qmd`**, não um par separado de slides
e notas. O mesmo arquivo produz duas saídas (HTML e RevealJS) via
blocos `::: {.content-visible when-format="..."}`:

- **HTML** (`unless-format="revealjs"`): prosa corrida, completa,
  com as provas/derivações por extenso, citações de página do livro,
  avisos de leitura e notas de rodapé pedagógicas.
- **RevealJS**: versão condensada em bullets/fragmentos (`. . .`,
  `::: {.fragment}`), sem prosa longa, para uso em sala.

Código Python (ou R) é embutido nos mesmos chunks, gerando as figuras
que ilustram tanto a versão HTML quanto a RevealJS. Siga o padrão do
arquivo de referência em `fontes/exemplos-estilo/`:

- Um único bloco de **setup global** no topo (imports, seed do RNG,
  paleta de cores fixa reutilizada em toda a aula, funções auxiliares).
- Chunks com `#| echo: false` e `#| fig-align: center` para as figuras.
- Numeração de blocos/seções consistente com a numeração usada no
  planejamento do semestre.
- Avisos de leitura (`::: {.callout-warning}`, `::: {.callout-note}`,
  `::: {.callout-important}`) quando a interpretação do curso diverge
  da referência bibliográfica, ou quando há uma armadilha prática
  conhecida (ex: zeros exatos quebrando uma verossimilhança).

**Nomes de arquivo de saída:** o `index.md` da disciplina espera os
nomes `notas.html` (saída HTML) e `slides.html` (saída RevealJS) — ver
Etapa 5. Definir isso explicitamente no YAML do `.qmd` com
`output-file`, já que o padrão do Quarto usaria o nome do próprio
`.qmd` para ambos os formatos:

```yaml
format:
  html:
    output-file: notas.html
  revealjs:
    output-file: slides.html
```

## Preview local da aula

Para visualizar a aula renderizada durante a edição, sem abrir
navegador automaticamente e num processo isolado por porta (útil para
ter várias aulas em preview simultâneo), usar:

```bash
uv run quarto preview <disciplina>/aulaNN/02-aula.qmd --to html --port 4200 --no-browser
```

Ajustar `--to` para `revealjs` ao querer visualizar a versão de
slides, e `--port` para evitar conflito quando houver mais de um
preview aberto ao mesmo tempo (ex: `4200` para a aula em edição,
`4201` para uma aula anterior aberta para comparação).

## Sugestão de fluxogramas e diagramas

Ao montar o bloco, se o conteúdo tiver estrutura sequencial, uma árvore
de decisão, um processo com ramificações, ou uma comparação de
caminhos alternativos (ex: "três saídas honestas para um problema"),
**proponha um diagrama Mermaid** (` ```{mermaid} ` ), sem esperar o
usuário pedir. Use Mermaid porque renderiza nativamente em Quarto nos
dois formatos de saída (HTML e RevealJS). Só pergunte se não estiver
claro que o diagrama ajuda mais do que texto.

---

## Para cada aula (repetir o ciclo)

### 1. Identificar a aula no planejamento
Consultar `index.md` e confirmar com o usuário o tema,
objetivos e carga horária da aula NN. Não seguir sem confirmação.

### 2. Plano de aula (resumo + estrutura)
Gerar `aulaNN/00-plano-aula.md`, contendo:

- **Resumo** (5-10 linhas): o que a aula cobre, objetivos de
  aprendizagem, pré-requisitos (conferindo com o que já foi dado nas
  aulas anteriores aprovadas).
- **Plano de aula**: sequência de blocos/tópicos na ordem em que serão
  apresentados, com tempo estimado por bloco (somando à carga horária
  da aula) e a lógica de transição entre eles (ex: "Bloco 1 termina
  com uma pergunta sem resposta, que o Bloco 2 resolve").

Formato:

```markdown
## Resumo — Aula N

[5-10 linhas: cobertura, objetivos, pré-requisitos]

## Plano de aula — Aula N (carga horária: XXmin)

1. **[Nome do bloco]** (~XX min) — [o que cobre, por que vem aqui]
2. **[Nome do bloco]** (~XX min) — [o que cobre, como conecta com o anterior]
...
```

**PARAR** e esperar aprovação/edição do usuário.

### 3. Fontes — com trecho citado literalmente
Gerar `aulaNN/01-fontes.md` listando cada fonte usada, com:
- referência (livro, capítulo, seção, páginas);
- **o uso pretendido** daquele trecho na aula;
- **o trecho citado literalmente**, extraído do PDF/slide antigo —
  nunca reescrito de memória ou paraphraseado nesta etapa, para que a
  checagem do usuário seja direta.

Formato:

```markdown
## Fontes usadas — Aula N

### Fonte 1: PRML, §1.5.1, pp. 39-41
**Uso pretendido:** prova de que o cruzamento das conjuntas minimiza
o erro esperado.

**Trecho:**
> "the smallest probability of misclassification is achieved if
> each value of x is assigned to the class for which the joint
> probability p(x, Ck) is largest..."

---

### Fonte 2: DLFC, §2.1.1, pp. 25-26
**Uso pretendido:** exemplo de triagem médica (Bayes discreto).

**Trecho:**
> [trecho copiado literalmente do PDF]
```

**PARAR** e esperar aprovação/edição do usuário.

**Fontes como link simbólico:** os arquivos em `fontes/` podem ser
links simbólicos apontando para os PDFs/slides originais em outro
lugar do disco (ex: `ln -s ../../livros/prml.pdf fontes/prml.pdf`).
Leia-os normalmente pelo caminho dentro de `fontes/` — não há
tratamento especial necessário. Prefira links relativos, para o
projeto continuar funcionando se a pasta for movida.

### 4. Montar a aula completa
Gerar `aulaNN/02-aula.qmd`: arquivo único com saída dupla
HTML/RevealJS, código Python embutido, seguindo o estilo descrito
acima, o tom do(s) arquivo(s) de referência em `fontes/exemplos-estilo/`,
e a estrutura de blocos definida em `00-plano-aula.md`. Incluir
diagramas Mermaid onde fizer sentido (ver seção acima). **PARAR.**

### 5. Atualizar o `index.md` da disciplina
Após o usuário aprovar `02-aula.qmd` (fim da Etapa 4), propor a
atualização do `index.md` da disciplina — um markdown para Hugo com o
planejamento geral, que contém a lista de aulas com links.

Adicionar (ou atualizar, se a aula já tinha uma entrada anterior) uma
linha no formato:

```markdown
* **[Lesson N: <título da aula>](../../<disciplina>/aulaNN/notas.html)** ([Slides](../../<disciplina>/aulaNN/slides.html))
```

onde `<título da aula>` vem do plano de aula aprovado em
`00-plano-aula.md`, e `<disciplina>` e `aulaNN` seguem a estrutura de
pastas do projeto. Ajustar a profundidade do caminho relativo
(`../../`) conforme a posição real do `index.md` em relação à pasta da
aula — confirmar isso olhando a estrutura de pastas real antes de
propor o link, em vez de assumir a mesma profundidade do exemplo.

**Esta é uma edição de um arquivo já existente, não a criação de um
arquivo novo — por isso o mesmo cuidado das etapas anteriores não
basta.** Antes de escrever no `index.md`:

1. Mostrar no chat o trecho exato que será alterado/adicionado (a
   linha nova ou o antes/depois, se for uma atualização).
2. Esperar confirmação explícita do usuário.
3. Só então aplicar a edição no arquivo.

Se o usuário pedir para regenerar `02-aula.qmd` depois de já ter uma
entrada no `index.md` (ex: reaprovação de uma versão revisada), tratar
a atualização do link/título da mesma forma — propor, mostrar, esperar
aprovação.

### 6. Avançar
Só gerar a aula N+1 quando o usuário disser algo como "próxima aula"
ou "continuar".

---

## Continuidade entre aulas

Antes de gerar uma aula nova, reler os planos de aula e `.qmd` das
aulas anteriores já aprovadas, para manter notação, nível de
formalismo e progressão consistentes — e para não repetir conteúdo já
coberto.

## Precisão de conteúdo técnico

Ao lidar com conteúdo matemático/estatístico, sinalizar explicitamente
quando algo estiver sendo inferido ou generalizado a partir do livro,
em vez de copiado fielmente — especialmente em provas, propriedades
estatísticas, e afirmações sobre otimalidade.

## Registro de estado

Sempre atualizar `progresso.md` marcando a aula atual e o que já foi
aprovado nela (plano de aula / fontes / aula completa).