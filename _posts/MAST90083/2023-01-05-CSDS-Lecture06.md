---
layout:     post   				    # 使用的布局（不需要改）
title:      CSDS Lecture 6：Missing Data and EM  	# 标题 
subtitle:   墨尔本大学 MAST90083 Computational Statistics and Data Science 课程笔记 #副标题
date:       2023-01-05 				# 时间
author:     Cassiel Huo  						# 作者
header-img: img/csds.jpeg 	#这篇文章标题背景图片
header-includes:
   - \usepackage{amsmath,amssymb}
   - \usepackage{mathptmx}
catalog: true 						# 是否归档
mathjax: true                       # 是否启用 MathJax
tags:								#标签
    - MAST90083
    - 课程笔记
---

# Lecture 6: Missing Data and EM 

> Reference: School of Mathematics & Statistics, The University of Melbourne, MAST90083 Computational Statistics and Data Mining, -- By Karim Seghouane


### `Note 1`

The EM algorithm, also known as Expectation-Maximization, usually used as a statistical model where we want to find the maximum likelihood estimation of the hidden variable. So we can model the dataset Y as a parametric probability density model that has set of parameters $\theta$:

$$y \sim g(y;\theta)$$

We have the likelihood:

$$L(y;\theta) = g(y;\theta) = g(y_1,...,y_N ; \theta) = \prod_{i=1}^{N} g(y_i;\theta)$$

With the maximum likelihood technique as the most popular parameter estimation of $\hat{\theta}$:

$$
    \hat{\theta} = \arg \max_{\theta} L(y;\theta)
$$

### Note 2: `Maximum Likelihood`

we have some definitions to introduce first:

* Score Function: 

$$ \dot{l} (y;\theta) = \sum_{i=1}^{N} \dot{l}(y_i;\theta) = \sum_{i=1}^{N} \frac{\partial l(y;\theta)}{\partial \theta} $$

* Information Matrix where I($\theta$) evaluated at $\theta = \hat{\theta}$:

$$ I(\theta) = -\sum_{i=1}^{N} \frac{\partial^2 l(y_i;\theta)}{\partial \theta \partial \theta ^{T}}$$

*  Fisher Information or Expected Information:

$$ i(\theta) = E_{\theta}[I(\theta)] $$

The sampling distribution of maximum likelihood estimator $\hat{\theta}$ follows a normal distribution ,where $\theta_0$ denotes the true value of $\theta$, and can be approximated by the following: 

$$
\begin{equation}
    \hat{\theta} \rightarrow{} N (\theta_0, i(\theta_0)^{-1}) 
\end{equation}
$$

$$
\begin{equation}
    \hat{\theta} \sim N (\hat{\theta}, I(\hat{\theta})^{-1})
\end{equation}
$$

Then the corresponding standard error of $\hat{\theta_j} = \sqrt{I(\hat{\theta})_{jj}^{-1}}$



### Note 3: `Local Likelihood`

Allocating observation weights can make parametric model local, where parameter $\theta$ at location $z_0$ = likelihood * kernel:

$$
 \begin{equation}
     l(z;\theta(z_0)) = \sum_{i=1}^{N} K_h (Z_0,Z_i) l(z_i;\theta(z_0))
 \end{equation}
$$

Where for $Z_i$ far away from $Z_0$, the effect on likelihood is less. E.g. $l(z,\theta) = (y-X^T\theta)^2$ fits a linear varying coefficient model that maximize local likelihood.


### Note 4: `Kullback-Leibler Divergence`

To see how to using KL Divergence for parameter estimation: Kullback-Leibler Divergence measures the distance between two probalistic densities, when KL value =0 indicates two pdf equals to each other, other wise positive. Some identities here:

* Empirical Density:

    $$
    g_N(y) = \frac{1}{N} \sum_{i=1}^{N} \delta(y-y_i)
    $$

    Which the effect of this is to put a $\frac{1}{N}$ mass on every $y_i$ (as line number 3 from following), then writing the formula of $\hat{\theta}$:


    $$
    \begin{equation}
    \begin{split}
        \hat{\theta} &= \arg \max_{\theta} l(y;\theta) \\ 
                    &= \arg \max_{\theta} \sum_{i=1}^{N}\log g(y_i;\theta) \\
                    &= \arg \max_{\theta} \int \log g(y;\theta) g_N(y) dy \\
                    &= \arg \max_{\theta} \int \log g(y;\theta) \,dg_N(y) \\
                    &= \arg \min_{\theta} [\int \log g(y;\theta_0) \,dg_N(y) - \int \log g(y;\theta) \,dg_N(y)] \\
                    &=  \arg \min_{\theta} [\int \log g(y;\theta_0) \,dG(y;\theta_0) - \int \log g(y;\theta) \,dG(y;\theta)] \\
                    &= \arg \min_{\theta} KL[g(y;\theta_0),g(y;\theta)]
    \end{split}
    \end{equation}
    $$

We say ML estimation (Maximum Likelihood Estimation) works as minimise KLD between candidate model and true model, or between family of parameterized distributions and true distribution.

### Note 5: `Multiple Distributions`

$$
\begin{equation}
\begin{split}
    y_1 \sim N(\mu_1, \sigma_1^2) \quad  y_2 \sim N(\mu_2, \sigma_2^2) \\
