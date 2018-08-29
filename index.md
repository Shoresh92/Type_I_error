<script type="text/x-mathjax-config"> MathJax.Hub.Config({ tex2jax: {inlineMath: [['$','$'], ['\\(','\\)']]} }); </script> <script src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.0/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# Understanding Type I Error in Statistical Analysis
I want to answer this question
> Why we reject Null Hypothesis, when $p \geq \alpha$
where p is the famous p-value and $\alpha$ is the significance level. 

I want to emphasize there are great resources available to teach Statisitcal Analysis, and relevant concpets such as Type I and II errors. However, I did not find many of them get to the buttom of why exactly $p \geq$ leads to rejecting 
$H_0$ something I want to explain in this short note. 

## Basic Concepts
Here I assume the reader is familiar with the basic concpets of Hypothesis Testing and will not go through it. However, I will present a definition or interpretation for the most important ones, to make sure we are on the same page before jumping ahead and making conclusions based on them.


* Significance Level ($ \alpha $)

The probability of rejecting a Null Hypothesis, $H_0$, when $H_0$ is actually true!

* p-value

In A/B testing, the p-value is the probability that we would get the observed difference between the A and B groups (or a more extreme difference) by random chance. 

Shoresh: explain here: where does the p-value come from? For example explain why the statement above is correc?

> p-value is the probability that we would get the observed difference between the A and B groups (or a more extreme difference) by random chance.

## Where does p-value come from?
p-value is obtained from the normal probability density plot. Let's forget about significance level for a moment and focus on the origin of p-value. We know that for any variable $x$ with normal distribution, the standard score, or z-score is defined as follwoing:

$$
z = \frac{x - \mu}{\sigma}
$$

where $\mu$ and $\sigma$ are the mean and standard deviation of the distribution, respectively. 

This transformation from a normal distribution to standard normal distribution can be best shown in probablity density plot which is the probability density function vs. z-values, as shown in figure below.

![Probability Density Plot](~/fairlynerdy.png)

Figure source: [Failry Nerd](http://www.fairlynerdy.com/normal-distribution-summary/)

One, however, should note that we usually use this plot to find cumulative probabilities. As stated by Failry [Nerdy](http://www.fairlynerdy.com/normal-distribution-summary/)
> You more frequently see the normal curve plotted as a probability density function (i.e. the bell curve). But most of the time when you actually use it, such as to look up the probability of something being more than 2 standard deviations away from the mean by using a Z table, you are actually using the cumulative density function.

A p-value for any particular z-score, namely $z_0$, is in fact the **cumulative probability**, or the area under curve when $z \leq z_0$ (for the sake of simplicity I do not discuss right-tailed or two-tailed situations here).
