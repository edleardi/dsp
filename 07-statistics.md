# Statistics

# Table of Contents

[1. Introduction](#section-a)  
[2. Why We Are Using Think Stats](#section-b)  
[3. Instructions for Cloning the Repo](#section-c)  
[4. Required Exercises](#section-d)  
[5. Optional Exercises](#section-e)  
[6. Recommended Reading](#section-f)  
[7. Resources](#section-g)

## <a name="section-a"></a>1.  Introduction

[<img src="img/think_stats.jpg" title="Think Stats"/>](http://greenteapress.com/thinkstats2/)

Use Allen Downey's [Think Stats (second edition)](http://greenteapress.com/thinkstats2/) book for getting up to speed with core ideas in statistics and how to approach them programmatically. This book is available online, or you can buy a paper copy if you would like.

Use this book as a reference when answering the 6 required statistics questions below.  The Think Stats book is approximately 200 pages in length.  **It is recommended that you read the entire book, particularly if you are less familiar with introductory statistical concepts.**

Complete the following exercises along with the questions in this file. Some can be solved using code provided with the book. The preface of Think Stats [explains](http://greenteapress.com/thinkstats2/html/thinkstats2001.html#toc2) how to use the code.  

Communicate the problem, how you solved it, and the solution, within each of the following [markdown](https://guides.github.com/features/mastering-markdown/) files. (You can include code blocks and images within markdown.)

## <a name="section-b"></a>2.  Why We Are Using Think Stats 

The stats exercises have been chosen to introduce/solidify some relevant statistical concepts related to data science.  The solutions for these exercises are available in the [ThinkStats repository on GitHub](https://github.com/AllenDowney/ThinkStats2).  You should focus on understanding the statistical concepts, python programming and interpreting the results.  If you are stuck, review the solutions and recode the python in a way that is more understandable to you. 

For example, in the first exercise, the author has already written a function to compute Cohen's D.  **You could import it, or you could write your own code to practice python and develop a deeper understanding of the concept.** 

Think Stats uses a higher degree of python complexity from the python tutorials and introductions to python concepts, and that is intentional to prepare you for the bootcamp.  

**One of the skills to learn here is to understand other people’s code.  And this author is quite experienced, so it’s good to learn how functions and imports work.**

---

## <a name="section-c"></a>3.  Instructions for Cloning the Repo 
Using the [code referenced in the book](https://github.com/AllenDowney/ThinkStats2), follow the step-by-step instructions below.  

**Step 1. Create a directory on your computer where you will do the prework.  Below is an example:**

```
(Mac):      /Users/yourname/ds/metis/metisgh/prework  
(Windows):  C:/ds/metis/metisgh/prework
```

**Step 2. cd into the prework directory.  Use GitHub to pull this repo to your computer.**

```
$ git clone https://github.com/AllenDowney/ThinkStats2.git
```

**Step 3.  Put your ipython notebook or python code files in this directory (that way, it can pull the needed dependencies):**

```
(Mac):     /Users/yourname/ds/metis/metisgh/prework/ThinkStats2/code  
(Windows):  C:/ds/metis/metisgh/prework/ThinkStats2/code
```

---


## <a name="section-d"></a>4.  Required Exercises

*Include your Python code, results and explanation (where applicable).*

### Q1. [Think Stats Chapter 2 Exercise 4](statistics/2-4-cohens_d.md) (effect size of Cohen's d)  
Cohen's D is an example of effect size.  Other examples of effect size are:  correlation between two variables, mean difference, regression coefficients and standardized test statistics such as: t, Z, F, etc. In this example, you will compute Cohen's D to quantify (or measure) the difference between two groups of data.   

You will see effect size again and again in results of algorithms that are run in data science.  For instance, in the bootcamp, when you run a regression analysis, you will recognize the t-statistic as an example of effect size.


    firsts = live[live.birthord == 1]
    others = live[live.birthord != 1]
    first_hist = thinkstats2.Hist(firsts.totalwgt_lb)
    other_hist = thinkstats2.Hist(others.totalwgt_lb)
    width = 0.2
    thinkplot.PrePlot(2)
    thinkplot.Hist(first_hist, align='right', width=width)
    thinkplot.Hist(other_hist, align='left', width=width)
    thinkplot.Show(xlabel='weeks', ylabel='frequency', xlim=[0, 16])

Looks like first babies might be lighter than others (dark blue = first_hist, light blue = other_hist)

    def CohenEffectSize(group1, group2):
        diff = group1.mean() - group2.mean()
        var1 = group1.var()
        var2 = group2.var()
        n1, n2 = len(group1), len(group2)
        pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
        d = diff / math.sqrt(pooled_var)
        return d
    CES = CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb)
    print(CES)

Difference of 0.089 standard deviations which is small. Similar to the difference in pregnancy lengths between first and other babies of 0.029


### Q2. [Think Stats Chapter 3 Exercise 1](statistics/3-1-actual_biased.md) (actual vs. biased)
This problem presents a robust example of actual vs biased data.  As a data scientist, it will be important to examine not only the data that is available, but also the data that may be missing but highly relevant.  You will see how the absence of this relevant data will bias a dataset, its distribution, and ultimately, its statistical interpretation.

    df = nsfg.ReadFemResp()
    kids = df.numkdhh
    kidspmf = thinkstats2.Pmf(kids)
    print(kidspmf)
    kidspmf_bias = BiasPmf(kidspmf)
    print(kidspmf_bias)

>>> Pmf({0: 0.46617820227659301, 1: 0.21405207379301322, 2: 0.19625801386889966, 3: 0.087138558157791451, 4: 0.025644380478869556, 5: 0.010728771424833181})

>>> Pmf({0: 0.0, 1: 0.20899335717935616, 2: 0.38323965252938175, 3: 0.25523760858456823, 4: 0.10015329586101177, 5: 0.052376085845682166})

    thinkplot.PrePlot(2)
    thinkplot.Pmfs([kidspmf, kidspmf_bias])
    thinkplot.Show(xlabel='num of kids', ylabel='PMF')

>>> graph

    kidspmf_mean = 0.0
    for i, prob in kidspmf.d.items():
            kidspmf_mean += prob * i
    print(kidspmf_mean)

    kidspmf_bias_mean = 0.0
    for i, prob in kidspmf_bias.d.items():
        kidspmf_bias_mean += prob * i
    print(kidspmf_bias_mean)

>>> 1.02420515504

>>> 2.40367910066

Effect size calculated by finding the difference in means shows that the class size bias for this data is really significant!

### Q3. [Think Stats Chapter 4 Exercise 2](statistics/4-2-random_dist.md) (random distribution)  
This questions asks you to examine the function that produces random numbers.  Is it really random?  A good way to test that is to examine the pmf and cdf of the list of random numbers and visualize the distribution.  If you're not sure what pmf is, read more about it in Chapter 3.  

    import random
    import thinkplot
    import thinkstats2

    count = 0
    stop = 1000
    numbers = []
    while count <= stop:
        count += 1 
        i = random.randint(1,1001)
        numbers.append(i)

    rand_pmf = thinkstats2.Pmf(numbers)
    rand_cdf = thinkstats2.Cdf(numbers)

PMF Graph

    width = 0.05
    thinkplot.PrePlot(1)
    thinkplot.Pmf(rand_pmf)
    thinkplot.Show(xlabel='weeks', axis=[1, 1000, 0, 0.008])

CDF Graph

    thinkplot.PrePlot(1)
    thinkplot.Cdf(rand_cdf)
    thinkplot.Show(xlabel='weight', ylabel='CDF')

The CDF graph is approximately a straight line, which means that the distribution is uniform. The PMF varied anywhere from 0 to 8 occurences of the same number. 

### Q4. [Think Stats Chapter 5 Exercise 1](statistics/5-1-blue_men.md) (normal distribution of blue men)
This is a classic example of hypothesis testing using the normal distribution.  The effect size used here is the Z-statistic. 

Import brfss data and find height column segmented for men

    brfss_data = ReadBrfss()
    men = brfss_data[brfss_data.sex == 1]
    heights = men.htm3

Check mean and std to make sure sex == 1 is male

    mean = heights.mean()
    std = heights.std()

Write in scipy function from chapter

    import scipy
    def EvalNormalCdf(x, mu=0, sigma=1):
        return scipy.stats.norm.cdf(x, loc=mu, scale=sigma)

Convert inches to cm
6'1" = 185 cm
5'10" = 183 cm

Apply function to find answer

    sixone = EvalNormalCdf(185, 178, 7.7)
    fiveten = EvalNormalCdf(183, 178, 7.7)
    cdf_answer = sixone - fiveten
    print(cdf_answer)

0.0764 or ~8% of are between 5'10" and 6'1" 


### Q5. Bayesian (Elvis Presley twin) 

Bayes' Theorem is an important tool in understanding what we really know, given evidence of other information we have, in a quantitative way.  It helps incorporate conditional probabilities into our conclusions.

Elvis Presley had a twin brother who died at birth.  What is the probability that Elvis was an identical twin? Assume we observe the following probabilities in the population: fraternal twin is 1/125 and identical twin is 1/300.  

RV Defintions:
K - twin brothers
I - identical twins
E - fraternal twins

Want: 
P(I|K) - probability Elivs was an identical twin given that he had a twin

Bayes Formula:
P(I|K) = (P(K|I) * P(I)) / P(K)
P(I) = 1/300
P(E) 1/125
P(K|I) = 1/2
P(K) = (P(I) * P(K|I)) + (P(E) * P(K|E)) = (1/300 * 1/2) + (1/125 * 1/2 * 1/2)
P(I|K) = 5/11

### Q6. Bayesian &amp; Frequentist Comparison  
How do frequentist and Bayesian statistics compare?

Frequentist statistics evaluates sample data by focusing on the frequency of occurences in the data. Bayesian statistics evaluates sample data by updating the probability of a hypothesis with extra information. Bayesian reasoning involves frequentist reasoning. Bayes theorem essentially says the probability of a hypothesis given a piece of evidence is equal to the probability of the evidence given the hypothesis times the probability of the hypothesis (a frequentist calculation) divided by the probability of the evidence (a frequentist calculation).


## <a name="section-e"></a>5.  Optional Exercises

The following exercises are optional, but we highly encourage you to complete them if you have the time.

### Q7. [Think Stats Chapter 7 Exercise 1](statistics/7-1-weight_vs_age.md) (correlation of weight vs. age)
In this exercise, you will compute the effect size of correlation.  Correlation measures the relationship of two variables, and data science is about exploring relationships in data.    

### Q8. [Think Stats Chapter 8 Exercise 2](statistics/8-2-sampling_dist.md) (sampling distribution)
In the theoretical world, all data related to an experiment or a scientific problem would be available.  In the real world, some subset of that data is available.  This exercise asks you to take samples from an exponential distribution and examine how the standard error and confidence intervals vary with the sample size.

### Q9. [Think Stats Chapter 6 Exercise 1](statistics/6-1-household_income.md) (skewness of household income)
### Q10. [Think Stats Chapter 8 Exercise 3](statistics/8-3-scoring.md) (scoring)
### Q11. [Think Stats Chapter 9 Exercise 2](statistics/9-2-resampling.md) (resampling)

---

## <a name="section-f"></a>6.  Recommended Reading

Read Allen Downey's [Think Bayes](http://greenteapress.com/thinkbayes/) book.  It is available online for free, or you can buy a paper copy if you would like.

[<img src="img/think_bayes.png" title="Think Bayes"/>](http://greenteapress.com/thinkbayes/) 

---

## <a name="section-g"></a>7.  More Resources

Some people enjoy video content such as Khan Academy's [Probability and Statistics](https://www.khanacademy.org/math/probability) or the much longer and more in-depth Harvard [Statistics 110](https://www.youtube.com/playlist?list=PL2SOU6wwxB0uwwH80KTQ6ht66KWxbzTIo). You might also be interested in the book [Statistics Done Wrong](http://www.statisticsdonewrong.com/) or a very short [overview](http://schoolofdata.org/handbook/courses/the-math-you-need-to-start/) from School of Data.
