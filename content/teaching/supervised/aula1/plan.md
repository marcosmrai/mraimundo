## Position in the Course

This lesson establishes the thesis that the remaining eleven lessons will elaborate: **every supervised algorithm is a distributional assumption, a likelihood, and a decision rule.** Lesson 1 makes all three visible at once, in the simplest possible setting — a single continuous feature on a bounded interval and two classes — so that later lessons can add dimensions, non-linearity, and optimization machinery without the student losing sight of the underlying structure.

The deliberate choice of a **one-dimensional** problem is what makes this possible: the decision boundary is a single number, the error probabilities are literal areas under two curves, and the trade-off between them can be drawn on the board rather than asserted.

---

## Prerequisites

Basic calculus (integration, change of variables), elementary probability (random variables, expectation, variance), and familiarity with Python and NumPy/SciPy. No prior exposure to machine learning is assumed.

---

## Required Reading

| Topic | Source | Section | Pages |
|---|---|---|---|
| Motivating screening example, Bayes' theorem | Bishop & Bishop (2024) | §2.1.1, §2.1.3–2.1.5 | 25–31 |
| Probability densities, normalization | Bishop & Bishop (2024) | §2.2, §2.2.1 | 32–34 |
| Beta distribution and its shapes | Bishop (2006) | §2.1.1 | 71–74 |
| Decision theory, misclassification rate | Bishop (2006) | §1.5, §1.5.1 | 38–41 |
| Expected loss and the reject option | Bishop (2006) | §1.5.2–1.5.3 | 41–42 |
| Misclassification rate (modern treatment) | Bishop & Bishop (2024) | §5.2.1–5.2.3 | 139–143 |
| Confusion matrix, precision, recall, FPR | Bishop & Bishop (2024) | §5.2.5 | 147–148 |
| ROC curve | Bishop & Bishop (2024) | §5.2.6 | 148–150 |

**Two notes on the sources.** First, the 2024 *Deep Learning* book does **not** cover the Beta distribution — Chapter 3 goes straight from Bernoulli and binomial to the multivariate Gaussian. All Beta material must come from PRML §2.1.1. Second, PRML introduces the Beta as a *conjugate prior over the parameter* \\(\mu\\) of a Bernoulli, not as a density over observed data. This lesson repurposes it as a data model for bounded observations \\(x \in [0,1]\\). The mathematics is identical; the interpretation is not, and the difference should be stated explicitly in class rather than glossed over.

---

## Content Sequence

Timings assume a single 100-minute session and should be treated as proportions, not commitments.

### Block 0 — Why probability comes first (10 min)

Open with the medical screening example (Bishop & Bishop, §2.1.1, pp. 25–26, revisited in §2.1.4, p. 30). A test with a 90% detection rate for a disease affecting 1 in 100 people, applied to a person who tests positive, gives a posterior probability of disease far lower than most students expect.

The pedagogical value is that **a classifier already exists before any algorithm is introduced.** Bayes' theorem alone converts a class-conditional model plus a prior into a decision. Everything that follows in the course is machinery for estimating those two ingredients when the problem is harder.

### Block 1 — From counts to densities (15 min)

Move from the discrete screening example to a continuous feature. Cover the normalization and non-negativity conditions (Bishop & Bishop, §2.2, pp. 32–33, eqs. 2.27–2.28) and insist on the distinction between a **density** and a **probability**: \\(p(x)\\) may exceed 1, only \\(\int p(x)\,dx\\) is constrained.

Then motivate the choice of support. Credit scores, default rates, click-through rates, proportions, and normalized measurements live in \\([0,1]\\). A Gaussian fitted to such data assigns positive mass outside the feasible region and produces thresholds that can fall outside the domain. **The support of the model is a modelling decision, not a technicality.**

### Block 2 — The Beta distribution (20 min)

Introduce \\(\text{Beta}(x \mid a, b)\\) (PRML eq. 2.13, p. 71), with its normalization via the Gamma function. Walk through the shape gallery in PRML Figure 2.2 (p. 72), which is the single most useful image of the lesson:

