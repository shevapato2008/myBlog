---
layout: post
title: LaTex in MarkDown
meta: This post introduces some simple $\LaTeX$ syntax in Markdown environment.
---

This post introduces some simple $\LaTeX$ syntax in Markdown environment.

Latex is a language to represent mathematical formula using text.

For Latex documentation please check the wiki: <br>
http://en.wikibooks.org/wiki/LaTeX/Mathematics

### 1. Inline and Block $\LaTeX$
---

#### Code

(1.1) **In-Line Mathematics**:

Ones that _occur within a paragraph_

```LaTeX
* $x = y$
* \\(x = y\\)
```

(1.2) **Displayed Mathematics**:

Larger equations that _appear separated from the rest of the text on lines by themselves_

```LaTeX
* $$x = y$$
* \\[x = y\\]
```

#### Output

(1.1) In-Line Mathematics:
* $x = y$
* \\(x = y\\)

(1.2) Displayed Mathematics:
* $$x = y$$
* \\[x = y\\]

<br><br>

### 2. Greek Alphabet $^{[1]}$
---

| Name          |  Symbols               | $\LaTeX$ Command             |
|--------------:|:----------------------:|:----------------------------:|
| Alpha         | $\alpha$ $A$           | `$\alpha$ $A$`               |
| Beta          | $\beta$ $B$            | `$\beta$ $B$`                |
| Gamma         | $\gamma$ $\Gamma$      | `$\gamma$ $\Gamma$`          |
| Delta         | $\delta$ $\Delta$      | `$\delta$ $\Delta$`          |
| Epsilon       | $\epsilon$ $E$         | `$\epsilon$ $E$`             |
| Zeta          | $\zeta$ $Z$            | `$\zeta$ $Z$`                |
| Eta           | $\eta$ $E$             | `$\eta$ $E$`                 |
| Theta         | $\theta$ $\Theta$      | `$\theta$ $\Theta$`          |
| Iota          | $\iota$ $I$            | `$\iota$ $I$`                |
| Kappa         | $\kappa$ $K$           | `$\kappa$ $K$`               |
| Lambda        | $\lambda$ $\Lambda$    | `$\lambda$ $\Lambda$`        |
| Mu            | $\mu$ $M$              | `$\mu$ $M$`                  |
| Nu            | $\nu$ $N$              | `$\nu$ $N$`                  |
| Omicro        | $\omicron$ $O$         | `$\omicron$ $O$`             |
| Pi            | $\pi$ $\Pi$            | `$\pi$ $\Pi$`                |
| Rho           | $\rho$ $R$             | `$\rho$ $R$`                 |
| Sigma         | $\sigma$ $\Sigma$      | `$\sigma$ $\Sigma$`          |
| Tau           | $\tau$ $T$             | `$\tau$ $T$`                 |
| Upsilon       | $\upsilon$ $\Upsilon$  | `$\upsilon$ $\Upsilon$`      |
| Phi           | $\phi$ $\Phi$          | `$\phi$ $\Phi$`              |
| Chi           | $\chi$ $X$             | `$\chi$ $X$`                 |
| Psi           | $\psi$ $\Psi$          | `$\psi$ $\Psi$`              |
| Omega         | $\omega$ $\Omega$      | `$\omega$ $\Omega$`          |

<br><br>

### 3. Basic operations
---

#### Code

```LaTeX
$y = x + 5$
$y = x - 5$
$y = 5x$
$y = x \times 5$
$y = \frac{x}{5}$
$y = x \div 5$
```

#### Output

 - $y = x + 5$
 - $y = x - 5$
 - $y = 5x$
 - $y = x \times 5$
 - $y = \frac{x}{5}$
 - $y = x \div 5$

<br><br>

### 4. Power and Index
---

#### Code

```LaTeX
$y_n = x_n - x_{n-1}$
$y = x^2 - 2x^{x-1}$
```


#### Output

 - $y_n = x_n - x_{n-1}$
 - $y = x^2 - 2x^{x-1}$

 <br><br>

### 5. Fraction
---

#### Code

```LaTeX
- $^1/_2$
- $\frac{1}{2}$
```

#### Output

- $()^{1}/_{2}$
- $\frac{1}{2}$

<br><br>

### 6. Roots
---

#### Code

```LaTeX
$\sqrt{\frac{1}{3}}$
$\sqrt[3]{2x}$
```

#### Output

 - $\sqrt{\frac{1}{3}}$
 - $\sqrt[3]{2x}$

<br><br>

### 7. Sums and Integrals
---

#### Code

```LaTeX
(7.1) Sums

* $\sum\limits_{i = 1}^{10} t_i x_i$
* $\sum_{i = 1}^{10} t_i x_i$

(7.2) Integrals

+ $\int\limits_{- \infty}^{\infty} \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{(x - \mu)^2}{2 \sigma^2}} dx$
+ $\int_{- \infty}^{\infty} \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{(x - \mu)^2}{2 \sigma^2}} dx$

```

#### Output

(7.1) Sums

* $\sum\limits_{i = 1}^{10} t_i x_i$
* $\sum_{i = 1}^{10} t_i x_i$

(7.2) Integrals

+ $\int\limits_{- \infty}^{\infty} \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{(x - \mu)^2}{2 \sigma^2}} dx$
+ $\int_{- \infty}^{\infty} \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{(x - \mu)^2}{2 \sigma^2}} dx$

<br><br>

### Reference
---

`[1]` [LaTeX commands to display the Greek alphabet](https://www.latex-tutorial.com/symbols/greek-alphabet/ "LaTeX commands to display the Greek alphabet")<br>
`[2]` [A simple guide to LaTeX - Step by Step](https://www.latex-tutorial.com/tutorials/ "A simple guide to LaTeX - Step by Step")
