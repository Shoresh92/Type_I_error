<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]} }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Why we reject Null Hypothesis when $p \leq \alpha$?

Understanding Type I and II errors are of the fundamental importance in interpreting the results of Hypothesis Tests such as A/B testing. 

In Hypothesis Testing, we normally define (somehow arbitrary) Significance Level ($\alpha$) and use our test statistic to calcuate the associated $p$-value. When $p \leq \alpha$ we reject the Null Hypothesis, $H_0$, and do not reject it otherwise. 

The reason for rejecting $H_0$ when $p \leq \alpha$ was not clear to me. The tremendous number of resources online and offline gives us the impression that these concepts are well understood and, sometimes, we [do not have the guts](https://math.stackexchange.com/questions/582945/in-statistics-why-do-you-reject-the-null-hypothesis-when-the-p-value-is-less-th) to question them. On the other hand, studying the results of a simple Google search shows that they are some of the most confusing and misunderstood concepts. [Academic research](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2895822/) also warn against misinterpreting them:

> The concept of a $p$-value is not simple and any statements associated with it must be considered cautiously.

Here I briefly disucc what $p$-values are and how they are calculated. I use a simple example to interpret $p$-values and then  relate it to Type I error and Significance Level. It is assumed the reader is familiar with Hypothesis Testing. 


## Where does p-value come from?

According to [minitab](http://blog.minitab.com/blog/adventures-in-statistics-2/how-to-correctly-interpret-p-values)
> A $p$-value is the probability of obtaining an effect at least as extreme as the one in your sample data, assuming the truth of the null hypothesis. 

Let's elaborate on this: any variable $x$ with normal distribution can be transormed to variable $z$ with standard normal distribution using the following formula

$$
z = \frac{x - \mu}{\sigma}
$$

where $\mu$ and $\sigma$ are the mean and standard deviation of the distribution of $x$ values, respectively and $z$ is the z-score. 

The mean and standard deviation of standard normal distribution, also known as the probability density distribution (figure below) are 1 and 0, respectively, and its area curve is unity. $p$-values are obtained from the probability density distribution. 

In fact, for the test statistic $z$, the associated $p$-value is the **Cumulative Probability** of observing $z \in (-\infty, z]$ under the condition that the Null Hypothesis is true (figure below). Mathematically speaking, for any $z_0$ value, we can write $p$-value as

$$
p\big(z\in(-\infty, z_0]|H_0\big)
$$

<div style="text-align:center"><img src ="left-tailed-test.png" height="200" width="300"/><figcaption> <font size="2">Source: <a href="http://www.mathcaptain.com/statistics/p-value.html"> Mathcaptain</a></font></figcaption></div>


## Interpreting $p$

Let's use a simple example and assume we want to verify the claim that having a sample with the sample mean $\bar x = \bar x_0$, the population mean is $\mu = \mu_0$. Null Hypothesis (assuming a random sample and Central Limit Theorem) is stated as

$$
H_0: \mu = \mu_0,
$$

indicating that the popuation mean is in fact equal to $\mu_0$ and $\bar x_0$ is an error due to sampling. Assuming the Null Hypotheis is true, we then want to find out the likelihood of generating a sample with the sample mean equal or smaller than $\bar {x} = \bar x_0$.  As we saw in the previous session, We can achieve this by finding the p-value associated with the test statistic given by

$$
z_0 = \frac{\bar x_0 - \mu_0}{\sigma}
$$

Therefore, $p$ can be interpreted as the possibility/probability of observing a sample with the sample mean $\bar x_0$ for a population with the population mean $\mu_0$ due to [random sampling error](http://blog.minitab.com/blog/adventures-in-statistics-2/how-to-correctly-interpret-p-values). Remember we assumed $H_0$ is true!


## $p$-value and $\alpha$

We should remind the reader to avoid the commom misunderstanding: $p$ is not the probability that $H_0$ is true or false. It is because to claucate $p$, we already assumed $H_0$ is true. Instead, $p$ provides a measure of observing an effect when in fact it does not exist. [In other words](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2895822/),
> $p$-value is simply a measure of the strength of evidence against[or in favor of] $H_0$.

This means that low(high) $p$-value indicates a weak(strong) $H_0$, i.e. the effect is unlikely(likely) to be due to pure sampling error.

Therefore, we found out how $p$-value, as the result of Null Hypothesis can be in favor or against $H_0$. 

Here is where $\alpha$ comes into play: an artificial cutpoint which is used as a measure to reject or not-reject the Null Hypothesis. To clarify this, let's try two thresholds ($a\lpha = 0.05$ and $\alpha = 0.03$) for $p=0.03$. 



Therefore, $p \leq \alpha$ means the evidence in support of $H_0$ is not strong in \alpha level and $p > \alpha$ says the evidence are strong enough not to reject $H_0$.

$p = 0.03$: there is a 3% chance of observing an effect, solely due to the sampling error, when it is actually none.
$\alpha = 0.05$ means we are up to 5% confident that any observed effect is due to random sampling. Since we only have 3% chance of observing the effect due to sampling error, the confidence in $\alpha$ level is not fulfilled and consequently we reject $H_0$ at $alpha$-level. 

On the other hand, $\alpha = 0.01$ indicates if we are up to 1% confident that $H_0$ is true and the observed effect are due to random sampling. Comparing this with $p = 0.03$, we can expect to see this random effect in $\alpha$-level and that's why we do not reject $H_0$. 

If you have any feedback, please do not hesistate to share.
