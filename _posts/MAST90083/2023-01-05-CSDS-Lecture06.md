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
    - CSDS
    - MAST90083
    - 课程笔记
---

# Lecture 6: Missing Data and EM 


### Note 1

The EM algorithm, also known as Expectation-Maximization, usually used as a statistical model where we want to find the maximum likelihood estimation of the hidden variable. So we can model the dataset Y as a parametric probability density model that has set of parameters $\theta$:

$$y \sim g(y;\theta)$$

We have the likelihood:

$$L(y;\theta) = g(y;\theta) = g(y_1,...,y_N ; \theta) = \prod_{i=1}^{N} g(y_i;\theta)$$

With the maximum likelihood technique as the most popular parameter estimation of $\hat{\theta}$:

$$
    \hat{\theta} = \arg \max_{\theta} L(y;\theta)
$$

## Note 2

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

---



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