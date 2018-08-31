<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]} }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Why we reject Null Hypothesis when $p \leq \alpha$?

Understanding Type I and II errors are of the fundamental importance in interpreting the results of Hypothesis Tests such as A/B testing. 

In Hypothesis Testing, we normally define (somehow arbitrary) significance level ($\alpha$) and use our test statistic to calcuate the well-known $p$-value. If $p \leq \alpha$ we reject the Null Hypothesis, $H_0$, and do not reject it otherwise. 

The reason why we reject $H_0$ when $p \leq \alpha$ was not quite clear to me. As pointed about by a user on [Stackexchange](https://math.stackexchange.com/questions/582945/in-statistics-why-do-you-reject-the-null-hypothesis-when-the-p-value-is-less-th), and with having access to stat books, articles and blog posts online as well as offline resources, we sometimes don't have the guts to question the underlying assumptions and conclusions of well-known mehotds such as A/B testing. Something you get the impressions that everybody knows it  except YOU! On the other hand, a simple Google search shows that it is one of the most confusing and misused concepts.

Before I continue, I assume the reader is familiar with Hypothesis Testing and to keep this writing short, I only discuss few concepts that are crucial in understanding the outcome. 


## Where does p-value come from?

According to [minitab](http://blog.minitab.com/blog/adventures-in-statistics-2/how-to-correctly-interpret-p-values)
> In technical terms, a $p$-value is the probability of obtaining an effect at least as extreme as the one in your sample data, assuming the truth of the null hypothesis. 

Let's elaborate on this: Any variable $x$ with normal distribution can be transormed to variable $z$ with standard normal distribution using the following formula

$$
z = \frac{x - \mu}{\sigma}
$$

where $\mu$ and $\sigma$ are the mean and standard deviation of the distribution, respectively and $z$ is the z-score. 

The mean and standard deviation of standard normal distribution, also known as the probability density distribution (figure below) are 1 and 0, respectively. Also, the area aunder curve for the distribution is unity. $p$-value is obtained from the probability density distribution. 

One, however, should note that $p$-value is of the type of **Cumulative Probability**. For instance, for left-tailed test and the test statistic $z_0$, $p$-value is the cumulative probability of $z$-values in the $[-\infty, z_0]$ range (figure below). Check out [this link](http://www.fairlynerdy.com/normal-distribution-summary/) for more. 


<div style="text-align:center"><img src ="left-tailed-test.png" height="200" width="300"/><figcaption> <font size="2">Source: <a href="http://www.mathcaptain.com/statistics/p-value.html"> Mathcaptain</a></font></figcaption></div>


## A simple example

I use a simple left-tailed z-test here. Having the sample mean, $\bar x = \bar x_0$, I want to find out the likelihood that the population mean is $\mu = \mu_0$. I start with developing the Null Hypothesis (assuming a random sample and Central Limit Theorem that leads to $\mu_{\bar x} = \mu$), 
as 

$$H_0: \mu = \mu_0$$. 

Assuming the Null Hypotheis is true, I want to find out how likely is it that $\bar {x}$ belongs to a disrtibution with $\mu = \mu_0$. Hence, I define the test statistic as

$z_0 = \frac{\bar x_0 - \mu_0}{\sigma/\sqrt{n}}$

where $n$ is the sample size. The z-score table can help us find the $p$-value. As a reminder, the obtained $p$-value is the cumulative probability that $z \leq z_0$ belong to a distribution with $\mu = \mu_0$ assuming that $H_0$ is true. [In other words](http://blog.minitab.com/blog/adventures-in-statistics-2/how-to-correctly-interpret-p-values), 
> $p$-values are calculated based on the assumptions that the null is true for the population and that the difference in the sample **is caused entirely by random chance.**

Let's assume $p=0.03$. This means that if the Null Hypotheis is true, only 3% of the time we find a random sample with $\bar x = \bar x_0$. 


## $\alpha$ and $p$-value

$\alpha$, the [significance level](https://en.wikipedia.org/wiki/Statistical_significance#Role_in_statistical_hypothesis_testing), is the probability of the occurence of Type I error, i.e., rejecting Null Hypothesis when it is true. The statement "when the Null Hypothesis is true" is a very important assumption behind the definition of Type I error and is often overlooked.

Significance level is the level of risk we want to take in rejecting $H_0$. The lower this value, the more confident we are about the outcome of the test.  For example, $\alpha$ = 5% indicates we accept 5% risk in rejecting true $H_0$. In other words, we want to be up to 95% confident that we rightfully rejected Null. 

On the other hand, $p$-value is the probability of observing an effect (like coming up with a sample with sampling mean $\bar x_0$) [due to random sampling error](http://blog.minitab.com/blog/adventures-in-statistics-2/how-to-correctly-interpret-p-values), when the effect does not actually exist (the population mean is $\mu_0$). Obvoiusly, the closer $\bar x_0$ to $\mu_0$ (or  $z_0$ to 0), the bigger the area under curve and p-value, and vice versa.

[NIH](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2895822/)
> This is the most critical concept to keep in mind as it means that one cannot infer from the p value whether H0 is true or false.

[NIH](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC2895822/)
> The concept of a p value is not simple and any statements associated with it must be considered cautiously.

> the p value only gives us the probability that, simply owing to the chance selection of patients from the larger (target) population, the clinical experiment resulted in a difference in the samples, as large or larger, than the actual 26% observed.

> Thus a p value is simply a measure of the strength of evidence against H0.

> The p value is calculated based on an assumption that chance is the only reason for observing any difference. Thus it cannot provide evidence for the truth of that statement.

> An artificial cut point is chosen, called the significance level, and the result is called statistically significant if the p value is less than the significance level leading to the rejection of the null hypothesis.



If you have any feedback, please do not hesistate to share.
