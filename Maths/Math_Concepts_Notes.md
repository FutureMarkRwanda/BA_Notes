# Refined Notes on Required Topics and Formulas


## 1. Complex Numbers

### Representations

* **Rectangular Form**: $z = a + bi$, with $a \in \mathbb{R}$, $b \in \mathbb{R}$.
* **Polar Form**: $z = r(\cos \theta + i \sin \theta)$, where

  * $r = |z| = \sqrt{a^2 + b^2}$ (modulus)
  * $\theta = \arg(z) = \tan^{-1}(b/a)$ (adjust for correct quadrant)
* **Exponential Form**: $z = re^{i\theta}$, via Euler's formula: $e^{i\theta} = \cos \theta + i \sin \theta$
* **Conversions**:

  * Rectangular → Polar: $r = \sqrt{a^2 + b^2},\ \theta = \tan^{-1}(b/a)$
  * Polar → Rectangular: $a = r\cos \theta, b = r\sin \theta$

### Operations

* **Addition/Subtraction**: Add real and imaginary parts directly.
* **Multiplication**: Expand using distributive property or convert to polar and use:

  $$
  z_1 z_2 = r_1 r_2 e^{i(\theta_1 + \theta_2)}
  $$
* **Division**:

  $$
  \frac{z_1}{z_2} = \frac{r_1}{r_2} e^{i(\theta_1 - \theta_2)}
  \quad \text{or use conjugate:} \quad \frac{a + bi}{c + di} = \frac{(a + bi)(c - di)}{c^2 + d^2}
  $$
* **Conjugate**: $\overline{z} = a - bi$; $|z|^2 = z\overline{z}$

### De Moivre’s Theorem & Roots

* **Powers**: $z^n = r^n [\cos(n\theta) + i\sin(n\theta)]$
* **n-th Roots**:

  $$
  z_k = r^{1/n} \left[ \cos\left( \frac{\theta + 2k\pi}{n} \right) + i \sin\left( \frac{\theta + 2k\pi}{n} \right) \right],\ k = 0,1,...,n-1
  $$

### Roots of Unity

* $z^n = 1 \Rightarrow \omega_k = e^{2k\pi i/n}$, $k = 0, 1, ..., n-1$
* These lie on the unit circle and form a regular polygon in the complex plane.
* Their sum is 0 for $n \geq 2$.

### Trigonometric Identities

* $\cos(n\theta) = \Re[(\cos \theta + i \sin \theta)^n]$
* $\sin(n\theta) = \Im[(\cos \theta + i \sin \theta)^n]$

### Solving Equations

* **Quadratics**: Use the standard formula; roots may be complex.
* **Higher-degree polynomials**: Use factorization, De Moivre, or substitution.
* **Sum and Product of Roots** (Cubic): For $az^3 + bz^2 + cz + d = 0$,

  * Sum: $z_1 + z_2 + z_3 = -\frac{b}{a}$
  * Product: $z_1 z_2 z_3 = -\frac{d}{a}$

---

## 2. Circuit Analysis

### Impedance

* **Impedance in AC circuits**: $Z = R + j(X_L - X_C)$

  * $X_L = \omega L$ (inductive reactance)
  * $X_C = \frac{1}{\omega C}$ (capacitive reactance)
* **Magnitude**: $|Z| = \sqrt{R^2 + (X_L - X_C)^2}$
* **Phase Angle**: $\phi = \tan^{-1} \left( \frac{X_L - X_C}{R} \right)$

### Resonance

* Occurs when $X_L = X_C \Rightarrow \omega = \frac{1}{\sqrt{LC}}$
* At resonance:

  * $Z = R$
  * Current is maximum
  * Circuit behaves as a purely resistive one

### Capacitance

* From $X_C$: $C = \frac{1}{\omega X_C}$

---

## 3. Binomial Expansion

* **Theorem**: $(x + y)^n = \sum_{j=0}^n \binom{n}{j} x^j y^{n-j}$
* **Binomial Coefficient**: $\binom{n}{j} = \frac{n!}{j!(n-j)!}$

