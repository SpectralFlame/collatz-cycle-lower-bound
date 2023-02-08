# A greatly improved lower bound to the period of a non trivial Collatz cycle

Anthony McAtear; November 27, 2021

The Collatz conjecture has stumped mathematicians for nearly a century.
I too have spent several years looking at the intricate structures that arise from the simple Collatz rules.
Along the way I have been able to show that the period $p$ of a non trivial Collatz cycle must be at least $2^{68} + 68$, and more generally $\theta + \log_2 \theta$, with $\theta$ equal to all consecutive numbers that experimentally have been shown to go to 1.
Let me explain things from the very beginning, starting with what exactly the Collatz conjecture is about.

## The Collatz conjecture

This conjecture has many names; the $3n + 1$ problem, the Ulam conjecture, Kakutani's problem, the Thwaites conjecture, among others.
I was first introduced to this problem [from a Numberphile video in 2016](https://www.youtube.com/watch?v=5mFpVDpKX70) under the name of the Collatz conjecture, so that is what I'm going to call it.

It is conjectured that any positive integer $n$ will eventually reach $1$ after repeatedly applying two simple arithmetic operations based on whether $n$ is even or not:

$$
h(n) = \begin{cases}
n / 2 & \mathrm{if}\ n \equiv 0 \\
3n + 1 & \mathrm{if}\ n \equiv 1
\end{cases}
\hspace{1em} (\mathrm{mod} \ 2) \ .
$$

Noticing that $3n + 1$ must be even when $n$ is odd, we can define a "shortcut" form of the Collatz function:

$$
g(n) = \begin{cases}
n / 2 & \mathrm{if} \ n \equiv 0 \\
\frac{3n + 1}2 & \mathrm{if} \ n \equiv 1
\end{cases}
\hspace{1em} (\mathrm{mod} \ 2) \ .
$$

The repetitive nature of the Collatz conjecture can be expressed as

$$
g^k(n) = 1 \ \forall \ n,k \in \mathbb{Z}^+ \ .
$$


### Disproving the Collatz conjecture

To disprove the Collatz conjecture, one has to show that there exists a positive integer $n$ such that

$$ 
\lim_{k\to\infty} g^k(n) = \infty \ ,
$$

or that a non trivial cycle with period $p$ exists

$$ 
\min_p g^p(n) = n \hspace{1em} \mathrm{with} \ \ n > 4 \ , \ p \ge 1 \ .
$$

The latter is what this work touches on; improving the lower bound of the period $p$ of such a non trivial Collatz cycle.

### Collatz cycles

A Collatz cycle is a sequence of terms that repeat.
Only one Collatz cycle is known to exist, the $(4, 2, 1)$ cycle, with its equivalent in the shortcut form being $(2, 1)$ with period $p = 2$.
This is the trivial Collatz cycle:

$$
g(2) = 2 / 2 = 1 \hspace{1em} \to \hspace{1em} g(1) = \frac{3 \cdot 1 + 1}2 = 2
$$

In this work, the shortcut form of the Collatz function is used to determine the period $p$ of a Collatz cycle.
Note that this period equals the total number of divisions by two to complete one cycle.

## Outline

We'll first work our way to express a Collatz cycle as the simple diophantine equation

$$
n = \frac\gamma\delta \hspace{1em} \mathrm{with} \ n \in \mathbb Z^+ \ \mathrm{and} \  \gamma, \delta \in \mathbb Z
$$

After this is achieved, we'll look at the upper and lower bounds of the numerator and denominator respectively, in function of the cycle period.

Finally, incorporating these bounds of $\gamma$ and $\delta$, as well as the lower bound of $n$ given by experimental evidence, an improved lower bound to the cycle period $p$ can be found.
This turns out to be $2^{68} + 68$, or more generally $\theta + \log_2 \theta$.


## The Odd Collatz function

In this work, we'll use a slightly different representation of the Collatz function, namely the Odd Collatz Function (OCF).
The domain of the OCF only includes all odd positive integers, but conserves the intricate structure of the original Collatz function. It is defined as

$$
f(n) = \begin{cases}
f_0(n) = \frac{n - 1}4 & \mathrm{if} \ n \equiv 5 \\
f_1(n) = \frac{3n + 1}2 & \mathrm{if} \ n \equiv 3,7 \\
f_2(n) = \frac{3n + 1}4 & \mathrm{if} \ n \equiv 1
\end{cases}
\hspace{1em} (\mathrm{mod} \ 8) \hspace{1em} \mathrm{with} \ \ n \equiv 1 \ (\mathrm{mod} \ 2) \ .
$$

Notice that each case of the Odd Collatz Function (OCF) is of the form 

$$
f_i(n) = 2^{-a_i} (3^{b_i} + c_i) \ ,
$$

with the values of $a$, $b$ and $c$ for each $f_i$ given in the table bellow:

$f_i$ | $a_i$ | $b_i$ | $c_i$
---|---|---|---
$f_0$ | 2 | 0 | -1
$f_1$ | 1 | 1 | 1
$f_2$ | 2 | 1 | 1

## A diophantine equation for Collatz cycles

Let $S$ be the ordered set $(i_1, \dots, i_k)$, with $S_i \in \{0, 1, 2\}$, such that

$$
f_S = f^k = f_{i_k} \circ \cdots \circ f_{i_1} \ ,
$$

representing the sequence of OCFs to be applied in order.
Given $S$, we can calculate the result of $f_S(n)$ directly:

$$
f_S(n) = \delta' n + \gamma' \ ,
$$

with 

$$
\begin{aligned}
\delta' &= 2^{-\alpha} 3^\beta \\
\gamma' &= \sum_{i = 1}^{|S|} 2^{-\alpha_i} 3^{\beta_{i - 1}} c_{S^\ast_i} \\
\alpha_k &= \sum_{i = 1}^k a_{S^\ast_i} \hspace{3em} \alpha = \alpha_{|S|} \\
\beta_k &= \sum_{i = 1}^k b_{S^\ast_i} \hspace{3em} \beta = \beta_{|S|}
\end{aligned} \ ,
$$

with $S^\ast$ the reverse and $|S|$ the length of $S$.

From this, it follows that $n = \delta' n + \gamma'$, so an integer solution to the diophantine equation

$$
n = \frac{\gamma'}{1 - \delta'} \hspace{1em} \mathrm{with} \ n \in \mathbb Z \ ,
$$

corresponds with a Collatz cycle where $n$ is one of the elements in that cycle.
Let $\gamma = 2^\alpha \gamma'$ and $\delta = 2^\alpha (1 - \delta')$.
Then the above equation simplifies to

