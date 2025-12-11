### Combinatorics

**Definitions**

- **Permutations ($P_n$):** Used to arrange a set of objects where **order matters**. You arrange the entire set of elements. 212121
  
  $P_n = n!$
  
  22

- **Variations ($V^n_p$):** Picking a subset ($p$) from a total ($n$) and arranging them. **Order matters**. 232323
  
  - Without repetition: $V_{p}^{n}=\frac{n!}{(n-p)!}$ 24
  
  - With repetition: $\overline{V}_{p}^{n}=n^{p}$ 25

- **Combinations ($C^n_p$):** Picking a subset of elements where **order is irrelevant** (does not matter).
  
  $C_{p}^{n} = \binom{n}{p} = \frac{n!}{p!(n-p)!}$
  
  
  
  - Symmetry property: $C_{p}^{n} = C_{n-p}^{n}$ (Choosing $p$ elements is the same as leaving $n-p$ elements behind).

Relationship between Combinations and Variations

$C = \frac{V}{P}$

Combinations count all permutations of a given set of numbers as a single group, whereas variations count them separately.

---

### Probability Theory

**Basic Rules**

- **Probability Formula:** $P(event) = \frac{\text{\# outcomes of event}}{\text{\# outcomes in Sample Space}}$ 

- **Complement Rule:** $P(A) = 1 - P(A')$ 31

- **Union ($A \cup B$):** $P(A \cup B) = P(A) + P(B) - P(A \cap B)$ 
  
  - If mutually exclusive: $P(A \cup B) = P(A) + P(B)$ 

- **Intersection ($A \cap B$):**
  
  - Dependent: $P(A \cap B) = P(A) \cdot P(B|A)$ 
  
  - Independent: $P(A \cap B) = P(A) \cdot P(B)$ 

**Conditional Probability vs. Bayes' Theorem** 

- Conditional Probability: Used when $P(A \cap B)$ and $P(B)$ are easy to calculate.
  
  $P(A|B) = \frac{P(A \cap B)}{P(B)}$
  
  Bayes' Theorem: Used to update beliefs (hypothesis $A$) given new evidence ($B$).

- $$P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}$$
  
  

---

### Probability Distributions

1. Discrete Distributions 39

| **Distribution**      | **Notation**          | **PMF P(X=x)**                                      | **Mean E[X]** | **Variance σ2**      | **Description**                                                                                |
| --------------------- | --------------------- | --------------------------------------------------- | ------------- | -------------------- | ---------------------------------------------------------------------------------------------- |
| **Bernoulli**         | $X \sim Bern(p)$      | $\begin{cases}p & x=1\\ 1-p & x=0\end{cases}$       | $p$           | $p(1-p)$             | 1 trial, 2 possible outcomes (success/failure). 40404040                                       |
| **Binomial**          | $X \sim B(n,p)$       | $\binom{n}{x}p^{x}(1-p)^{n-x}$                      | $np$          | $np(1-p)$            | Number of successes in $n$ independent trials. 414141414141414141                              |
| **Geometric**         | $X \sim Geo(p)$       | $(1-p)^{x-1}p$                                      | $\frac{1}{p}$ | $\frac{1-p}{p^2}$    | Trials until the **first** success. 424242424242424242                                         |
| **Negative Binomial** | $X \sim NB(r,p)$      | $\binom{x-1}{r-1}(1-p)^{x-r}p^r$                    | $\frac{r}{p}$ | $\frac{r(1-p)}{p^2}$ | Waiting time for $r$ successes. 43434343                                                       |
| **Hypergeometric**    | $HGeom(n, m, r)$      | $\frac{\binom{r}{x}\binom{n-r}{m-x}}{\binom{n}{m}}$ | -             | -                    | Sampling **without replacement**. $r$=Type 1 elements, $n$=Total elements, $m$=Sample size. 44 |
| **Poisson**           | $X \sim Poi(\lambda)$ | $\frac{\lambda^x e^{-\lambda}}{x!}$                 | $\lambda$     | $\lambda$            | Frequency of events in a specific interval (time/space). 454545454545454545                    |

2. Continuous Distributions 46

For continuous distributions, $P(X=x) = 0$. Probabilities are calculated over intervals using the Cumulative Distribution Function (CDF). 47

| **Distribution**      | **PDF f(x)**                                                            | **Mean**            | **Variance**          | **Notes**                                                                      |
| --------------------- | ----------------------------------------------------------------------- | ------------------- | --------------------- | ------------------------------------------------------------------------------ |
| **Uniform**           | $\frac{1}{b-a}$ for $x \in [a,b]$                                       | $\frac{a+b}{2}$     | $\frac{(b-a)^2}{12}$  | All outcomes equally likely. 48484848                                          |
| **Exponential**       | $\lambda e^{-\lambda x}$ ($x \ge 0$)                                    | $\frac{1}{\lambda}$ | $\frac{1}{\lambda^2}$ | Time between events in a Poisson process. 49494949                             |
| **Normal (Gaussian)** | $\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{1}{2}(\frac{x-\mu}{\sigma})^{2}}$ | $\mu$               | $\sigma^2$            | Symmetric "Bell Curve". 50505050                                               |
| **Student's t**       | -                                                                       | $\mu$               | $\frac{S^2 k}{k-2}$   | Small sample size approx of Normal. Fatter tails. $k$ = degrees of freedom. 51 |
| **Chi-Squared**       | -                                                                       | $k$                 | $2k$                  | Used for goodness-of-fit and variance testing. 52525252                        |

**Important Normal Distribution Properties:**

- **Empirical Rule (68-95-99.7):**
  
  - 68% of data falls within $\mu \pm 1\sigma$ 53535353
  
  - 95% of data falls within $\mu \pm 2\sigma$ 54545454
  
  - 99.7% of data falls within $\mu \pm 3\sigma$ 55555555

- Standard Normal ($Z$):
  
  $$Z = \frac{Y - \mu}{\sigma} \sim N(0, 1)$$
  
  56

---

### Approximations

1. Binomial Approximation of Hypergeometric

Used when Population ($N$) is very large and Sample ($n$) is small ($n/N < 0.05$). Sampling without replacement roughly equals sampling with replacement. 57

2. Normal Approximation of Poisson

If $\lambda$ is large, Poisson becomes bell-shaped.

$$X \sim Poi(\lambda) \Rightarrow X \approx N(\mu=\lambda, \sigma^2=\lambda)$$

58

3. Normal Approximation of Binomial

Used when $np \ge 10$ and $n(1-p) \ge 10$. 59

$$X \approx N(np, \sqrt{np(1-p)})$$

60

- **Continuity Correction:** When approximating discrete with continuous, adjust the interval by 0.5 (e.g., $P(X \le a) \approx P(Y < a + 0.5)$). 61
4. Poisson Approximation of Binomial (Law of Rare Events)

Used when $n > 50$ (large trials) and $p < 0.10$ (small probability). 62

$$X \sim Bin(n, p) \approx Poi(\lambda = np)$$

63

---

### Descriptive Statistics

**Types of Data** 64

- **Categorical (Qualitative):** Nominal (no order), Ordinal (ordered).

- **Numerical (Quantitative):** Discrete, Continuous/Measurements. Interval (no true zero), Ratio (true zero).

**Measures of Central Tendency**

- **Mean:** $\bar{x} = \frac{\sum x_i}{N}$ (Sensitive to outliers). 65

- **Median:** Middle number at position $\frac{n+1}{2}$. 66

- **Mode:** Most frequent value. 67

**Measures of Asymmetry (Skewness)** 68

- **Right (Positive) Skew:** Mean > Median. Outliers are to the right. 69696969

- **Left (Negative) Skew:** Mean < Median. Outliers are to the left. 70707070

**Measures of Dispersion**

- **Variance ($\sigma^2$):**
  
  - Population: $\sigma^{2}=\frac{\sum(x_{i}-\mu)^{2}}{N}$ 71
  
  - Sample: $s^{2}=\frac{\sum(x_{i}-\overline{x})^{2}}{n-1}$ 72

- **Coefficient of Variation ($C_v$):** $C_v = \frac{\sigma}{\mu}$. Used to compare data sets with different units/means. 73737373

**Measures of Relation**

- **Covariance ($S_{xy}$):** Indicates direction of relationship. 74

- Correlation Coefficient ($r$):
  
  $r = \frac{Cov(x,y)}{StdDev(x) \cdot StdDev(y)}$
  
  Range: $[-1, 1]$. $0$ means independent. $1$ is perfect positive correlation. 75

---

### Inferential Statistics

**Hypothesis Testing Steps** 76

1. **Formulate Hypothesis:** $H_0$ vs $H_1$.

2. **Select Test:**
   
   - **Z-test:** Variance known, large sample, Normal dist. 77
   
   - **t-test:** Variance unknown, small sample ($n < 30$). 78

3. **Define Significance Level ($\alpha$):** Typically 0.05.

4. **Compare:** Resulting value vs. Critical value.

**Errors and Power** 79

- **Confidence Level:** Typically 95% ($1 - \alpha$).

- **Significance Level ($\alpha$):** Probability of Type I Error (False Positive).

- **Power ($1 - \beta$):** Probability of avoiding Type II Error (False Negative). Typically aim for 80%.

---

### Math Supplement

**Geometry Formulas** 80

- **Pythagorean Theorem:** $c^2 = a^2 + b^2$

- **Trigonometry:** SOH CAH TOA ($\sin = \frac{opp}{hyp}$, $\cos = \frac{adj}{hyp}$, $\tan = \frac{opp}{adj}$).

- **Area of Circle:** $A = \pi r^2$

- **Area of Trapezoid:** $A = \frac{a+b}{2}h$

**Algebraic Rules**

- **Difference of Squares:** $a^2 - b^2 = (a+b)(a-b)$ 81

- **Square Expansion:** $(a-b)^2 = a^2 - 2ab + b^2$ 82

- **Quadratic Formula:** $x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$ 83

**Exponents** 84

- $a^m \times a^n = a^{m+n}$

- $(a^m)^n = a^{mn}$

- $a^{-m} = \frac{1}{a^m}$

- $a^0 = 1$



### Hypothesis Testing Fundamentals

P-Value Definition

The P-value is the probability of observing the results obtained given that the null hypothesis (H_0) is true. 17

- **P-value < 0.05:** Strong evidence to suggest the observed effect is real. Reject the Null Hypothesis (H_0). 18

- **P-value > 0.05:** No significant result. Fail to reject the Null Hypothesis. 19

- **Note:** If P < 0.05, there is an increased risk of Type I error. Reasons for misleading P-values can include small sample sizes or small observed effects. 20
