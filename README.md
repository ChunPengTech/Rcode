# Rcode

## Some recommended books

[Cookbook for R 中文版](https://openbiox.github.io/Cookbook-for-R-Chinese/index.html)

[R for Data Science (2e)](https://r4ds.hadley.nz/)

[ggplot2: Elegant Graphics for Data Analysis (3e)](https://ggplot2-book.org/)

[Welcome to ModernDive (v2) | Statistical Inference via Data Science](https://moderndive.com/v2/index.html)

[R语言实战机器学习](https://ayueme.github.io/machine_learning_base_r/)



> ---
>
> # 实证分析一般范式及常用方法梳理（问卷数据）
>
> ---
>
> <center><font face="楷体" size=3>彭春 2024.12.02</font></center>


<center><font face="黑体" size=4>目录</font></center>

[toc]



**需要预先安装的R包**

```R
install.packages("tidyverse")
install.packages("bruceR")
install.packages(c("autoReg","moonbook"))
install.packages("mediation")
install.packages(c("lavaan","semTools"))
install.packafes("tidySEM")
install.packages("blavaan")
install.packages("seminr")
install.packages("powerMediation")
install.packages("semPower")
install.packages("sjPlots")
```



**导入数据**

```R
library(bruceR)
set.wd()
data_inf <- import("basic info.xlsx", as = "data.frame")
data <- import("data304n.csv", as = "data.frame")
```



## 受访者基本信息统计

`样本人口统计特征表`



## 共同方法偏差 (Common method bias, CMB)

**CB SEM** : <a href="#Williams & McGonagle 2016">Williams & McGonagle (2016)</a> 提出了四种用于评估和控制 CMV 的潜变量验证性因子分析模型设计。<a href="#汤丹丹 & 温忠麟 2020">汤丹丹 & 温忠麟 (2020)</a> 从数学模型角度分析 CMV 的影响，并讨论了 CMB 常用的检验法，给出了 CMB 检验的建议。

**PLS-SEM** : <a href="#Tehseen et al 2017">Tehseen et al. (2017)</a> 围绕着如何使用 PLS 检验和控制共同方法偏差进行综述和探讨，并建议同时使用程序性和统计性补救措施，以检验和控制 CMV 对研究结果的影响。

### Harman’s single-factor test

未旋转的第一因子提取方差占总方差比重未超过 40% 或 50% <a href="#Podsakoff et al 2003">(Podsakoff et al., 2003;</a> <a href="#周浩 & 龙立荣 2004">周浩 & 龙立荣, 2004)</a>，但无论是 40% 还是 50% 都是经验说法。



### 控制不可测量的潜在方法因子（ULMC）

在原有特定因子的基础上，将所有项目作为方法因子（一般因子）的指标，建立双因子模型 (Bifactor model)。将方法因子作为全局因子,  特定因子作为局部因子，特定因子间要设置相关。一般认为若双因子模型与仅含特定因子的模型差异显著，则 CMB 严重 <a href="#Podsakoff et al 2003">(Podsakoff et al., 2003)</a>。更进一步的，<a href="#Chen et al 2012">Chen et al. (2012)</a> 认为双因子模型中的一般因子与特定因子之间应保持无相关性，特定因子之间也应保持无相关性。这种正交性的设定排除了因子之间可能存在的高度共线性，确保了模型的准确性和可解释性。



### 单因素模型

单因素模型的拟合指标比原模型差很多，即可证明无严重共同方法偏差



### 相关性

相关系数小于 0.9 <a href="#Bagozzi et al 1991">(Bagozzi et al., 1991)</a> 



### 共线性

PLS-SEM中可以添加一个无关变量并使用内部模型的共线性 (VIF< 3.3) 对共同方法偏差进行检验 



## 信效度分析 (Reliability and validity test)

### 信度

分量表的内部一致性使用 Cronbach's alpha (α) 计算。α > 0.7 说明有足够的信度，最好加上置信区间 <a href="#Kelley & Pornprasertmanit 2016">(Kelley & Pornprasertmanit., 2016;</a> <a href="#McNeish 2018">McNeish, 2018)</a> 



###  聚敛效度 (Convergent validity)

### 区分效度 (Discriminant validity)

#### Fornell-Larcker criterion

区分效度可以通过比较任意两个构念的 AVE 的平方根和构念之间的相关性估计来评估 <a href="#Fornell & Larcker 1981">(Fornell & Larcker ,1981)</a> 

#### HTMT ratio

严格阈值为 0.85，自由阈值为 0.90 <a href="#Henseler et al 2015">(Henseler et al., 2015)</a> 

#### 交叉载荷 (Cross-loading)

 <a href="#Chin 1998">(Chin, 1998)</a> 

#### 卡方差异检验

构建包含不同因子个数的验证性因子模型，若其他模型与原模型相比，各拟合指标均变差，且卡方检验显著，则说明原模型区分效度较好 <a href="#沈伊默 et al 2019">(沈伊默等, 2019;</a><a href="#郑少芳 et al 2020"> 郑少芳等, 2020)</a> 

|      | Model           | χ2       | df   | χ2/df | CFI   | TLI   | RMSEA | SRMR  | 模型比较 | Δχ2         | Δdf  |      |
| ---- | --------------- | -------- | ---- | ----- | ----- | ----- | ----- | ----- | -------- | ----------- | ---- | ---- |
|      | 1.Four-factor   | 379.806  | 203  | 1.871 | 0.96  | 0.954 | 0.054 | 0.033 |          |             |      |      |
|      | 2.Three-factor  | 577.646  | 206  | 2.804 | 0.915 | 0.905 | 0.078 | 0.045 | 2 vs. 1  | 197.840\*** | 3    |      |
|      | 3.Two-factor    | 745.921  | 208  | 3.586 | 0.877 | 0.864 | 0.093 | 0.055 | 3 vs. 1  | 366.115\*** | 5    |      |
|      | 4.Single-factor | 1019.399 | 209  | 4.878 | 0.815 | 0.796 | 0.114 | 0.068 | 4 vs. 1  | 639.593\*** | 6    |      |
|      | 5.Bifactor      | 360.755  | 187  | 1.929 | 0.96  | 0.951 | 0.056 | 0.032 | 5 vs. 1  | 19.051      | 16   |      |



## 均值、标准差与相关性分析 (Mean, stand deviation and  correlation analysis)



## 假设检验 (Hypothesis testing)

`SEM（PLS-SEM、CB SEM、Bayesian-SEM）` `Regression`

### 中介效应检验 (Mediation effect test)

#### 因果逐步法 (Casual step method)

$$
Y=cX+e_1··········(1)\\
M=aX+e_2··········(2)\\
Y=c'X+bM+e_3·····(3)
$$

逐步检验回归系数的方法分为三步 <a href="#Baron & Kenny 1986">(Baron & Kenny, 1986</a>;<a href="#温忠麟 et al 2004"> 温忠麟等, 2004)</a> 

- 第一步：检验方程 (1) 的系数 c，也就是自变量 X 对因变量 Y 的总效应
- 第二步：检验方程 (2) 的系数 a，也就是自变量 X 和 中介变量 M 的关系
- 第三步：控制中介变量 M 后，检验方程 (3) 的系数 c’ 和系数 b 

**注**

- 逐步检验的检验力在各种方法中最低，当中介效应较弱时，逐步法很难检验出中介效应显著的结果。但反过来，<a href="#温忠麟 & 叶宝娟 2014">温忠麟 & 叶宝娟 (2014)</a> 提出如果用逐步法已经得到显著的结果，检验力低的问题就不再是问题。
- 方程 (1) 的系数 c 显著是逐步法的基础，但在有些情况下 c 不显著恰恰是受到了中介效应的影响（即，抑制 / 遮掩模型）。现在，对中介效应存在的条件进一步简化，如 <a href="#Zhao et al 2010">Zhao et al. (2014)</a> 认为只需要满足在模型中加入中介变量时，自变量对因变量的影响减小即可。因为即使没有自变量的直接影响，中介效应也可能发生。由此，<a href="#温忠麟 & 叶宝娟 2014">温忠麟 & 叶宝娟 (2014)</a> 总结提出了一个新的中介效应分析流程。

#### 江艇两步法

考虑到xx，<a href="#江艇 2022">江艇 (2022)</a> 提出了一种新的中介效应检验方法
$$
Y=cX+e_1··········(1)\\
M=aX+e_2··········(2)\\
$$
若沿用江艇两步法，只需要检验总效应 c 和中介前半段 a，后半段使用相关具有强说服力的文献进行验证即可。

#### 系数乘积法

$$
Y=(ab+c')X+be_2+e_3
$$

检验系数乘积是直接针对假设 $H0: ab = 0$ 提出的检验方法。以下主要介绍两种常用方法。

**Sobel Test**

<a href="#Sobel 1982">Sobel (1982)</a> 提出了一种基于抽样分布为正态分布的检验法对中介效应进行检验。

检验统计量为 $z=\hat{a}\hat{b}/s_{ab}$，其中 $\hat{a}$ 和 $\hat{b}$ 分别是 a 和 b 的估计值， $\hat{a}\hat{b}$ 的标准误为：$se(ab)=\sqrt{\hat{b}^2 se_a^2 +\hat{a}^2se_b^2}$。$se_a$ 和 $se_b$ 分别是 $\hat{a}$ 和 $\hat{b}$ 的标准误。$|z| ＞ 1.96$，说明 $p < 0.05$，中介效应存在。



|      |      | z         |      |      | p         |      |      |
| ---- | ---- | --------- | ---- | ---- | --------- | ---- | ---- |
|      |      | z > 1.96  |      |      | p < 0.05  |      |      |
|      |      | z > 2..58 |      |      | p < 0.01  |      |      |
|      |      | z > 3.29  |      |      | p < 0.001 |      |      |

- 模拟研究发现，Sobel 法的检验力高于逐步法，也就是说 Sobel 可以检验出比前者更多的中介效应，但如果两种方法检验的结果都显著，逐步检验结果要强于 Sobel 检验结果 <a href="#温忠麟 et al 2004">(温忠麟等, 2004)</a>，所以先进行依次检验, 不显著才需要做 Sobel 检验
- 检验系数乘积的统计量推导需要假设 $\hat{a}\hat{b}$ 服从正态分布，这一点很难保证，因为即使 $\hat{a}$ 和  $\hat{b}$ 服从正态分布也无法保证两者的乘积服从正态分布，因而 Sobel 检验也存在一定的局限性。

**Bootstrapping**

基于抽样分布为非正态分布的Bootstrap抽样法是目前最常用和最理想的中介效应检验方法，且重复抽样次数需要在 1000 次及以上 <a href="#Preacher & Hayes 2008">(Preacher & Hayes, 2008)</a> 

- Bootstrap 的前提条件是样本能够代表总体
- 模拟研究发现，与其他中介效应检验方法相比，Bootstrap 具有较高的统计效力，Bootstrap 法是公认的可以取代 Sobel 方法而直接检验系数乘积的方法 <a href="#温忠麟 & 叶宝娟 2014">(温忠麟 & 叶宝娟, 2014)</a> 

#### 系数差异法

差异系数检验的是 $H0: c-c'=0$，因为通常情况下，$ab=c-c'$，因此，乘积系数法和差异系数法的检验效力是基本上相同的，区别在于两者的标准误不同。差异系数检验方法犯错的概率要高于系数乘积检验法 <a href="#温忠麟 et al 2004">(温忠麟等, 2004)</a>，很少使用。

### 调节效应检验 (Moderation effect test)

#### 乘积指标法 (Product indicator approach)

潜变量指标的乘积生成交互项指标，然后，交互项被视为一个单独的因子来预测结果变量 <a href="#Kenny & Judd 1984">(Kenny & Judd, 1984)</a> 

乘积指标有多种生成策略，策略的差异性会导致其分析结果存在差异。同时乘积项是非正态分布，基于正态分布假设的参数估计结果可能产生偏差。

#### 潜调节结构方程模型法 (Latent moderated structural equations method)

建立基准模型和包含潜调节(交互)项的有调节的中介结构方程模型，将两者的拟合指数进行比较，对比含潜调节(交互)项的模型的拟合情况是否更好 <a href="#Maslowsky et al 2015">(Maslowsky et al., 2015)</a>。先构造不带交互项的基准模型 (model 0) 获取拟合指数，再与含潜调节(交互)项的的模型 (model 1) 的 AIC 和 H0 进行比较，检查模型是否优化

主要思路：如果model 0 拟合很好，且根据对数似然比检验，model 1 的拟合度相对于 model 0 有显著提升，则可以得出结论，model 1 也是一个拟合很好的模型。

- 判断无交互项的 AIC  - 有交互项的 AIC  ≥ 0；

- 根据 H0 计算基准模型和有交互项模型的对数似然比之差，将其进行卡方检验。其中，χ^2^ = -2*(无交互项的 H0 - 有交互项的 H0)，df =有交互项的自由参数 - 无交互项的自由参数。

### 有调节的中介效应 (Moderated Mediation effect test)

## 其他

### 异常值 (Outlier)

### 效应量、样本量与检验功效 (Effect size, sample size and power)

#### G*power

[Universität Düsseldorf: G*Power](https://www.psychologie.hhu.de/arbeitsgruppen/allgemeine-psychologie-und-arbeitspsychologie/gpower) 

#### Free Statistics Calculators

[Free A-priori Sample Size Calculator for Structural Equation Models - Free Statistics Calculators](https://www.danielsoper.com/statcalc/calculator.aspx?id=89) 

#### Power Analysis in R

**semPower package**



**powerMediation package**



### 多重共线性 (Multicollinearity)

### 稳健性检验 (Robustness test)

### CB SEM、PLS-SEM 还是 Bayesian SEM ？



PLS

Ghasemy, M., Teeroovengadum, V., Becker, J.-M., & Ringle, C. M. (2020). This fast car can move faster: A review of PLS-SEM application in higher education research. *Higher Education*, *80*(6), 1121-1152.



## 示例

### Multiple Linear Regression in R



### CB SEM in R (lavaan package)

#### 验证性因子分析



获取拟合指数

|      |      | R包         |      |      | 函数           |      |      |
| ---- | ---- | ----------- | ---- | ---- | -------------- | ---- | ---- |
|      |      | bruceR      |      |      | lavaan_summary |      |      |
|      |      | tidySEM     |      |      | table_fit      |      |      |
|      |      | performance |      |      | performance    |      |      |
|      |      | lavaan      |      |      | fitmeasures    |      |      |
|      |      | broom       |      |      | glance         |      |      |



#### 路径分析



|      |      | R包        |      |      | 函数           |      |      |
| ---- | ---- | ---------- | ---- | ---- | -------------- | ---- | ---- |
|      |      | bruceR     |      |      | lavaan_summary |      |      |
|      |      | broom      |      |      | tidy           |      |      |
|      |      | parameters |      |      | parameters     |      |      |
|      |      | base       |      |      | summary        |      |      |



### PLS-SEM in R (seminr package)

#### 测量模型

#### 结构模型



### Bayesian-SEM

有学者认为，当前使用最大似然 （ML） 和似然比卡方检验的分析不必要地应用了严格的模型来表示来自实质性理论的假设。这通常会导致对模型的拒绝和利用一系列可能的机会对模型修改。因此，<a href="#Muthén & Asparouhov 2012">Muthén & Asparouhov (2012)</a> 提出了一种使用贝叶斯分析进行因子分析和结构方程建模的新方法。

基于抽样的贝叶斯方法较少的依赖大样本渐进理论，在小样本和复杂模型中依旧表现良好，对于潜变量的测量测量和结构模型的估计部分非常有用。 <a href="#张沥今 et al 2019">张沥今等 (2019)</a> 介绍了贝叶斯结构方程模型的方法基础和优良特性及几类常用的贝叶斯结构方程模型及其应用现状。[基于贝叶斯估计的结构方程模型 in Mplus (张沥今, 2019)](https://lijinzhang.com/share/190525_r_bsem.pdf) 

#### Bayesian-SEM in Amos

[贝叶斯结构方程模型（Bayesian-SEM）简介及AMOS实现](https://zhuanlan.zhihu.com/p/432443299) 

#### Bayesian-SEM in R (blavaan package)



## 参考文献

<a name="江艇 2022">江艇. (2022). 因果推断经验研究中的中介效应与调节效应. *中国工业经济*, *5*, 100–120. </a>

<a name="沈伊默 et al 2019">沈伊默, 马晨露, 白新文, 诸彦含, 鲁云林, 张庆林, & 刘军. (2019). 辱虐管理与员工创造力: 心理契约破坏和中庸思维的不同作用. *心理学报*, *51*(2), 238.</a> 

<a name="汤丹丹 & 温忠麟 2020">汤丹丹 & 温忠麟. (2020). 共同方法偏差检验：问题与建议. *心理科学*, *43*(1), 215–223. </a>

<a name="温忠麟 & 叶宝娟 2014">温忠麟 & 叶宝娟. (2014). 中介效应分析:方法和模型发展. *心理科学进展*, *22*(05), 731–745.</a>

<a name="温忠麟 et al 2004">温忠麟, 张雷, 侯杰泰, & 刘红云. (2004). 中介效应检验程序及其应用. *心理学报*, *36*(5), 614-620.</a>

<a name="周浩 & 龙立荣 2004">周浩 & 龙立荣. (2004). 共同方法偏差的统计检验与控制方法. *心理科学进展*, *6*, 942–950.</a>

<a name="张沥今 et al 2019">张沥今, 陆嘉琦, 魏夏琰, & 潘俊豪. (2019). 贝叶斯结构方程模型及其研究现状. *心理科学进展*, *27*(11), 1812.</a>

<a name="郑少芳 et al 2020">郑少芳, 唐方成, 葛安茹, & 刘锐剑. 高新技术企业间知识治理对协同创新绩效的影响. *科技进步与对策*, *37*(15), 107-115.</a>

<a name="Bagozzi et al 1991">Bagozzi, R. P., Yi, Y., & Phillips, L. W. (1991). Assessing construct validity in organizational research. *Administrative science quarterly*, 421-458.</a>

<a name="Baron & Kenny 1986">Baron, R. M., & Kenny, D. A. (1986). The moderator–mediator variable distinction in social psychological research: Conceptual, strategic, and statistical considerations. *Journal of personality and social psychology*, *51*(6), 1173.</a>

<a name="Chen et al 2012">Chen, F. F., Hayes, A., Carver, C. S., Laurenceau, J. P., & Zhang, Z. (2012). Modeling general and specific variance in multifaceted constructs: A comparison of the bifactor model to other approaches. *Journal of personality*, *80*(1), 219-251.</a>

<a name="Chin 1998">Chin, W. W. (1998). The partial least squares approach to structural equation modeling. *Modern methods for business research/Lawrence Erlbaum Associates*.</a>

<a name="Fornell & Larcker 1981">Fornell, C., & Larcker, D. F. (1981). Evaluating structural equation models with unobservable variables and measurement error. *Journal of marketing research*, *18*(1), 39-50.</a>

<a name="Henseler et al 2015">Henseler, J., Ringle, C. M., & Sarstedt, M. (2015). A new criterion for assessing discriminant validity in variance-based structural equation modeling. *Journal of the academy of marketing science*, *43*, 115-135.</a>

<a name="Kelley & Pornprasertmanit 2016">Kelley, K., & Pornprasertmanit, S. (2016). Confidence intervals for population reliability coefficients: Evaluation of methods, recommendations, and software for composite measures. *Psychological Methods*,*21*(1),69-92.</a>

<a name="Kenny & Judd 1984">Kenny, D. A., & Judd, C. M. (1984). Estimating the nonlinear and interactive effects of latent variables. *Psychological bulletin*, *96*(1), 201.</a>

<a name="Maslowsky et al 2015">Maslowsky, J., Jager, J., & Hemken, D. (2015). Estimating and interpreting latent variable interactions: A tutorial for applying the latent moderated structural equations method. *International Journal of Behavioral Development*, *39*(1), 87–96. </a>

<a name="McNeish 2018">McNeish, D. (2018). Thanks coefficient alpha, we' ll take it from here. *Psychological Methods*, *23*(3),412-433. </a>

<a name="Muthén & Asparouhov 2012">Muthén, B., & Asparouhov, T. (2012). Bayesian structural equation modeling: A more flexible representation of substantive theory. *Psychological Methods*, *17*(3), 313–335.</a>

<a name="Podsakoff et al 2003">Podsakoff, P. M., MacKenzie, S. B., Lee, J. Y., & Podsakoff, N. P. (2003). Common method biases in behavioral research: a critical review of the literature and recommended remedies. *Journal of applied psychology*, *88*(5), 879.</a>

<a name="Preacher & Hayes 2008">Preacher & Hayes 2008Preacher, K. J., & Hayes, A. F. (2008). Asymptotic and resampling strategies for assessing and comparing indirect effects in multiple mediator models. _Behavior research methods_, _40_(3), 879-891.    </a>

<a name="Sobel 1982">Sobel, M. E. (1982). Asymptotic intervals for indirect effects in structural equations models. In S. Leinhart (Ed.), *Sociological methodology 1982* (pp.290-312). San Francisco: Jossey-Bass.</a>

<a name="Tehseen et al 2017">Tehseen, S., Ramayah, T., & Sajilan, S. (2017). Testing and controlling for common method variance: A review of available methods. *Journal of Management Sciences*, *4*(2), 142–168. </a>

<a name="Williams & McGonagle 2016">Williams, L. J., & McGonagle, A. K. (2016). Four Research Designs and a Comprehensive Analysis Strategy for Investigating Common Method Variance with Self-Report Measures Using Latent Variables. *Journal of Business and Psychology*, *31*(3), 339–359.</a>

<a name="Zhao et al 2010">Zhao, X., Lynch Jr, J. G., & Chen, Q. (2010). Reconsidering Baron and Kenny: Myths and truths about mediation analysis. *Journal of consumer research*, *37*(2), 197-206.</a>





