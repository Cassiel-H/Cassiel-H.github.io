---
layout:     post   				    # 使用的布局（不需要改）
title:      CSDS Lecture 6：Missing Data and EM  	# 标题 
subtitle:   墨尔本大学 MAST90083 Computational Statistics and Data Science 课程笔记 #副标题
date:       2023-01-05 				# 时间
author:     Cassiel Huo  						# 作者
header-img: img/csds.jpeg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
mathjax: true                       # 是否启用 MathJax
tags:								#标签
    - CSDS
    - MAST90083
    - 课程笔记
---

# Lecture 6: Missing Data and EM 


### Note 1


Model the dataset as a parametric probability density model:

$$y \sim g(y;\theta)$$

We have the likelihood:

$$L(y;\theta) = g(y;\theta) = g(y_1,...,y_N ; \theta) = \prod_{i=1}^{N} g(y_i;\theta)$$