*   \\(a, b < 1\\) — U-shaped, mass concentrated at both endpoints
*   \\(a = b = 1\\) — uniform
*   \\(a, b > 1\\) — unimodal, with skew controlled by the ratio \\(a/b\\)

State the mean, variance, and mode (PRML Exercise 2.6, p. 129). Then address fitting honestly:

*   **Maximum likelihood has no closed form.** The stationarity conditions involve digamma functions and require numerical solution. Do not promise students a formula that does not exist.
*   **Method of moments does have one.** With sample mean \\(m\\) and sample variance \\(v\\) satisfying \\(v < m(1-m)\\):
    \\(\hat{a} = m\left(\frac{m(1-m)}{v} - 1\right)\\), \\(\hat{b} = (1-m)\left(\frac{m(1-m)}{v} - 1\right)\\).

This is a good first encounter with the idea that estimators differ, and that closed form and optimality are not the same property — a theme that returns in Lessons 5 and 7.

### Block 3 — One class: anomaly as a tail event (15 min)

Fit a Beta to *normal* observations only and define the exclusion region as a low-probability set — either a tail \\(\{x > t\}\\) or a level set \\(\{x : p(x) < \lambda\}\\). The threshold is then a **quantile of the fitted model**, and the false-alarm rate is \\(\alpha\\) by construction.

Then make the limitation explicit: **with a single fitted density, the Type II error is not defined.** There is no model of what an anomaly looks like, so the probability of missing one cannot be computed. Students routinely miss this. Stating it here is what motivates the next block rather than making it feel like a repetition.

### Block 4 — Two classes: overlapping densities (25 min)

Introduce class-conditional densities \\(p(x \mid \mathcal{C}_1) = \text{Beta}(x \mid a_1, b_1)\\) and \\(p(x \mid \mathcal{C}_2) = \text{Beta}(x \mid a_2, b_2)\\) with priors \\(\pi_1, \pi_2\\), and form the joints \\(p(x, \mathcal{C}_k)\\).

Reproduce the region argument of PRML Figure 1.24 (p. 40) on the board. As the boundary \\(\hat{x}\\) moves, the combined area of two of the error regions stays constant while a third shrinks to zero exactly when \\(\hat{x}\\) sits at the crossing point of the two joint curves — which is precisely the rule "assign \\(x\\) to the class with the larger posterior \\(p(\mathcal{C}_k \mid x)\\)" (PRML §1.5.1, pp. 39–41).

**Emphasize that Figure 1.24 plots joint distributions, not class-conditionals.** The area interpretation of the errors only works once the priors have been folded in. This is one of the most common sources of confusion in the entire lesson.

Both error probabilities are now well defined and, for the Beta, available in closed form through the regularized incomplete beta function \\(I_t(a,b)\\):

*   Type I (false positive): \\(P(x > t \mid \mathcal{C}_1) = 1 - I_t(a_1, b_1)\\)
*   Type II (false negative): \\(P(x \le t \mid \mathcal{C}_2) = I_t(a_2, b_2)\\)

Flag the terminological point: "Type I" and "Type II" are hypothesis-testing labels and require a designated null. In anomaly detection the null is "normal"; in a symmetric two-class problem the labelling is a convention that must be announced.

### Block 5 — Quantifying and trading off the errors (25 min)

Build the confusion matrix and define precision, recall, false positive rate, and false discovery rate (Bishop & Bishop, §5.2.5, eqs. 5.30–5.33, pp. 147–148). Use their own cautionary example: with 1 case in 1,000, a classifier that predicts "negative" for everyone reaches 99.9% accuracy and is useless. **Accuracy is not a scalar summary of a decision problem.**

Then sweep the threshold and trace the ROC curve (§5.2.6, pp. 148–150), presenting it as *the locus of achievable operating points for a fixed pair of fitted densities*. The curve is a property of the model; the point chosen on it is a property of the application.

Close the block by making the cost structure explicit:

