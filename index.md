<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]} }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Why we reject Null Hypothesis when $p \leq \alpha$?

Understanding Type I and II errors are of the fundamental importance in interpreting the results of Hypothesis Tests such as A/B testing. 

In Hypothesis Testing, we define (somehow arbitrary) Significance Level ($\alpha$) and use our test statistic to calcuate the associated $p$-value. When $p \leq \alpha$ we reject the Null Hypothesis, $H_0$, and do not reject it otherwise. 

The reason for rejecting $H_0$ when $p \leq \alpha$ was not clear to me. The tremendous number of resources online and offline gives us the impression that these concepts are well understood and, sometimes, we [do not have the guts](https://math.stackexchange.com/questions/582945/in-statistics-why-do-you-reject-the-null-hypothesis-when-the-p-value-is-less-th) to question them. On the other hand, studying the results of a simple Google search shows that they are some of the most confusing and misunderstood concepts. [Academic research](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2895822/) also warn against misinterpreting them:

> The concept of a $p$-value is not simple and any statements associated with it must be considered cautiously.

Here I briefly disuss how $p$-values are calcluated and interpreted. I use a simple example to interpret $p$-value and then  relate it to Type I error and Significance Level. It is assumed the reader is familiar with Hypothesis Testing. 


## Where does p-value come from?

According to [minitab](http://blog.minitab.com/blog/adventures-in-statistics-2/how-to-correctly-interpret-p-values)
> A $p$-value is the probability of obtaining an effect at least as extreme as the one in your sample data, assuming the truth of the null hypothesis. 

Let's elaborate on this: any variable $x$ with normal distribution can be transormed to variable $z$ with standard normal distribution using the following formula

$$
z = \frac{x - \mu}{\sigma}
$$

where $\mu$ and $\sigma$ are the mean and standard deviation of the distribution of $x$ values, respectively, and $z$ is the z-score. 

The area under curve of a standard normal distribution, also known as the probability density distribution, is unity. $p$-values are obtained from the probability density distribution. 

<div style="text-align:center"><img src ="left-tailed-test.png" height="200" width="300"/><figcaption> <font size="2">Source: <a href="http://www.mathcaptain.com/statistics/p-value.html"> Mathcaptain</a></font></figcaption></div>

In fact, for test statistic $z$, the associated $p$-value is the **Cumulative Probability** of observing $z \in (-\infty, z]$ under the condition that the Null Hypothesis is true (figure above). Mathematically speaking, for any $z_0$ value, we can write $p$ in the form of conditional probability, 

$$
p\big(z\in(-\infty, z_0]|H_0\big)
$$


## Interpreting $p$

Let's use a simple example and assume we want to verify the claim that having a sample with the sample mean $\bar x = \bar x_0$, the population mean is $\mu = \mu_0$. Null Hypothesis (assuming a random sample and Central Limit Theorem) is stated as

$$
H_0: \mu = \mu_0,
$$

indicating that the popuation mean is equal to $\mu_0$ and $\bar x_0$ is an error due to sampling. Assuming the Null Hypotheis is true, we then want to find out the likelihood of generating a sample with the sample mean equal or smaller than $\bar x_0$.  As we saw in the previous session we can achieve this by finding the p-value associated with the test statistic given by

$$
z_0 = \frac{\bar x_0 - \mu_0}{\sigma}
$$

Therefore, $p$ can be interpreted as the possibility/probability of observing a sample with the sample mean $\bar x_0$ for a population with the population mean $\mu_0$ due to [random sampling error](http://blog.minitab.com/blog/adventures-in-statistics-2/how-to-correctly-interpret-p-values).


## $p$-value and $\alpha$

We should remind the reader to avoid the commom mistake in understanding $p$: $p$ is not the probability that $H_0$ is true or false. We assumed the truthness of $H_0$ to calculate $p$. Instead, $p$ provides a measure of observing an effect when in fact it does not exist. [In other words](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2895822/),
> $p$-value is simply a measure of the strength of evidence against [or in favor of] $H_0$.

This means that low (high) $p$-value indicates a weak (strong) $H_0$, i.e. the observed effect is unlikely (likely) be due to sampling error. This is how $p$-value can be used to favor/disfavor $H_0$. 

And here is where $\alpha$ comes into play: an artificial cutpoint which is used as a measure to reject or not-reject the Null Hypothesis. To clarify, let's remind that [Type I error occurs}(https://www.stat.berkeley.edu/~hhuang/STAT141/Lecture-FDR.pdf)
> when we are observing a difference [effect] when in truth there is none.

To find out how $\alpha$ and $p$ relate, let's set two significant levels ($\alpha = 0.05$ and $\alpha = 0.01$) and assume  $p=0.03$.

$p = 0.03$: there is a 3% chance of observing an effect, solely due to the sampling error, when there is actually none.

$\alpha = 0.05$: we are up to 5% confident that any observed effect is due to random sampling (or 95% confident that it is not!). 

Since we only have 3% chance of observing the effect due to sampling error, we cannot be up to 5% confident that the observed effect is due to random sampling and support $H_0$ at this level. Therefore, we reject $H_0$ **at 5% level**. 

Following the same logic, we are $\alpha = 0.01$ confident that the observed effect is random and $H_0$ is true. Therefore, we do not reject $H_0$ **at 1% level**.

I hope the reader is convinced why $H_0$ is rejected when $p \leq \alpha$. This interpretation can be used to interpret the results of any hypothesis testing that employs $p$-values.