---

## 4. Probability

### Basic Rules

* $P(A') = 1 - P(A)$
* $P(A \cup B) = P(A) + P(B) - P(A \cap B)$
* $P(A \cap B) = P(A) P(B|A)$

  * If independent: $P(A \cap B) = P(A)P(B)$
* **Bayes’ Theorem**:

  $$
  P(A|B) = \frac{P(B|A)P(A)}{P(B)} \quad \text{where} \quad P(B) = \sum P(B|A_i)P(A_i)
  $$

### Discrete Distributions

* **Binomial**:

  * $P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}$
  * $E(X) = np,\quad \operatorname{Var}(X) = np(1-p)$
* **Poisson**:

  * $P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}$
  * $E(X) = \operatorname{Var}(X) = \lambda$

---

## 5. Random Variables

### Discrete

* **PMF**: $\sum p(x) = 1$
* **Expected Value**: $E(X) = \sum x p(x)$
* **Variance**: $\operatorname{Var}(X) = E(X^2) - [E(X)]^2$
* **Transformations**:

  * $E(aX + b) = aE(X) + b$
  * $\operatorname{Var}(aX + b) = a^2 \operatorname{Var}(X)$
* **CDF**: $F(x) = \sum_{k \leq x} p(k)$

### Continuous

* **PDF**: $\int_{-\infty}^{\infty} f(x) dx = 1$
* $P(a < X < b) = \int_a^b f(x) dx$
* $E(X) = \int_{-\infty}^{\infty} x f(x) dx$
* $\operatorname{Var}(X) = \int x^2 f(x) dx - [E(X)]^2$
* **CDF**: $F(x) = \int_{-\infty}^x f(t) dt$

### Common Distributions

* **Normal Distribution**:

  * Standard: $Z \sim N(0,1)$
  * General: $X \sim N(\mu, \sigma^2) \Rightarrow Z = \frac{X - \mu}{\sigma}$
* **Uniform Distribution**:

  * $f(x) = \frac{1}{b-a}$, $x \in [a, b]$
  * $E(X) = \frac{a+b}{2},\ \operatorname{Var}(X) = \frac{(b-a)^2}{12}$

---

## 6. Inferential Statistics

### Sampling Distributions

* **Mean**: $\mu_{\bar{X}} = \mu$
* **Standard Error**: $\sigma_{\bar{X}} = \frac{\sigma}{\sqrt{n}}$
* **Shape**: Normal if population is normal or $n \geq 30$ (CLT)

### Confidence Intervals

* **Mean, $\sigma$ known**:

  $$
  \bar{X} \pm z_{\alpha/2} \cdot \frac{\sigma}{\sqrt{n}}
  $$
* **Mean, $\sigma$ unknown**:

  $$
  \bar{X} \pm t_{\alpha/2, n-1} \cdot \frac{s}{\sqrt{n}}
  $$
* **Proportion**:

  $$
  \hat{p} \pm z_{\alpha/2} \cdot \sqrt{ \frac{\hat{p}(1 - \hat{p})}{n} }
  $$
* **Sample Size**:

  $$
  n = \left( \frac{z_{\alpha/2} \sigma}{E} \right)^2
  $$

### Hypothesis Testing

* **Types of Errors**:

  * Type I: Rejecting true $H_0$
  * Type II: Failing to reject false $H_0$
* **Two-sample test statistic** (large samples):

  $$
  z = \frac{\bar{X}_1 - \bar{X}_2}{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}
  $$

### ANOVA

* **F-statistic**:

  $$
  F = \frac{\text{Mean Square Between}}{\text{Mean Square Within}}
  $$
* **Sums of Squares**:

  * Total: $SST = \sum (x_{ij} - \bar{x})^2$
  * Between: $SSB = \sum n_i (\bar{x}_i - \bar{x})^2$
  * Within: $SSW = SST - SSB$
* **Degrees of Freedom**:

  * Between: $df_B = k - 1$
  * Within: $df_W = N - k$
  * Total: $df_T = N - 1$


