## Resumo — Aula 3: Árvores de Decisão — Particionamento Guloso

### Posição no curso

A Aula 2 fechou apontando uma limitação compartilhada por tudo que vimos
até aqui: tanto a fronteira gaussiana com covariância compartilhada quanto
o Naive Bayes decidem a **forma** da fronteira de decisão *antes* de olhar
para os dados — ela é sempre linear, por construção do modelo paramétrico
escolhido. Esta aula introduz uma família de modelos que inverte essa
lógica: árvores de decisão (CART) não assumem nenhuma forma paramétrica
para $p(\mathbf{x}\mid\mathcal{C}_k)$ — elas particionam recursivamente o
espaço de entrada em regiões, ajustando um modelo constante (a média, ou a
proporção de cada classe) dentro de cada uma. A aula reinterpreta esse
processo, que costuma ser ensinado como pura heurística ("escolha o split
que reduz mais a impureza"), como exatamente o mesmo princípio que já
sustentou o curso inteiro: **maximização de verossimilhança** — só que
aplicada a um modelo não-paramétrico (constante por partes) em vez de um
modelo paramétrico fixo.

### Pré-requisitos

Aulas 1–2 completas: densidades condicionais por classe, regra do
posterior máximo, teoria da decisão formal (função de perda, risco
posterior, regra de Bayes), Naive Bayes e o preço da suposição de
independência. Estimação por máxima verossimilhança para distribuições
categóricas e gaussianas (usada informalmente nas Aulas 1–2; formalizada
aqui via a derivação verificada nos Blocos 2–3). Não exige nada de
Cálculo além de encontrar o máximo de uma função de uma variável.

### Objetivos de aprendizagem

- **ML Concept:** O algoritmo CART para classificação e regressão.
- **Statistical Concept:** Estimação não-paramétrica da densidade
  condicional como função constante por partes. Medidas de impureza
  (Entropia e Gini) interpretadas como incerteza de distribuições
  categóricas, e splits entendidos como maximização gulosa de uma
  log-verossimilhança de perfil.
- **Objectives:** Reinterpretar particionamento recursivo como um
  procedimento de estimação não-paramétrica guiado por verossimilhança, em
  vez de uma heurística.
- **Expected Competencies:** Implementar CART, calcular ganhos de
  impureza, e justificar critérios de split em termos de maximização de
  log-verossimilhança.

*(fonte dos objetivos: `../index.md`, Lesson 3 — planejamento fixo do
semestre)*

### Fontes e uma decisão já tomada

Leitura principal: **PRML §14.4 "Tree-based Models"** (Bishop, 2006, pp.
663–666) — cobertura completa o suficiente para os objetivos desta aula
(árvores de regressão e classificação, critérios de impureza, poda por
custo-complexidade, limitações). **ESL Cap. 9, §9.2** (Hastie, Tibshirani
& Friedman) fica como leitura de apoio/opcional — decisão do usuário nesta
sessão —, citado só onde acrescentar profundidade que o PRML não cobre.

**Achado técnico verificado nesta sessão, antes de escrever a aula:** a
conexão "impureza = log-verossimilhança de perfil" não está explícita no
PRML — é a reformulação estatística que o objetivo da aula pede, e foi
**derivada e verificada numericamente** (script Python, não incluído na
aula) antes de ser incorporada:

1. **Classificação:** o MLE de uma distribuição categórica numa folha com
   contagens $n_{\tau k}$ é $\hat p_{\tau k} = n_{\tau k}/N_\tau$ (a
   proporção empírica) — verificado testando a log-verossimilhança em
   várias distribuições candidatas, o máximo bate com $\hat p_{\tau k}$.
   A log-verossimilhança maximizada é
   $\ell_\tau(\hat p_\tau) = N_\tau \sum_k \hat p_{\tau k}\ln\hat p_{\tau k} = -N_\tau H(\hat p_\tau)$,
   onde $H(p) = -\sum_k p_k\ln p_k$ é a entropia (com o sinal padrão).
   Logo, **maximizar a log-verossimilhança equivale a minimizar a
   entropia** — exatamente o critério de crescimento da árvore.
2. **Regressão:** sob um modelo gaussiano $t_n\mid\text{folha }\tau \sim
   \mathcal{N}(y_\tau, \sigma^2)$ com $\sigma^2$ fixo, o MLE de $y_\tau$ é
   a média amostral, e maximizar a log-verossimilhança equivale
   exatamente a minimizar $Q_\tau(T) = \sum (t_n - y_\tau)^2$ — a soma de
   quadrados residuais do PRML (eq. 14.30). Verificado numericamente com
   dados simulados.

::: {.callout-warning}
**Inconsistência encontrada na própria fonte (PRML, eq. 14.32).** O livro
escreve a "cross-entropy" da folha como
$Q_\tau(T) = \sum_k p_{\tau k}\ln p_{\tau k}$ (sem o sinal negativo
padrão da entropia) e então afirma, em prosa, que essa quantidade "vanish
for $p_{\tau k}=0,1$ and have a maximum at $p_{\tau k}=0.5$." Verificado
numericamente: a fórmula **como impressa** (sem o sinal) vale $0$ nas
bordas e é **mínima** (mais negativa) em $p=0.5$ — o oposto do que o
texto descreve. A descrição em prosa só bate com a entropia padrão $H(p)
= -\sum p\ln p$ (que *é* máxima em $p=0.5$). Não é uma errata que
localizei em fontes externas — é uma observação nossa, feita ao verificar
a matemática antes de escrever a aula. Nesta aula usamos a convenção
padrão (com o sinal negativo), que é a que faz a conexão com
log-verossimilhança funcionar e a que bate com a descrição em prosa do
próprio livro — mas o trecho citado em `01-fontes.md` preserva a fórmula
exatamente como impressa, sem "corrigi-la".
:::

### Exercícios (novo requisito do `CLAUDE.md`)

Esta é a primeira aula gerada depois da atualização do `CLAUDE.md`
(2026-08-17) que exige exercícios em toda aula. Planejar:

- **Notas (HTML):** seção de Exercícios ao final — pelo menos um exercício
  de cálculo manual de Gini/entropia num split pequeno, e um de
  implementação (completar uma função de split gulosa).
- **Slides (RevealJS):** pelo menos dois exercícios de checagem
  intercalados (ex.: "qual destas duas folhas tem menor entropia,
  sem calcular — só olhando as proporções?", com a solução no slide
  seguinte), além das figuras/derivações principais.

## Plano de aula — Aula 3 (carga horária estimada: ~110–120min, mesmo padrão de aulas mais longas já aceito nas Aulas 1–2)

### Bloco 0 — Abertura (5 min)

Recapitular a ponte da Aula 2: fronteiras gaussianas e Naive Bayes são
sempre lineares — a forma é decidida antes de ver os dados. Pergunta que
abre a aula: e se deixássemos os próprios dados decidirem a forma da
fronteira, sem suposição paramétrica alguma?

### Bloco 1 — Árvores como estimação não-paramétrica (15 min)

Partição recursiva do espaço de entrada em regiões cuboides
axis-aligned; cada região recebe um modelo constante (PRML, Fig.
14.5–14.6, o exemplo de 5 regiões e a árvore binária correspondente).
Interpretação central do bloco: isto é uma estimativa não-paramétrica de
$p(\mathbf{x}\mid\mathcal{C}_k)$ (ou de $\mathbb{E}[t\mid\mathbf{x}]$) como
função constante por partes — o oposto do que Naive Bayes e a gaussiana
faziam. O preço dessa liberdade é o assunto dos Blocos 4–5.

### Bloco 2 — Árvores de regressão: verossimilhança gaussiana (20 min)

Critério: $y_\tau = \frac{1}{N_\tau}\sum_{\mathbf{x}_n\in\mathcal{R}_\tau} t_n$
(PRML, eq. 14.29), soma de quadrados residuais $Q_\tau(T)$ (eq. 14.30).
Núcleo estatístico do bloco: derivar (com a verificação numérica já
feita) que isso é exatamente o MLE de um modelo gaussiano com média
constante por folha e variância compartilhada — a mesma equivalência
OLS $\leftrightarrow$ MLE que a Aula 5 vai formalizar para hiperplanos,
aqui aplicada a um modelo constante por partes. Crescimento guloso:
busca exaustiva sobre variável de split e limiar, porque a otimização
conjunta da estrutura inteira é combinatorialmente inviável (PRML, p.
665).

### Bloco 3 — Árvores de classificação: verossimilhança categórica, entropia e Gini (25 min)

Núcleo estatístico da aula. Derivar (com a verificação numérica já
feita) que o MLE categórico numa folha é a proporção empírica
$\hat p_{\tau k}$, e que maximizar a log-verossimilhança resultante
equivale a **minimizar a entropia** $H(\hat p_\tau)$ — reformulação
estatística do critério "cross-entropy" do PRML (eq. 14.32), com a nota
de precisão sobre o sinal já registrada acima. Apresentar o **índice de
Gini** (eq. 14.33) como alternativa, com sua própria interpretação —
a taxa de erro esperada de um classificador que sorteia rótulos segundo
$p_\tau$ e compara contra outro sorteio independente da mesma
distribuição — sem forçar a mesma conexão de verossimilhança (Gini não é
um MLE de forma tão direta quanto a entropia). Comparar com a taxa de
erro de classificação bruta: por que ela não é usada para *crescer* a
árvore (não-diferenciável, menos sensível a mudanças nas probabilidades
dos nós) mas é preferida para *podar* (PRML, p. 666).

### Bloco 4 — Poda e o critério de custo-complexidade (20 min)

Por que não parar de crescer a árvore cedo, mesmo quando um split não
reduz o erro: empiricamente, um split "inútil" pode habilitar um split
seguinte muito bom — argumento míope da busca gulosa (PRML, p. 665).
Prática recomendada: crescer uma árvore grande, depois podar. Critério
de custo-complexidade $C(T) = \sum_\tau Q_\tau(T) + \lambda|T|$ (eq.
14.31), $\lambda$ escolhido por validação cruzada — ponte direta com a
Aula 4 (Model Selection and Resampling), que vem logo a seguir no curso
e vai formalizar exatamente esse tipo de escolha.

### Bloco 5 — Limites e fechamento (10–15 min)

Duas limitações que o PRML nomeia explicitamente (p. 666): (1) splits
axis-aligned podem ser muito subótimos para fronteiras que não se alinham
aos eixos — uma fronteira a 45° (o próprio caso de covariância
compartilhada não-diagonal da Aula 2!) precisaria de muitos splits para
ser aproximada, enquanto a gaussiana da Aula 2 a captura em uma única
direção; (2) instabilidade — pequenas mudanças nos dados de treino podem
produzir uma estrutura de árvore bem diferente; (3) partição rígida —
cada ponto pertence a exatamente uma folha, produzindo previsões
descontínuas, particularmente ruim para alvos de regressão suaves.
Fechamento: a mesma liberdade que permite à árvore capturar qualquer
fronteira também a torna instável e gulosamente míope — **nenhum dos dois
extremos (sempre linear vs. totalmente livre) é gratuito.** Ponte para a
Aula 4: como escolher a complexidade certa ($\lambda$, profundidade
máxima) é uma instância do problema geral de seleção de modelo e
validação cruzada — e ponte de mais longo alcance para a Aula 9
(Ensemble Theory): a instabilidade que aqui é uma fraqueza da árvore
isolada é exatamente o que torna o *bagging* eficaz mais adiante no
curso.