*   **Expected loss** with an asymmetric loss matrix (PRML §1.5.2, p. 41; Bishop & Bishop §5.2.2, p. 140). The crossing condition becomes cost-weighted: the boundary satisfies \\(\pi_1 L_{12}\, p(t \mid \mathcal{C}_1) = \pi_2 L_{21}\, p(t \mid \mathcal{C}_2)\\), so raising the cost of a missed detection pushes the threshold in a predictable direction.
*   **The reject option** (PRML §1.5.3, p. 42; Bishop & Bishop §5.2.3, p. 142), as the admission that abstaining is sometimes the lowest-loss action.

### Block 6 — Closing and bridge (5 min)

The take-away to state in one sentence: **a decision threshold is not a hyperparameter to be tuned blindly — it is the solution to an optimization problem defined by the fitted densities, the priors, and the loss.**

Bridge to Lesson 2: everything here rested on one feature. With many features the class-conditional density becomes a high-dimensional object, and Naive Bayes is the first structural assumption introduced to make it estimable.

---

## Derivations to Carry Out on the Board

1.  **Normalization of the Beta distribution** (PRML Exercise 2.5, p. 128) — the change of variables through the Gamma function. Assign as reading rather than deriving in full if time is short.
2.  **Mean and variance of the Beta, then inversion to method-of-moments estimators** (PRML Exercise 2.6, p. 129). Short and gives the students a working estimator by the end of the class.
3.  **The minimum-misclassification boundary** as the crossing point of the joint densities (PRML eqs. 1.78–1.79, pp. 39–40).
4.  **How the boundary moves under an asymmetric loss matrix** — a two-line modification of derivation 3 that changes the practical answer completely.

---

## Computational Lab

A single notebook, run in the second half or assigned immediately after:

1.  Simulate (or load) a bounded feature for two populations; plot histograms against fitted Beta densities.
2.  Fit by method of moments and by numerical MLE (`scipy.stats.beta.fit`); compare the estimates and discuss the discrepancy.
3.  Compute Type I and Type II error rates analytically via `scipy.stats.beta.cdf` and verify them empirically by simulation.
4.  Sweep the threshold, plot the ROC curve, and mark three operating points: minimum total error, a fixed false-alarm budget of \\(\alpha = 0.05\\), and the minimum-expected-loss point under a 10:1 cost asymmetry.
5.  Repeat step 4 with a strongly imbalanced prior and observe how the optimal threshold and the ROC curve respond differently — the ROC is invariant to the class prior, the chosen operating point is not.

Step 5 is the intellectual pay-off of the lab and should not be cut.

---

## Suggested Exercises

*   **PRML 2.5** (p. 128) — normalization of the Beta.
*   **PRML 2.6** (p. 129) — mean, variance, and mode of the Beta.
*   **PRML 1.24** (p. 64) — minimum expected loss with a reject option, and the relationship between the rejection cost and the rejection threshold.
*   **Course exercise:** given two fitted Betas and a cost ratio, solve numerically for the optimal threshold and show it coincides with the tangency point on the ROC curve.

---

## Teaching Notes and Common Pitfalls

*   **Densities are not probabilities.** Expect at least one student to be troubled by a Beta density taking values above 1.
*   **Exact 0s and 1s break the Beta likelihood** when \\(a < 1\\) or \\(b < 1\\), since the density diverges at the endpoints. Real bounded data frequently contains exact zeros. Mention clipping and zero/one-inflated models as the honest fixes; do not let students discover this silently in the lab.
*   **The Beta-as-prior versus Beta-as-data-model distinction** (see the reading notes above) will confuse anyone who reads PRML §2.1.1 without warning.
*   **Joint versus class-conditional densities** in PRML Figure 1.24 — restate this at least twice.
*   **"Type I" and "Type II" require a designated null hypothesis.** Announce the convention before using the terms.
*   Resist the temptation to introduce the likelihood ratio formally here. It is the natural object, but it lands better in Lesson 2 once Bayes' theorem has been developed in the multidimensional setting.