$$
n = \frac\gamma\delta = \frac{{\sum}^{|S|}_{i=1} 2^{\alpha - \alpha_i} 3^{\beta_i - 1} c_{S^\ast_i}}{2^\alpha - 3^\beta} \hspace{1em} \mathrm{with} \ n, \gamma, \delta \in \mathbb Z \ .
$$

Whereas $\gamma'$ and $\delta'$ are rational numbers, $\gamma$ and $\delta$ are always odd integers.
There can only be a positive solution if both $\gamma$ and $\delta$ are positive, or if both are negative.
It is first shown that it is impossible for both to be negative.
Then, an upper bound for $\gamma$ and a lower bound for $\delta$ are defined in terms of $\alpha$.
These bounds in combination with experimental evidence to set a lower bound on $n$, are used to find a lower bound for $\alpha$, which directly corresponds to the cycle period $p$.


## There are no positive cycles when $\gamma \le \delta < 0$

Let $S$ be an ordered set such that $\gamma \le \delta < 0$. It can be shown that such a set does not exist.

### A condition for $\delta < 0$

With $\delta = 2^\alpha - 3^\beta$, the following condition must be met such that $\delta < 0$:

$$
\begin{aligned}
\alpha &< \beta \log_2 3 \\
\alpha &< \beta \cdot 1.585
\end{aligned} \ .
$$

This condition poses a restriction on $S$, namely that $1 \in S$, as $f_1$ is the only subfunction of the OCF that satisfies this condition.

### A condition for $\gamma < 0$

Decreasing $\gamma$ can only be achieved by having a negative $c$ value, i.e. $f_0$.
Thus for the most negative $\gamma$, we find that $0 \in S$, and more specifically at the end of $S$ as then it has the most influence on $\gamma$.

