---
title: NLP
published: true
date: '01:48 10-07-2020'
hide_git_sync_repo_link: false
visible: true
blog_url: /blog
show_sidebar: false
show_breadcrumbs: false
show_pagination: false
header_image: '0'
post_icon: file-text
hide_from_post_list: false
feed:
    limit: 10
content:
    items: '- ''@self.children'''
    limit: '5'
    order:
        by: date
        dir: desc
    pagination: '1'
    url_taxonomy_filters: '1'
bricklayer_layout: '1'
display_post_summary:
    enabled: '0'
---

# SM算法

## SM-0

### 步骤

1、将知识点记忆项尽可能的分割成最小的问-答形式；
英文：Split the knowledge into smallest possible question-answer items

2、将这些知识点记忆项以$20-40$个数量划分成一组一组的，这些组在这里被定义为**页面**（一种称谓而已，就是一对组合记忆项）；
英文：Associate items into groups containing 20-40 elements. These groups are later called pages

3、以天为间隔，以组为一次记忆单元，按照以下算法进行重复记忆: 
英文：Repeat whole pages using the following intervals (in days):)

$$
 I(i) =\begin{cases}
 1 & i = 1\\
 7 & i = 2\\
 16 & i = 3\\
 35 & i = 4\\ 
 I(i-1)*2 & i > 4
 \end{cases} 
 ，I(i)是第i-1次重复记忆的间隔
$$

4、将所有$35$天以后忘记的知识点记忆项[^1]拷贝到一个新的页面组中（并不是将其从原始的记忆Pages中删除），这些新的页面组将重复上述算法继续出现一遍记忆。

注意，第$5$次的记忆重复后，在后续的记忆过程中按照天维度会以$2$倍的天数出现。这个数据的来源基于直觉而非具体的实验结果。

## SM-2
$$
 I(i) =\begin{cases}
 1 & i = 1\\
 6 & i = 2\\
 I(i-1)*EF & n > 2\\
 \end{cases} 
$$

+ $I(i)$是第$i-1$次重复记忆的间隔;
+ $EF$是一个知识点记忆项被记住的难易程度因子

$EF$现在被称为$E-Factor$，它的值域为$[1.1,2.5]$，其中$1.1$代表最难的知识点记忆项的**记忆难易程度因子值**，$2.5$代表最简单的知识点记忆项的**记忆难易程度因子值**，一个新的知识记忆项第一次进入到所有知识记忆项的数据（集）库中时，它的记忆难易程度因子$E-Factor$的值假设等于$2.5$，所以在记忆重复的过程中，$E-Factor$的值会随着记忆的困难而降低，也就是说：一个知识记忆项越难被记住，$E-Factor$的值会越来越小，最终的体现就是该算法导致越难记住的记忆项会每隔很小的一段时间间隔就会出现一次。

> $E-Factor$的大小低于$1.3$的时候会导致知识记忆项频繁的出现，而且是该算法内在的缺点，经常无法适配`最小信息原则(minimum information principle)`。因此$E-Factor$不要低于$1.3$可以改进记忆过程中的知识记忆项的出现次数和为知识记忆项被公式计算而进行重复记忆提供参数指标。

### E-Factor

$$
EF'=f(EF,q),
$$
+ $EF'$:$E-Factor$的新值
+ $EF$:$E-Factor的旧值$
+ $q$:记忆知识记忆项质量：$0-5$或$0-3$
+ $f$:计算$EF'$的函数

函数$f$一开始是具有乘法特性的，当$E-Factor$的值在演变的过程中改变较大，必须将$f$转变为与$EF',EF$和$q$无关的。为了简化算法，最新版本的函数$f$如下：
$$
EF'=EF-0.8+0.28*q-0.02*q*q
$$
简化如下：
$$
EF'=EF+(0.1-(5-q)*(0.08+(5-q)*0.02))
$$

注意：当$q=4$的时候，$E-Factor$不变.

### 步骤
1、将所要学习的书本或者知识点成体系的尽可能的分割成最小的问答形式的知识项；
2、对1中所分割出来的知识项，设置它们的$E-Factor=2.5$；
3、按照下述的算法得出的**间隔**$I(i)$，让知识项重复显现，进行记忆：
$$
I(i) =\begin{cases}
1 & i = 1\\
6 & i = 2\\
I(i-1)*EF & n > 2\\
\end{cases} 
$$

+ $I(i)$是第$i-1$次重复记忆的间隔;
+ $EF$是一个知识点记忆项被记住的难易程度因子
+ 如果**间隔**$I(i)$的值是小数，将其向上舌入为其整数，如：$0.4$向上舍入为$1$

4、在每一个知识项按照上述的**间隔**$I(i)$出现后，用整数$0-5$来衡量知识项被当前人理解记忆好坏反应的程度。
  + $5$: 十分完美的理解记忆反应
  + $4$: 一份犹豫后且能够理解正确的记忆反应
  + $3$: 非常困难下理解正确的记忆反应
  + $2$: 错误回应；where the correct one seemed easy to recall
  + $1$: 错误回应；the correct one remembered
  + $0$: 脑子一片空白。

5、在每一次知识点记忆项出现后，且得到了当前人对于该知识点记忆项理解记忆好坏的反应程度，根据下列的公式重新计算该知识点记忆项下次出现的时间**间隔**:

$$
EF'=EF+(0.1-(5-q)*(0.08+(5-q)*0.02))
$$
+ $EF'$:$E-Factor$的新值
+ $EF$:$E-Factor的旧值$
+ $q$:记忆知识记忆项质量：$0-5$

注意：如果$EF<1.3$，设置$EF=1.3$

!!!! :fa-fire: 当前人对知识点记忆项出现时进行回忆的反应可以从$5$个等级简化为$3$个等级！


6、如果当前人对知识点记忆项出现时进行回忆的反应值小于$3$的话，那么重新以$I(1),I(2)$的方式对其进行展示，而<font color="#ff0000">无需改变</font>此时的$E-Factor$.

7、结束给定一天的所有知识记忆项的记忆后，重新记忆那些反应程度（当前人知识点记忆项理解记忆好坏的反应程度）低于$4$的所有知识记忆项。继续这些记忆直到所有知识记忆项的反应程度的值至少是$4$。

! :fa-warning:

## 附录
### 术语(Glossary)
+ 知识点记忆项：将知识分割成最小的知识点，该知识点是用来进行记忆或者理解的，该知识点尽量简化便于理解，尽量避免抽象晦涩的描述，尽可能的用图片、声音、类比等（《如何高效学习》书籍中介绍的方法）方式进行表达，它的最终形式可能是问答形式的flashcard，也可能是一段视频，或者语音，更者是其组合。