\end{split}
\end{equation}
$$ 

We can then write $y \sim (1-Z)y_1+Zy_2$ with $Z \in $ \{0,1\} and p(Z=1) = $\pi$ is the mixing coefficient.    

Let's list some terminologies:

* Joint Density in mixture:

    $$
    \begin{equation}
        p(y) = (1-\pi)\phi_{\theta_1}(y) + \pi \phi_{\theta_2}(y) = \sum_{i=1}^{2} m_i\phi_{\theta_i} (y)
    \end{equation}
    $$ 

    Where $m_1 = 1-\pi$, $m_2 = \pi$, $\sum m_i = 1$ , and $\phi (y)$ is the normal density of y

* The likelihood:

    $$
    \begin{equation}
        l(y;\theta) = \sum_{i=1}^{N} \log [(1-\pi)\phi_{\theta_1}(y_i) + \pi \phi_{\theta_2}(y_i)]
    \end{equation}
    $$

* Marginal density on latent variable Z:

    $$
    \begin{equation}
        p(Z) = \pi ^{Z} (1-\pi)^{1-Z} = 
        \begin{cases}
            (1-\pi) &\text{if Z=0} \\
            \pi &\text{if Z=1}
        \end{cases}
    \end{equation}
    $$

* Conditional density of observed data on Z:

    $$
    \begin{equation}
        p(y|Z) = \phi_{\theta_2}(y)^{Z} + \phi_{\theta_1}(y)^{1-Z} =
        \begin{cases}
            \hat{\phi}_{\theta_1} (y) &\text{if Z=0} \\
            \hat{\phi}_{\theta_2} (y) &\text{if Z=1}
        \end{cases}
    \end{equation}
    $$

Then if we combine the conditional density and marginal density we have together the joint density:

$$
\begin{equation}
\begin{split}
    p(y) &= \int p(y,Z) dZ = \sum_{Z} p(y,Z) \\
        &= \sum_{Z} p(y|Z) p(Z) \\
        &= \pi \phi_{\theta_2} (y) +(1-\pi) \phi_{\theta_1}(y)
\end{split}
\end{equation}
$$

### Note 6: `EM`

First use $\gamma(Z)$ to denote p(Z=1\|y), the conditional probability of latent variable Z, once we have observed y, using [Bayes Theorem](https://en.wikipedia.org/wiki/Bayes%27_theorem) :

$$
\begin{equation}
    \gamma(Z) = p(Z=1|y) = \frac{p(Z=1)p(y|Z=1)}{p(y)} = \frac{p(Z=1)p(y|Z=1)}{\pi \phi_{\theta_2} (y) +(1-\pi) \phi_{\theta_1}(y)}
\end{equation}
$$

Where $\pi$ is the probability of Z=1, and we can think $\gamma(Z)$ as the responsibility that $\phi_{\theta_2}$ takes for explaining the observation y. (Or the weight)

**`NOW HERE IS MAJOR EM !!!!!`**

 * Expectation Step:

    $$
    \begin{equation}
        \gamma_i = \frac{\hat{\pi}\phi_{\hat{\theta}_2}(y_i)}{\hat{\pi}\phi_{\hat{\theta}_2}(y_i) + (1-\hat{\pi})\phi_{\hat{\theta}_1}(y_i)}    \qquad  \text{i = 1,...,N}
    \end{equation}
    $$

* Maximization Step:

    $$
    \begin{equation}
        \hat{\mu_1} = \frac{\sum_{i=1}^{N}(1-\hat{\gamma_i})y_i}{\sum_{i=1}^{N}(1-\hat{\gamma_i})}   \qquad    \hat{\sigma_1^2} = \frac{\sum_{i=1}^{N}(1-\hat{\gamma_i})(y_i-\hat{\mu_1})^2}{\sum_{i=1}^{N}(1-\hat{\gamma_i})} 
    \end{equation}
    $$

    $$
    \begin{equation}
        \hat{\mu_2} = \frac{\sum_{i=1}^{N}\hat{\gamma_i}y_i}{\sum_{i=1}^{N}\hat{\gamma_i}}   \qquad   \hat{\sigma_2^2} = \frac{\sum_{i=1}^{N}\hat{\gamma_i}(y_i-\hat{\mu_2})^2}{\sum_{i=1}^{N}\hat{\gamma_i}}
    \end{equation}
    $$

    **Note:** since we have $\sum \pi_i = 1$, thus if we assume more than two distributions (e.g. 3), then simply initialise $\pi_i = \frac{1}{3}$ 

* Update Step:

    $$
    \begin{equation}
        \hat{\pi} = \frac{\sum_{i=1}^{N}\hat{\gamma_i}}{N} 
    \end{equation}
    $$

    $$
    \begin{equation}
    \begin{split}
        l(y,Z,\theta) &= \sum_{i=1}^{N} [(1-Z_i)\log \phi_{\theta_1}(y_i) + Z_i \log \phi_{\theta_2}(y_i)] \\
                    &+ \sum_{i=1}^{N} [(1-Z_i)\log (1-\pi) + Z_i \log (\pi)] 
    \end{split}
    \end{equation}
    $$