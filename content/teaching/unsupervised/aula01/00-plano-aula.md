## Resumo — Aula 1: Data Space, Parametric Generative Models, and Anomalies

Esta é a primeira aula do curso, e a primeira vez que os alunos veem
aprendizado **sem rótulo algum** — nem implícito. A pergunta central é: o
que significa "modelar dados" quando não há $y$ para prever? A resposta
desta aula é a mais simples possível: assumir que os dados foram gerados
por uma distribuição teórica conhecida (Gaussiana multivariada), ajustá-la
por máxima verossimilhança, e usar a verossimilhança de um ponto novo sob
esse modelo para decidir se ele é típico ou anômalo. A aula generaliza a
lógica de limiar-por-quantil (familiar de detecção de anomalias
unidimensional) para $d$ dimensões via distância de Mahalanobis, e fecha
com a identidade exata que torna o limiar rigoroso: a distância de
Mahalanobis ao quadrado de um ponto gaussiano segue qui-quadrado com $d$
graus de liberdade.

**Pré-requisitos:** probabilidade básica (vetor aleatório, média, matriz de
covariância), álgebra linear básica (inversa e determinante de matriz,
formas quadráticas). Nenhuma aula anterior do curso — é a Aula 1.

**Objetivos de aprendizagem** (do `index.md`, Lesson 1):
- **ML Concept:** O que significa "modelar dados" sem rótulos; *profiling*
  para identificar comportamentos atípicos.
- **Statistical Concept:** Distribuição empírica vs. teórica; assumir que
  os dados foram gerados por uma distribuição teórica conhecida (Gaussiana
  multivariada); usar a verossimilhança de um ponto sob o modelo ajustado
  para definir regiões de exclusão estatística.
- **Objectives:** Entender como ajustar distribuições teóricas a dados não
  rotulados e usar verossimilhança para detecção de anomalias.
- **Expected Competencies:** Ajustar uma Gaussiana multivariada a dados e
  definir limiares de anomalia robustos, baseados em probabilidade.

## Plano de aula — Aula 1 (carga horária: ~110min)

1.  **Abertura: modelar dados sem rótulos** (~10 min) — Contraste explícito
    com aprendizado supervisionado: não há $y$, só $\mathbf{x}_1,\dots,\mathbf{x}_N$.
    A pergunta deixa de ser "que função prever" e passa a ser "que forma
    esses dados têm". *Profiling*: descrever o comportamento típico de uma
    população para depois reconhecer o que se desvia dele (fraude, falha de
    sensor, transação suspeita).

2.  **Distribuição empírica vs. teórica** (~15 min) — O histograma/a
    distribuição empírica $\hat{p}(\mathbf{x})$ é sempre calculável, mas é
    ruidosa e não generaliza para pontos não vistos. A aposta desta aula:
    assumir que os dados vieram de uma família teórica conhecida (Gaussiana
    multivariada) troca ruído por estrutura — ao custo de a suposição poder
    estar errada. Motivar com um exemplo 2D (ex.: duas medidas de sensores
    correlacionadas) antes de formalizar.

3.  **A Gaussiana Multivariada: forma e parâmetros** (~20 min) — Definição
    $\mathcal{N}(\mathbf{x}\mid\boldsymbol\mu,\Sigma)$, papel geométrico de
    $\boldsymbol\mu$ (centro) e $\Sigma$ (forma/orientação das elipses de
    densidade constante — autovalores/autovetores de $\Sigma$). Por que é a
    escolha natural como *default*: Teorema Central do Limite, e é a
    distribuição de máxima entropia dada média e covariância fixas (citar,
    não provar em detalhe nesta aula).

4.  **Ajuste por Máxima Verossimilhança** (~15 min) — Derivar
    $\hat{\boldsymbol\mu} = \bar{\mathbf{x}}$,
    $\hat\Sigma = \frac{1}{N}\sum_n(\mathbf{x}_n-\bar{\mathbf{x}})(\mathbf{x}_n-\bar{\mathbf{x}})^T$
    maximizando a log-verossimilhança. Armadilha prática a anunciar: $\hat\Sigma$
    só é invertível se $N > d$ (mais amostras que dimensões) — antecipa a
    maldição da dimensionalidade da Aula 2.

5.  **Da Verossimilhança à Distância de Mahalanobis** (~20 min) — Mostrar
    que comparar $p(\mathbf{x})$ com um limiar é equivalente a comparar a
    forma quadrática do expoente,
    $D_M(\mathbf{x})^2 = (\mathbf{x}-\hat{\boldsymbol\mu})^T\hat\Sigma^{-1}(\mathbf{x}-\hat{\boldsymbol\mu})$,
    com um limiar — a **distância de Mahalanobis**. Diferença crucial com a
    distância Euclidiana: Mahalanobis "estica" o espaço pelas direções de
    baixa variância, então dois pontos igualmente distantes em Euclidiana
    podem ter distâncias de Mahalanobis muito diferentes se um está ao
    longo do eixo de alta correlação e outro não.

6.  **Limiares de Anomalia via Qui-Quadrado** (~20 min) — O resultado que
    fecha a aula com rigor: se $\mathbf{x}\sim\mathcal{N}(\boldsymbol\mu,\Sigma)$,
    então $D_M(\mathbf{x})^2 \sim \chi^2_d$. Isso dá um limiar exato,
    $t_\alpha = \chi^2_{d,1-\alpha}$, com taxa de alarme falso $\alpha$ por
    construção — a generalização direta, para $d$ dimensões com covariância,
    do limiar por quantil já visto em uma dimensão. Visualizar: elipses de
    contorno em 2D nos quantis de $\chi^2_2$, pontos fora marcados como
    anomalia.

7.  **Armadilhas e Ponte para a Aula 2** (~10 min) — O que pode quebrar
    tudo: (a) dados genuinamente multimodais (duas populações distintas)
    não são bem descritos por uma única Gaussiana — o ajuste "funciona"
    matematicamente e mesmo assim mente; (b) outliers no próprio conjunto
    de ajuste contaminam $\hat{\boldsymbol\mu}$ e $\hat\Sigma$, then inflam
    o limiar e escondem exatamente o que se queria detectar (problema de
    robustez, não resolvido aqui). Ponte: a saída não-paramétrica — $k$-NN
    e KDE — é o assunto da Aula 2.
