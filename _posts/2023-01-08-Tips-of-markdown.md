---
layout:     post   				    # 使用的布局（不需要改）
title:      Tips on some markdown writing  	# 标题 
subtitle:   一些使用markdown书写数学公式的tips！ #副标题
date:       2023-01-08 				# 时间
author:     Cassiel Huo  						# 作者
header-img: img/csds.jpeg 	#这篇文章标题背景图片
# header-includes:
#         - \usepackage{mathptmx}
#         - \usepackage{amsmath}
#     -\usepackage[utf8]{inputenc}
catalog: true 						# 是否归档
mathjax: true                       # 是否启用 MathJax
tags:								#标签
    - Markdown
    - Tutorial
---

> Some normal Latex format varies a little bit here when deployed on Github-Page, hope this blog helps!!

## 1. Unordered Single Line Math Equation   
Wrap the math equation with `$$` and use `\` before any special charater like using normal Latex logic. For example the following equation is created by: 

                                    $$y\sim g(y;\theta)$$  

$$y \sim g(y;\theta)$$


## 2. Ordered Single Line Math Equation

`PROBLEM EXPERIENCED` ⚠️: This numbered equation seems only works locally but not supported by github-page. Anyone have idea?

<p align="center">
    <img src="/media/ordered_equation.png" width="">
</p>


Using the `\begin{equation}` format but also wrap the math equation inside `$$`, for example the following equation is created by:

                                    $$
                                    \begin{equation}
                                        y \sim g(y;\theta)
                                    \end{equation}
                                    $$

$$
\begin{equation}
    y \sim g(y;\theta)
\end{equation}
$$

Some tutorial would tell you to include the math package inside the YAML header as: 

                                header-includes:
                                    - \usepackage{mathptmx}

But I find it's okay to omit this one, but if it doesn't work on your case maybe give it a try.

**`Update`** : Adding the above script works fine when locally testing the website, but not supported by github-page, so it will cause this blog not showing on the website!!

## 3. Multiple Line Math Equation
Write everything same as using Latex except for wrap the whole `\begin{equation}` and `\begin{split}` with `$$` outside, for example the following equation is created by:

            $$
            \begin{equation}
            \begin{split}
                \hat{\theta} &= \arg \max_{\theta} l(y;\theta) \\ 
                            &= \arg \max_{\theta} \sum_{i=1}^{N}\log g(y_i;\theta) \\
            \end{split}
            \end{equation}
            $$

$$
\begin{equation}
\begin{split}
    \hat{\theta} &= \arg \max_{\theta} l(y;\theta) \\ 
                &= \arg \max_{\theta} \sum_{i=1}^{N}\log g(y_i;\theta) \\
\end{split}
\end{equation}
$$

Maybe you can see in one markdown file every equation inside the `\begin{equation}` is consequently ordered as the above is ordered as (2)