### A condition for $\gamma \le \delta < 0$

We thus find that $S$ must be of the form

$$
S = (\underbrace{1, \dots, 1}_{\lambda \ \mathrm{times}}, \underbrace{0, \dots, 0}_{\kappa \ \mathrm{times}}) \ .
$$

This restriction on $S$ allows $\gamma$ to be simplified into

$$
\gamma = \sum_{\ell = 0}^{\lambda - 1} 2^{\lambda - \ell - 1} 3^\ell - \sum_{k = 0}^{\kappa - 1} 2^{\lambda + 2k} \ ,
$$

which can further be simplified using geometric series:

$$
\begin{aligned}
\gamma &= 2^{\lambda - 1} \sum_{\ell = 0}^{\lambda - 1} (3 / 2)^\ell - 2^\lambda \sum_{k = 0}^{\kappa - 1} 4^k \\
&= 2^{\lambda - 1} \frac{ 1 - (3 / 2)^\lambda }{ 1 - (3 / 2) } - 2^\lambda \frac{ 1 - 4^\kappa }{ 1 - 4 } \\
&= 2^\lambda \left [ (3 / 2)^\lambda - 1 - \frac{ 4^\kappa - 1 }{ 3 } \right ] \ .
\end{aligned}
$$

Rewriting the condition $\alpha < \beta \log_2 3$ in terms of $\lambda$ and $kappa$, with $\alpha = \lambda + 2 \kappa$ and $\beta = \lambda$, we get

$$
\lambda > \kappa \frac{ 2 }{ \log_2 3 - 1 } \ .
$$

Substituting this into the formula for $\gamma$ gives us

$$
\gamma = 2^\lambda \left [ 4^\kappa - 1 - \frac{ 4^\kappa - 1 }{ 3 } \right ] \ .
$$

In this form, it is clear that $\gamma$ can never be negative when $\delta < 0$ and vice versa.
Therefore, both $\gamma$ and $\delta$ must be greater than $0$ for a positive cycle to exist.


## An upper bound to $\gamma$

Let $S$ be the ordered set that results in the largest value of $\gamma$.
It can be found that $S$ must be of the form

$$
S = (\underbrace{1, \dots, 1}_{\lambda \ \mathrm{times}}, \underbrace{2, \dots, 2}_{\kappa \ \mathrm{times}}) \ .
$$

As before, this allows for a simplified equation for $\gamma$:

$$
\gamma = \sum_{\ell = 0}^{\lambda - 1} 2^{\lambda - \ell - 1} 3^{\kappa + \ell} + \sum_{k = 0}^{\kappa - 1} 2^{\lambda + 2 k} 3^{\kappa - k - 1} \ ,
$$

which can be further simplified using geometric series:

$$
\begin{aligned}
\gamma &= 2^{\lambda - 1} 3^\kappa \sum_{\ell = 0}^{\lambda - 1} (3 / 2)^\ell + 2^\lambda 3^{\kappa - 1} \sum_{k = 0}^{\kappa - 1} (4 / 3)^k \\
&= 2^{\lambda - 1} 3^\kappa \frac{ 1 - (3 / 2)^\lambda }{ 1 - (3 / 2) } + 2^\lambda 3^{\kappa - 1} \frac{ 1 - (4 / 3)^\kappa }{ 1 - (4 / 3) } \\
&= 2^\lambda 3^\kappa \left [ (3 / 2)^\lambda + (4 / 3)^\kappa - 2 \right ] \\
&= 2^{2\kappa + \lambda} + 3^{\kappa + \lambda} - 2^{\lambda + 1} 3^\kappa \ .
\end{aligned}
$$

Defining $\gamma$ in terms of $\alpha = 2\kappa + \lambda$ and $\beta = \kappa + \lambda$ gives use

$$
\gamma = 2^\alpha + 3^\beta - 2 (3 / 2)^\alpha (4 / 3)^\beta \ .
$$

From the condition that $\delta > 0$, i.e. $\alpha > \beta \log_2 3$, $\gamma$ is the biggest when $\alpha = \beta \log_2 3$.
This results in

$$
\gamma = 2^{\alpha + 1} - 2^{(\log_2 3 + 2 \log_3 2 - 2)\alpha + 1} \approx 2^{alpha + 1} - 2^{0.847\alpha + 1} \ .
$$

A conservative upper bound of $\gamma$ in terms of $\alpha$ is thus

$$
\gamma < 2^{\alpha + 1}
$$


## A lower bound to $\delta > 0$

To find the lower bound to $\delta = 2^\alpha - 3^\beta > 0$, we need to make use of linear forms in logarithms.
The mathematics involved is quite complicated, so I'm just including some of the formulas here without any explanation as to where these formulas come from.
See [Applications of Linear Forms in Logarithms; Chapter 12](https://doi.org/10.1007/978-0-387-49894-2_4) for more information (note: please do not pay for access, these institutions should have never existed...).

Using linear forms in logarithms, it is proven that $\delta = | 2^\alpha - 3^\beta |$ tends to infinity with $\alpha + \beta$, and an explicit lower bound can be calculated.
For a specific value of $\delta$, it is thus possible to calculate an upper bound for $\alpha and $\beta$.
An initial upper bound for $\alpha$, denoted as $\hat \alpha_{(1)}$, is found using the following inequality:

$$
\log \delta > \hat \alpha_{(1)} \log 2 - 5.87 \cdot 10^8 \left( 1 + \log \hat \alpha_{(1)} \right) \ .
$$

This gives rise to an upper bound for $\beta$ being $\hat \beta_{(1)} = \hat \alpha_{(1)} \log_3 2$.
This initial estimate can be improved, with the improved estimate denoted $\hat \beta_{(2)}$, using

$$
\left | \alpha - \hat \beta_{(2)} \log_2 3 \right | < \frac{ \delta }{ \log 2 } 3^{-\hat \beta_{(2)}} \ .
$$

It can be shown that the left hand side is greater than the reciprocal of $\hat \beta_{(1)}$ for $\hat \beta_{(2)} < \hat \beta_{(1)}$, so we can write

$$
\frac{ \delta }{ \log 2 } 3^{-\hat \beta_{(2)}} > \frac{ 1 }{ \hat \alpha_{(1)} \log_3 2 } \ ,
$$

and can be simplified to

$$
\hat \alpha_{(2)} < \log_2 \delta + \log_2 \hat \alpha_{(1)} + \log_2 \log_3 2 - \log_2 \log 2 \ .
$$

Writing $\delta$ in the form of $2^x$, it further simplifies to

$$
\hat \alpha_{(2)} < x + \log_2 \hat \alpha_{(1)} - 0.135 \ ,
$$

which puts an upper bound on $\alpha$ for a given $\delta = 2^x$.
Similarly, for a given $\alpha$, the lower bound of $\delta = 2^x$ is given by

$$
x > \alpha - \log_2 \hat \alpha_{(1)} + 0.135
$$


## A lower bound to the period $p$ of a non trivial Collatz Cycle

As of 2020, the conjecture has been checked for all starting values up to $2^{68}$.
From this it follows that

$$
\frac \gamma \delta > 2^68 \hspace{1em} \mathrm{or \ that} \ \gamma > 2^{68 + x} \hspace{1em} \mathrm{with} \ \delta = 2^x
$$

From the relation $ \gamma < 2^{\alpha + 1} $, we get

$$
\alpha > 67 + x \ .
$$

Combining this with the lower bound of $\delta$:

$$
x > 67 + x - \log_2 \hat \alpha_{(1)} + 0.135 \ ,
$$

which leads to the following inequality

$$
\log_2 \hat \alpha_{(1)} > 67.135 \ .
$$

Plugging in this lower bound for $\hat \alpha_{(1)}$ results in

$$
x > 2^{67.135} - 5.87 \cdot 10^8 \left ( \frac{ 1 }{ \log 2 } + 67.135 \right ) > 2^{67} \ .
$$

The negative term in the formula is dwarfed by $2^{67.135}$ and can safely be ignored, resulting in $x > 2^{67}$, from which follows that $\alpha > 2^{67} + 67$.
As $p = \alpha$, we conclude that

$$
p > 2^{67} + 67 = 147573952589676412995 \ ,
$$

and more generally, knowing that all numbers up to $\theta$ go to $1$, we can say that

$$
p > \frac \theta 2 + \log_2 \theta - 1 \ .
$$

