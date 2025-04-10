# 信号与系统

## 写在前面

- Signal——信号：表达传递==信息==的符号

	目前，一般通过光或电的变化表示信息。

	- 信息：用来消除不确定性的东西	（香农《控制论》中的定义）

	  - 信息量：概率越小，信息量越大。

	  	当`b`为2时，如果`x`发生的概率是`1/2`，则根据信息量`I(x)`计算得1，那么说明表示这个x发生或没发生，则只需要1个bit。一般应用时，`b`取`2`或`e`，取2用于`bit`，取e用于`nat`
	
	  $$
	  I(x)=-\log_b(\mathbb{P}[x])
	  $$

	  - 信息熵：用于度量随机变量的不确定性或者信息的平均度量。
	
	    对连续随机变量，信息熵定义如下
	
	    $$
	    H(X) = -\int_{-\infty}^{\infty} f(x) \log_b(f(x)) dx
	    $$
	    对随机随机变量，信息熵定义如下
	
	    $$
	    \begin{aligned}
	            H(X) &= -\sum_{i=1}^{n} P(X=i) \log_b(P(X=i))\\
	            &=\mathbb{E}[-\log_b(\mathbb{P}[x])]
	    \end{aligned}
	    $$
	


- System——系统：

  有输入有输出。

  系统可以用一个函数或者运算来表示，信号与系统中将输入信号作为自变量，将输出信号作为因变量，函数表示系统输入输出的关系。其定义包括了系统的结构、性质，特性。

<img src="./Learning.assets/image-20230815115311732.png" alt="image-20230815115311732" />

## 信号的分类

### 根据信号维度

-   一维信号（音频信号等）
-   二维信号（图像信号等）
-   三维信号（深度图等）

-   多维信号

### 根据自变量取值

-   连续信号**`x(t)`**

    一定圆括号表示，其中$t\in R$。

-   离散信号**`x[n]`**

    一定方括号表示，其中$n\in Z$。

### 根据周期性

-   周期信号

    信号随时间变量`t`或者`n`的变化，具有重复性

    -   $x(t)=x(t+mT)$           其中$(m\in Z)$ 

        $T$叫最小正周期

    -   $x[n]=x[n+mN]$          其中$(m \in N)$

-   非周期信号

### 根据奇偶性

-   奇信号		(Odd Signal)

    $x(t)=-x(-t)$			or		$x[n]=-x[-n]$

-   偶信号 		(Even Signal)

    $x(t)=x(t) $					or		$x[n]=-x[-n]$

==任何一个信号都可以拆解成奇信号和偶信号==（以连续信号为例）
$$
x_o(t)=\frac{x(t)-x(-t)}{2}\\
x_e(t)=\frac{x(t)+x(-t)}{2}\\
x(t)=x_o(t)+x_e(t)
$$

### 根据单位

假设$x(t)$为电压或者电流，则它在$1\Omega$的电阻上的瞬时功率为$p(t)=|x(t)|^2$，则在$t_1\leq t \leq t_2$内消耗的能量为$E=\int_{t_1}^{t_2}|x(t)|^2dx$

当$T=(t_2-t_1)\rightarrow\infty$时，总能量$E$和平均功率$P$的分别定义为

​					$E=\lim_\limits{T \to \infty}(\int_{t_1}^{t_2}|x(t)|^2dx)$

​					$P=\lim_\limits{T \to \infty}\frac{1}{T}(\int_{t_1}^{t_2}|x(t)|^2dx)$

在$n_1<n<n_2$内的离散时间信号的总能量和平均功率是

​					$E=\sum_\limits{n=n_1}^{n=n2}|x[n]|^2$

​					$P=\frac{1}{n_2-n_1+2}\sum_\limits{n=n_1}^{n=n2}|x[n]|^2$

在无穷大区间上$N=n_2-n_1$

​					$E_\infty=\lim_\limits{N \to \infty}\sum_\limits{n=n_1}^{n=n2}|x[n]|^2$

​					$P_\infty=\lim_\limits{N \to \infty}\frac{1}{2N+1}\sum_\limits{n=n_1}^{n=n2}|x[n]|^2$

-   功率信号（功率有限信号）

    $x(t)$的功率满足：$0\le P \le \infty $ ，而$E=\infty$

    <img src="./Learning.assets/image-20230611154550669.png" alt="image-20230611154550669" style="zoom: 33%;" />

-   能量信号（能量有限信号）

    $x(t)$的满足：$0\le E \le \infty $ ，而$P=0$

    <img src="./Learning.assets/image-20230611154448784.png" alt="image-20230611154448784"  />

## 基本信号

### 单位阶跃信号

连续时间单位阶跃信号写作$u(t)$，在跳变点$t=0$处无定义。$u(0)$可以等于任意值
$$
u(t) = \begin{cases}
0, & \text{if } t < 0 \\
1, & \text{if } t \geq 0
\end{cases}
$$
​		事实上，$t=0$时，$u(t)$可以为任意值

离散时间单位阶跃信号写作$u[n]$
$$
u[n] = \begin{cases}
0, & \text{if } n < 0 \\
1, & \text{if } n \geq 0
\end{cases}
$$

### 冲激信号（奇异函数、冲激函数）

这只是一个理想化的数学模型。

用于表示一种物理现象，发生的时间短，而物理量取值又大
$$
u(t)=\int_{-\infty}^{t} \delta(t) dt\\
\\
\delta(t)=\frac{d u(t)}{d t}
$$
由于$u(t)$在$t=0$处无定义，所以上述式子并不能作为定义式。但是必须满足
$$
\delta(t) = 

\begin{cases}
\infty, & \text{if } t = 0 \\
0, & \text{others}
\end{cases}


\\
\\
\int_{-\infty}^{\infty} \delta(t) dt=1
$$

![image-20230710153310073](./Learning.assets/image-20230710153310073.png)

### 冲击偶函数

$\delta'(t)=\frac{d\delta(t)}{dt}$

$\mathop{lim} \limits_{t\rightarrow 0^+}\delta'(t)>0$

$\mathop{lim} \limits_{t\rightarrow 0^-}\delta'(t)>0$



### 冲激信号的性质

##### 性质一 $\int_{-\infty}^{\infty} \delta(t) dt=1$

证明：
![image-20230706192228236](./Learning.assets/image-20230706192228236.png)

$\int_{a}^{b}f(t)dt=\begin{cases}{1}&{(a<0}&{b>0\text{时})}\\{-1}&{(a>0}&{b<0\text{时})}\\{0}&{\text{其他}}\\ \end{cases}$
证明：相当于正向、反向积分。因为$\triangle$是一个无穷小量，只要任意一个$variable$大于零，它就一定大于$\triangle$



##### 性质二 $\int_{-\infty}^{+\infty}x\left(t\right)\delta\left(t\right)dt=x\left(0\right)$

证明如下：

![image-20230706200235146](./Learning.assets/image-20230706200235146.png)

性质一是性质二的特例
		理解第一条和第二条时，一定要从图像上去理解。$\delta_{\triangle}(t)$永远只是一个理想的模型，不要用微积分的性质去理解。

#####  性质三 $x(t)\delta(t)=x(0)\delta(t)$

勒贝格定理(Lebesgue Theory)：两个函数$f_1(t)$与$f_2(t)$什么时候相等？

-   （中学定义）：若对任意的$\forall t_0\in R$，有$f_1(t)=f_2(t)$，则$f_1(t)=f_2(t)$。
-   若$f_1(t)$与$f_2(t)$只在有限个点上不相等，则$f_1(t)=f_2(t)$
-   （勒贝格定理）若两个函数$f_1(t)$和$f_2(t)$对任意函数$y(t)$
    恒有$\int_{-\infty}^{+\infty}y(t)f_1(t)dt=\int_{-\infty}^{+\infty}y(t)f_2(t)dt$成立。则$f_1(t)=f_2(t)$
    （此处$y(t)$不能取奇异函数）

​		（可以推广至复数域）

特别地，根据勒贝格定理和性质2，可以推导出：

​		如果要证明一个函数$f(t)$是$\delta(t)$，只需要证明对任意函数$y(t)$有

​				$\int_{-\infty}^{+\infty}y(t)f(t)dt=y(0)$

 勒贝格积分

<div align=center>
    <img src="./Learning.assets/image-20230706202805914.png" alt="image-20230706202805914" style="zoom: 67%;" />
</div>

适用于黎曼积分的，毕必然适用于勒贝格积分，反之不然。

​             $\lambda(t)=\begin{cases}1 ~~~~\text{t为有理数}\\ 0 ~~~~\text{t为无理数}\end{cases} $

​            $\int_0^1\lambda(t)dt \stackrel{勒贝格积分}\rightarrow 0$

(根据定义2和勒贝格积分可知，若$f_1(t)$和$f_2(t)$在可数个点上不等而其他点相等，则仍有$f_1(t)=f_2(t)$

证明如下

![image-20230706205428801](./Learning.assets/image-20230706205428801.png)

性质三的变种$x(t)\delta(t-t_0)=x(t_0)\delta(t-t_0)$

##### 性质四 $\delta(at)=\frac{1}{|a|}\delta(t)$

证明：

![image-20230706210951017](./Learning.assets/image-20230706210951017.png)

性质四的变种：

​		$\delta(at+b)=\frac{1}{|a|}\delta(t+\frac{b}{a})$



##### 性质五 $\delta(f(t))=\sum\limits_{\forall f(t_0)=0}\frac{1}{|f^{'}(t_0)|}\delta(t-t_0)$

性质4是性质五的特例

##### 性质六 $\mathop{lim}\limits_{w\rightarrow+\infty}\frac{sin(wt)}{\pi t}=\delta(t)$

![image-20230707144530792](./Learning.assets/image-20230707144530792.png)

$w=10$

<img src="./Learning.assets/image-20230707144718881.png" alt="image-20230707144718881" style="zoom:25%;" />

$w=100$

<img src="./Learning.assets/image-20230707144751060.png" alt="image-20230707144751060" style="zoom:25%;" />

证明：

​		<img src="./Learning.assets/image-20230707153346564.png" alt="image-20230707153346564" style="zoom:50%;" />

<img src="./Learning.assets/image-20230707154920950.png" alt="image-20230707154920950" style="zoom: 80%;" />





##### 课后题：

-   证明 ==若$h_1(t)=h_2(t)$，则$x(t)\ast h_1(t)=x(t)\ast h_2(t)$==

<div>
证明：

![image-20230706211757554](./Learning.assets/image-20230706211757554.png)

关于可数：

​		无限集可以分为 可数无限集（可数集） 和 不可数无限集（不可数集）。
​				Cator在1900年提出：自然数和偶数一样多。（真实性无法证明，只借鉴其思想。

<div align=center>
    <img src="./Learning.assets/image-20230706221057119.png" alt="image-20230706221057119" style="zoom:67%;" />
</div>				

​								
</div>

证明：

![image-20230706211757554](./Learning.assets/image-20230706211757554.png)

关于可数：

​		无限集可以分为 可数无限集（可数集） 和 不可数无限集（不可数集）。
​				Cator在1900年提出：自然数和偶数一样多。（真实性无法证明，只借鉴其思想。

<div align=center>
    <img src="./Learning.assets/image-20230706221057119.png" alt="image-20230706221057119" style="zoom:67%;" />
</div>				

-   求解$\delta(t^2-3t+2)$
    		<img src="./Learning.assets/image-20230707134630818.png" alt="image-20230707134630818" style="zoom:50%;" />								

-   求解$\int_{-2\pi}^{2\pi}(1+t)\delta(cost)dt$


​				<img src="./Learning.assets/image-20230707141100012.png" alt="image-20230707141100012" style="zoom:50%;" />

-   ​	$x(t)=e^{-bt}u(t)$ $h(t)=e^{-at}u(t)$求$x(t)\ast h(t)$
    ​	![image-20230707160832276](./Learning.assets/image-20230707160832276.png)

-   ​	求解
    ![image-20230707162943356](./Learning.assets/image-20230707162943356.png)

​		

​		

### 抽样函数

连续时间抽样函数的定义
$$
S a(t)=\frac{\sin t}{t}\quad \\or\\ \quad\sin c(t)=\frac{\sin\pi t}{\pi t} \\\\\\
\text{其中}
Sa(t)=
\begin{cases}
1 &,     t=0\\
\frac{sin(t)}{t} &, t \ne t
\end{cases}
\\
\text{且}\\
\int_{-\infty}^{\infty}Sa(t) dt=\pi
\\
\\
\int_{0}^{\infty}Sa(t) dt=\int_{-\infty}^{0}Sa(t)dt=\frac{\pi}{2}
$$
![image-20230611165857810](./Learning.assets/image-20230611165857810.png)

证明：


$$
\text{令} \hspace{5cm}\hspace{5cm}
\\
I(a)=\int_{0}^{\infty}\frac{sin(t)}{t}e^{-at}dt\\
\text{对a求导}\hspace{5cm}\hspace{5cm}
\\
\frac{\delta{I(a)}}{\delta{a}}=-\int_{0}^{\infty}sin(t)e^{-at}dt\\
\text{利用欧拉公式} \hspace{5cm}\hspace{5cm}
\\
	\begin{cases}
		sin\theta&=\frac{e^{j\theta}-e^{-j\theta}}{2j}
		\\
		cos\theta&=\frac{e^{j\theta}+e^{-j\theta}}{2}
		\\
		e^{j\theta}&=cos\theta+jsin\theta
	\end{cases}
\\
\text{代入得}\hspace{5cm}\hspace{5cm}
\\
\begin{align}
\\
\frac{\delta{I(a)}}{\delta{a}}&=\frac{1}{2j}\int_{0}^{\infty}e^{-(a+j)t}e^{-(a-j)t}dt\\
&=\frac{1}{2j}[\frac{1}{a+j}-\frac{1}{a-j}]\\
&=-\frac{1}{a^2+1}\\


\\
\text{所以}\hspace{5cm}
\\
I(a)&=-arctan(a)+C\\
\\
\text{当a=}+\infty \hspace{5cm}\\
\\
I(a)&=0\\
\\
I(+\infty)&=-arctan(+\infty)+C\\
\\
C&=\frac{\pi}{2}\\
\\
I(a)&=-arctan(a)+\frac{\pi}{2}\\
\\


I(0)&=\int_{0}^{\infty}\frac{sin(t)}{t}dt\\
&=\frac{\pi}{2}
\end{align}
$$

## 信号的自变量变换

-   变换步骤
    -   化标准形式
    -   前有负号反转
    -   系数大于1压缩，系数小于1拉伸
    -   加左减右

​	得出的结论：
$$
x[n]=\sum_{k=-\infty}^{+\infty}x[k]\delta[n-k]
$$

## 系统的基本性质

### 线性系统 Linear System

1.  若$\forall x(t),a\in R  ~~~~x(t)\stackrel{system}{\rightarrow}y(t)$										  恒有	$ ax(t)\stackrel{system}{\rightarrow}ay(t)$												成立						（齐次性）
2.  若$\forall x_1(t),x_2(t) ~~~x_1(t)\stackrel{system}{\rightarrow}y_1(t)$，$ x_2(t)\stackrel{system}{\rightarrow}y_2(t)$		恒有		$ x_1(t)+x_2(t)\stackrel{system}{\rightarrow}y_1(t)+y_2(t)$     			 成立						（叠加性）

​	==若一个系统同时满足`齐次性`和`叠加性`，则它是线性系统，否则是非线性系统。== 

​	线性系统判据：==每一项都有x，且每一项的x都是一次==

​		例如$y(t)=3x(t)+2$就不是线性系统

### 时不变系统 Time-Invariant System

​	若$\forall x(t)\stackrel{system}{\rightarrow}y(t)$满足$\forall t_0\in R$		恒有		$x(t-t_0)\stackrel{system}{\rightarrow}y(t-t_0)$		成立，则称这个系统为时不变系统，否则为时变系统

​	==系统的输出不会随着时间的改变而改变==

​	时不变系统判据：==t只在x的括号里，t只能是t不能是其它。即t本身只能是一次且系数只能是1==

### 因果系统 Causal System

​	输出$y(t)$不能在输入$x(t)$之前发生

​	==非因果系统难以 实现==

​	因果系统判据：==x括号里的数恒小于y括号里的数==

### 稳定系统 Stable System

$ x(t)\stackrel{system}{\rightarrow}y(t)$中，若$x(t)$是有界的，则$y(t)$有界的，那么这个系统就是稳定系统

-   连续积分器不稳定
    $$
    x(t)\equiv1\\
    y(t)=\int_{\infty}^{t}x(t)dt\equiv \infty
    $$
    
-   连续微分器不稳定
    $$
    x(t)=	
    \begin{cases}
    t-1 ~~~~~ \text{t}\textless 0\\
    t+1 ~~~~~ \text{t}\textgreater 0
    \end{cases}
    \\
    y=\frac{d x(t)}{dt}=not~exists
    $$

-   离散叠加器不稳定

    $x[n]\leq M$有界，不妨设$x[n]\equiv1$
    $$
    x[n]\equiv1\\
    y[n]=\sum_\limits{k=-\infty}^{+\infty}x[k]=\infty
    $$
    
-   离散微分器稳定

    $x[n]\leq M$有界，那么二者的差值也有界
    $$
    \begin{align}
    y[n]&=x[n]-x[n-1]\\
    |y[n]|&\leq | x[n]-x[n-1] |\\
    &\leq B 
    
    \end{align}
    $$
    

### 无记忆系统 Memoryless System

​	一个系统无记忆，则$y(t)$的值仅仅只依赖$x(t)$

​	无记忆系统判据：==x括号和y括号里的数完全一样==

​	无记忆系统一定是因果系统

### 可逆系统 Invertible System

$x(t)$能唯一写成$y(t)$的形式（相当于有反函数）

特别要注意的是，积分器可逆，微分器不可逆。

-   积分器可逆

    由
    $$
    \begin{align}
    y[n]&=\sum_\limits{k=-\infty}^{n}x[k]
    \end{align}
    $$
    可推得
    $$
    x[n]=y[n]-y[n-1]
    $$

-   微分器不可逆

    由
    $$
    y(t)=\frac{dx(t)}{dt}
    $$
    得
    $$
    x(t)=\int_{-\infty}^{t} y(t)dt+C
    $$
    C为任意常数，无法由$y(t)$唯一推得$x(t)$故微分器不可逆。



| 系统            | 线性 | 时不变 | 无记忆 | 因果 | 稳定 |
| :---------------: | :----: | :------: | :------: | :----: | :----: |
| $y(t)=e^{x(t)}$ | F（不满足齐次性） | T | T | T | T |
| $y[n]=x[n]x[n-1]$ | F（不满足齐次性） | T | F | T | T |
| $y(t)=\frac{dx(t)}{dt}$ | T | T | F（存疑） | F（存疑） | F |



## LTI系统时域分析

LTI系统全称：Linear Time-Invariant System（线性时不变系统），如果一个系统既线性又时不变，我们就叫它线性时不变系统（LTI系统）。所有线性都是相对的，都是对现实问题的近似。如果知道LTI系统的一个输入$x(t)$对应的$y(t)$，那么就可以知道这个LTI系统所有的输入$x(t)$对应的$y(t)$。

单位脉冲响应$h[n]$是一个系统对单位脉冲序列$\delta[n]$作为输入的相应，也成为记忆函数

$h[n]$是LTI系统的唯一标识

### LTI卷积

卷积符号$\ast$。全称卷积积分

####  离散LTI系统卷积

$$
x[n]\ast h[h]=\sum\limits_{k=-\infty}^{+\infty}x[k]h[n-k]
$$

<img src="./Learning.assets/image-20230704212817323.png" alt="image-20230704212817323" style="zoom:33%;" />

卷积计算的四步：

​	翻转、平移、相乘、求和

<img src="./Learning.assets/image-20230704213314157.png" alt="image-20230704213314157" style="zoom:50%;" />

#### 连续LTI系统卷积

将连续的信号$x(t)$分解为无数个$\delta(t)$的叠加，并且已知$\delta(t)$经过LTI系统后的输出$h(t)$，那么就可以通过微分的方式，求出$x(t)$经过LTI系统后的输出$y(t)$。

$\delta(t)$为冲激函数，是无限窄的方波。$\delta_{\triangle}(t)$是长度为$\triangle$、高度为$\frac{1}{\triangle}$的方波。

<img src="./Learning.assets/image-20230706191016506.png" alt="image-20230706191016506" style="zoom: 200%;" />

根据定义

​				$\mathop{lim}\limits_{\triangle\rightarrow0}\delta_{\triangle}(t)=\delta(t)$

在$\triangle \rightarrow0$时，

​				$\delta_{\triangle}(t) \rightarrow \infty$

​				$\delta_{\triangle}(t) \stackrel{LTI}{\rightarrow}h_{\triangle}(t)$

则

​				$\delta(t)=\mathop{lim}\limits_{\triangle\rightarrow0}\delta_{\triangle}(t)\stackrel{LTI}{\rightarrow}h(t)=\mathop{lim}\limits_{\triangle\rightarrow0}h_{\triangle}(t)$

假设右侧极限存在

![image-20230706190559697](./Learning.assets/image-20230706190559697.png)

![image-20230707141946636](./Learning.assets/image-20230707141946636.png)

-   宽度一致的方波是三角波
    ![image-20230707165032051](./Learning.assets/image-20230707165032051.png)
    
-   宽度不一致的方波卷积是梯形波
  
    <div align=center>
        <img src="./Learning.assets/image-20230707165042131.png" alt="image-20230707165042131" style="zoom:80%;" />
        <img src="./Learning.assets/image-20230710131944411.png" alt="image-20230710131944411" style="zoom:80%;" />
        <img src="./Learning.assets/image-20230710132045565.png" alt="image-20230710132045565" style="zoom:70%;" />
        <img src="./Learning.assets/image-20230710132249730.png" alt="image-20230710132249730" style="zoom:80%;" />
    </div>

### LTI卷积性质

首先:

​		$x^{(-1)}(t)=x(t)\ast u(t)=\int_{-\infty}^tx(\tau)d\tau$

​		$\nabla x[k]=x[k]-x[k-1]$

​		$\triangle x[k]=x[k+1]-x[k]$

​		$y(t)=x(t)\ast h(t)$



-   交换律
    $x(t)\ast h(t)=h(t)\ast x(t)$

-   结合律
    $[x(t)\ast h_1(t)]\ast h_2(t)=x(t)\ast [h_1(t)\ast h_2(t)]$
    引理：两个LTI系统串联、并联，任然是LTI系统
    引理的证明：
    ![image-20230710145156627](./Learning.assets/image-20230710145156627.png)

    结合律证明
    ![image-20230710145840607](./Learning.assets/image-20230710145840607.png)







-   分配律
    $x(t)\ast[h_1(t)+h_2(t)]=x(t)\ast h_1(t)+x(t)\ast h_2(t)$
    积分（连续）、求和（离散）具有分配律即可得证

-   数乘结合律
    $a[x(t)\ast h(t)]=ax(t)\ast h(t)=x(t)\ast ah(t)$

-   平移特性

    若$y(t)=x(t)\ast h(t)$，则$x(t-t_0)\ast h(t-t_1)=y(t-t_1-t_2)$

-   微分特性（差分特性）
    $y'(t)=x'(t)\ast h(t)=x(t)\ast h'(t)$
    证明：
    ![image-20230711131925564](./Learning.assets/image-20230711131925564.png)
    
-   积分特性
    $y^{(-1)}(t)=x^{(-1)}(t)\ast h(t)=x(t)\ast h^{(-1)}(t)$

-   等效特性
    $y(t)=x^{(-1)}(t)\ast h'(t)=x'(t)\ast h^{(-1)}(t)$

此外

-   $x(t)\ast u(t)=x^{(-1)}(t)$		(积分器)	$x[n]\ast u[n]=\sum\limits_{k=-\infty}^{n}x[n]$	(累加器)

-   $x(t)\ast \delta'(t)=x'(t)$			（微分器）				$x[k]\ast \nabla\delta[k]=\nabla x[k]$		$x[k]\ast \triangle\delta[k]=\triangle x[k]$

-   $\int_{-\infty}^{+\infty}x(t)\delta'(t)dt=-x'(0)$
-   $x(t)\ast h(t)=x(t+t_0)\ast h(t-t_0)$
-   $x(t)\ast \delta(t)=x(t)$                              $x[k]\ast \delta[k]=x[k]$
-   $x(t)\ast \delta(t-t_0)=x(t-t_0)$              $x[k]\ast \delta[k-n]=x[k-n]$





### LTI系统稳定性

LTI系统稳定的充要条件是

​				$\int_{-\infty}^{+\infty}|h(t)|\lt +\infty$		（有界）

或

​				$\sum\limits_{k=-\infty}^{+\infty}|h[n]|<+\infty$		（有界）

<img src="./Learning.assets/image-20230711135104189.png" alt="image-20230711135104189" style="zoom:33%;" />

### LTI因果性

LTI系统的因果的充要条件是：

​		当$t<0$时，$h(t)=0$



## 连续信号与系统频域分析

背景：

​		![image-20230711144603035](./Learning.assets/image-20230711144603035.png)

​		当$t>0$时，求$f(x,t)$ 

### 傅里叶级数

<img src="./Learning.assets/image-20230711145937851.png" alt="image-20230711145937851" style="zoom: 200%;" />		

![image-20230711151414621](./Learning.assets/image-20230711151414621.png)

<img src="./Learning.assets/image-20230711154455467.png" alt="image-20230711154455467" style="zoom:50%;" />

<img src="./Learning.assets/image-20230712094711681.png" alt="image-20230712094711681" style="zoom:50%;" />

<img src="./Learning.assets/image-20230712100029096.png" alt="image-20230712100029096" style="zoom:50%;" />

其在复数表达下的形式为：
$$
\begin{cases}
x(t)=\sum\limits_{k=-\infty}^{+\infty}a_ke^{jkw_0t}\\
a_k=\frac{1}{T_0}\int_{0}^{T_0}x(t)e^{-jkw_0t}dt
\end{cases}
$$


其中
$$
\begin{cases}
B_0=a_0~~~~~~~k=0\\
B_k=a_{-k}+a_{k}~~~~~~k\ne0 \\
C_k=j(a_k-a_{-k})
\end{cases}
$$
可推得：（推导用欧拉公式$e^{j\theta}=cos\theta +jsin\theta$）
$$
\begin{cases}
a_0=B_0\\
a_k=\frac{1}{2}(B_k-jC_k)\\
a_{-k}=\frac{1}{2}(B_k+jC_k)
\end{cases}
$$

#### 狄利赫里收敛条件证明

-   $x(t)$一个周期内绝对可积
    $\int_0^{T_0}|x(t)|dt<+\infty$
-   $x(t)$一个周期最值个数有限
-   $x(t)$一个周期内有有限个不连续点

$x(t)$满足上述三个条件时，可以写成$x(t)=\sum\limits_{k=-\infty}^{+\infty}a_ke^{jkw_0t}$的形式

<img src="./Learning.assets/af5b865ba4876b87368d3e496e01036.jpg" alt="af5b865ba4876b87368d3e496e01036" style="zoom: 33%;" />



### 信号的正交分解

#### 内积运算(Inner Product)和正交函数族

  <img src="./Learning.assets/image-20230713120108688.png" alt="image-20230713120108688" style="zoom: 200%;" />

若函数族$\{e_i(t)\}_{i\in[1,+\infty)}$满足：$\forall k有<e_k,e_k>~>0$  且  $\forall k_1\ne k_2有 <e_{k_1},e_{k_2}>=0$，则称$\{e_i(t)\}_{i\in[1,+\infty)}$是正交函数族。

#### 信号分解

![image-20230713121549185](./Learning.assets/image-20230713121549185.png)

#### 标准正交基函数(Orthonoral Basis Function)

若函数族$\{e_i(t)\}_{i\in[1,+\infty)}$满足

1.  $\forall k,<e_k,e_k>=1$
2.  $\forall k_1\ne k_2,<e_{k_1},e_{k_2}>$

讲正交基变为标准正交基的过程为标准化

![image-20230713123021748](./Learning.assets/image-20230713123021748.png)

![image-20230713123255055](./Learning.assets/image-20230713123255055.png)

<img src="./Learning.assets/3d39ee3d9729464a770cb7024ddfa02.jpg" alt="3d39ee3d9729464a770cb7024ddfa02" style="zoom:50%;" />

#### 施密特正交化

![image-20230713133445171](./Learning.assets/image-20230713133445171.png)









####其他的正交基

1.  1905年Haar创造Haar小波（wavelet）
    ![image-20230713130745026](./Learning.assets/image-20230713130745026.png)

    

    ![image-20230713134913828](./Learning.assets/image-20230713134913828.png)

    

    ![image-20230713134928003](./Learning.assets/image-20230713134928003.png)

    

    

    

    

2.  勒让德多项式
    $P_n(x)=\frac{1}{2^n n!}\frac{d^n[(x^2-1)^n]}{dx^2}$

    性质：	$\int_{-1}^{1}[P_n(x)]^2dx=\frac{2}{2n+1}$

    ​				$\int_{-1}^{1}P_m(x)P_n(x)dx=0$		($m\ne n $)时
    用勒让德多项式表示$[-1,1]$函数$f(x)=\sum\limits_{k=1}^{=\infty}a_kP_k(x)$

    其中$a_k=\frac{<f(x),P_k(x)>}{<P_k(x),P_k(x)>}$

    

    <img src="./Learning.assets/image-20230713134938544.png" alt="image-20230713134938544" style="zoom:50%;" />

    

    

3.  PCA（Principal Component Analysis）主成分分析 

    ![6feddfd8dbd889470b8070169eeea34](./Learning.assets/6feddfd8dbd889470b8070169eeea34.jpg)

    ![0c0609d1f60156ab1031b7799fefe49](./Learning.assets/0c0609d1f60156ab1031b7799fefe49.jpg)

    ![1aaffc1cc1cd569ec2843709eaef0de](./Learning.assets/1aaffc1cc1cd569ec2843709eaef0de.jpg)

    ![image-20230714130217143](./Learning.assets/image-20230714130217143.png)

    图像领域中，将一个图像经常表示为$<m,n,channels>$三元组，即大小$m\times n \times c$的Tensor。RGB中，$c=3$

    PCA的核心是，从一大堆数据中，自动训练出一组正交基。

    <img src="./Learning.assets/image-20230714131403937.png" alt="image-20230714131403937" style="zoom: 50%;" />

    假设共有N个人脸

    其中$A_0=\frac{1}{N}\sum\limits_{i=1}^{N}X_i$是平均脸。

    并且满足$<A_i,A_j>=\sum\limits_{u=1}^{M}\sum\limits_{v=1}^{N}\sum\limits_{c=1}^{3}A_i(u,v,c)\overline{A_j(u,v,c)}=0$

    则可以把任意一个人脸$X$表示为$X=a_0A_0+a_1A_1+a_2A_2+...$

    其中$a_k=\frac{<X,A_k>}{<A_k,A_k>}$

    

### 傅里叶变换

傅里叶级数针对周期函数。可将非周期函数的周期$T_0$视为无穷大。

将傅里叶级数从周期函数推广到非周期函数：


<img src="./Learning.assets/image-20230714142424410.png" alt="image-20230714142424410" />

<img src="./Learning.assets/image-20230715103943923.png" alt="image-20230715103943923" />







### 典型信号的傅里叶变换

<img src="./Learning.assets/image-20230715113719159.png" alt="image-20230715113719159" />

$t^ne^{-at}u(t)\stackrel{F}{\rightarrow}\frac{n!}{(a+jw)^{n+1}}$

<img src="./Learning.assets/image-20230715114123353.png" alt="image-20230715114123353" style="zoom:200%;" />

<img src="./Learning.assets/image-20230715115310262.png" alt="image-20230715115310262" />

<img src="./Learning.assets/image-20230715132554483.png" alt="image-20230715132554483" />

<img src="./Learning.assets/image-20230715132611479.png" alt="image-20230715132611479" />

<img src="./Learning.assets/image-20230715142022810.png" alt="image-20230715142022810" />

类似于$\int_{-\infty}^{+\infty}\frac{sin(wt)}{?}d?$时：积$t$注意$w$，积$w$注意$t$


<img src="./Learning.assets/image-20230715183019336.png" alt="image-20230715183019336" />

$sinw_0t$和$cosw_0t$的证明用到了时移特性

<img src="./Learning.assets/image-20230802130815116.png" alt="image-20230802130815116" />





### 傅里叶变换的性质

#### 线性性质

若$x_1(t)+x_2(t)\stackrel{F}{\rightarrow}x_1(jw)+x_2(jw)$，则$ax_1(t)+bx_2(t)\stackrel{F}{\rightarrow}ax_1(jw)+bx_2(jw)$

可由积分的性质得证

#### 时移性质

若$x(t)\stackrel{F}{\rightarrow}x(jw)$，则$x(t-t_0)\stackrel{F}{\rightarrow}x(jw)e^{-jwt_0}$

![image-20230715160738780](./Learning.assets/image-20230715160738780.png)

<img src="./Learning.assets/image-20230715175216582.png" alt="image-20230715175216582" style="zoom:50%;" />

#### 频移性质

若$x(t)\stackrel{F}{\rightarrow}x(jw)$，则$x(t)e^{jw_0t}\stackrel{F}{\rightarrow}x(j(w-w_0))$

![image-20230715180350753](./Learning.assets/image-20230715180350753.png)

若$x(t)\stackrel{F}{\rightarrow}x(jw)$，则$x(t)cos(w_0t)\stackrel{F}{\rightarrow}\frac{1}{2}\{x[j(w-w_0)]+x[j(w+w_0)]\}$		且		$x(t)cos(w_0t)\stackrel{F}{\rightarrow}\frac{1}{2j}\{x[j(w-w_0)]-x[j(w+w_0)]\}$

#### 微分特性

##### 时域微分性

若$x(t)\stackrel{F}{\rightarrow}x(jw)$，则$\frac{dx(t)}{dt}\stackrel{F}{\rightarrow}jwx(jw)$

<img src="./Learning.assets/image-20230715185158082.png" alt="image-20230715185158082" style="zoom:50%;" />

##### 频域微分性

若$x(t)\stackrel{F}{\rightarrow}x(jw)$，则$tx(t)\stackrel{F}{\rightarrow}j\frac{dx(jw)}{dw}$

<img src="./Learning.assets/image-20230715190512504.png" alt="image-20230715190512504" style="zoom:50%;" />

#### 时域卷积性质

若$x(t)\stackrel{F}{\rightarrow}x(jw)$,$h(t)\stackrel{F}{\rightarrow}H(jw)$，则$x(t)\ast h(t)\stackrel{F}{\rightarrow}x(jw)H(jw)$

时域卷积的傅里叶变换等于各自频域相乘

<img src="./Learning.assets/image-20230715193343089.png" alt="image-20230715193343089" />

![image-20230715202221552](./Learning.assets/image-20230715202221552.png)

![image-20230715202241308](./Learning.assets/image-20230715202241308.png)

对于一个LTI系统，知道其在任何一个时刻$t_0$的==不为零的输入==与对应的输出，那么可以知道它在任何时刻对应的输入与输出。



#### 积分性质

若$x(t)\stackrel{F}{\rightarrow}x(jw)$,$h(t)\stackrel{F}{\rightarrow}H(jw)$，则$\int_{-\infty}^{t}x(\tau)d\tau\stackrel{F}{\rightarrow}\frac{x(jw)}{jw}+\pi x(j0)\delta(w)$

左侧为$x(t)\ast u(t)$即可得证



#### 调制性质

若$x_1(t)\stackrel{F}{\rightarrow}x_1(jw)$,	$x_2(t)\stackrel{F}{\rightarrow}x_2(jw)$，则$x_1(t)x_2(t)\stackrel{F}{\rightarrow}\frac{1}{2\pi}x_1(jw)\ast x_2(jw)$

<img src="./Learning.assets/image-20230726102523106.png" alt="image-20230726102523106" style="zoom:50%;" />

#### 时域扩展（尺度变换）

若$x(t)\stackrel{F}{\rightarrow}x(jw)$，则$x(at)\stackrel{F}{\rightarrow}\frac{1}{|a|}x(j\frac{w}{a})$

（换元法得证）

时域胖代表频域瘦。时域瘦代表频域胖





#### 对偶性质

若$x(t)\stackrel{F}{\rightarrow}X(jw)$，则$X(t)\stackrel{F}{\rightarrow}2\pi x(-w)$

#### 帕斯瓦尔定理

若$x(t)\stackrel{F}{\rightarrow}x(jw)$，则$\int_{-\infty}^{+\infty}|x(t)|^2dt\stackrel{F}{\rightarrow}\frac{1}{2\pi}\int_{-\infty}^{+\infty}|x(jw)|^2dw$

即傅里叶变换满足能量守恒

<img src="./Learning.assets/image-20230727135251164.png" alt="image-20230727135251164" />

#### 共轭性和共轭对称性

$实偶\stackrel{F}{\rightarrow}实偶$	如果$x(t)$是关于$t$的实偶函数，则$X(jw)$是关于$w$的实偶函数（只有cos分量）

$实奇\stackrel{F}{\rightarrow}虚奇$	如果$x(t)$是关于$t$的实偶函数，则$X(jw)$是关于w的纯虚奇函数（只有sin分量）

<img src="./Learning.assets/image-20230727140515786.png" alt="image-20230727140515786" />

若$x(t)$是实函数，则$x(jw)$实部偶函数、虚部奇函数

<img src="./Learning.assets/image-20230727141510117.png" alt="image-20230727141510117" />

若$x(t)$是实函数，设$x(jw)=|x(jw)|e^{j\theta(w)}$中，幅度谱$|x(jw)|$为偶函数，相位谱$\theta(w)$为奇函数

<img src="./Learning.assets/image-20230801230054355.png" alt="image-20230801230054355" />





### 系统函数$H(jw)$

![image-20230715204423059](./Learning.assets/image-20230715204423059.png)

### 调制与解调

调制（Modulation），解调（De-Modulation）。

通信系统传输某个信号$x(t)$时

1.  调制：发送端进行调制$y(t)=x(t)cos(w_ct)$，其中$w_c$为载波（Carrier Wave）。

    <img src="./Learning.assets/image-20230726104240924.png" alt="image-20230726104240924" />

    <img src="./Learning.assets/image-20230726104258515.png" alt="image-20230726104258515" />

2.  解调：接收端进行解调$w(t)=y(t)cos(w_c t)=x(t)cos^2(w_ct)$

    则$W(jw)=\frac{1}{2\pi}Y(jw)\ast F(cos(w_ct))$

    <img src="./Learning.assets/image-20230726110507228.png" alt="image-20230726110507228" style="zoom:67%;" />

    得到$W(jw)$后，将$W(jw)$经过一个低通滤波器，再进行$F^{-1}$，即可得到$x(t)$。

    (并且低通滤波器的高度应该为2，且低通滤波器的截止频率应该满足$w_0\lt w_p \lt 2w_c-w_0 $）

    <img src="./Learning.assets/image-20230726111212874.png" alt="image-20230726111212874" style="zoom:150%;" />
    
    <img src="./Learning.assets/image-20230726111745750.png" alt="image-20230726111745750" style="zoom:67%;" />

假设在同一个信道中传输两个信号$x_1(t)$和$x_2(t)$

<img src="./Learning.assets/image-20230727095304990.png" alt="image-20230727095304990" />



### 理想低通滤波器

理想低通滤波器有一定的缺点

-   非因果（无法实现实时系统）
    <img src="./Learning.assets/image-20230801232830520.png" alt="image-20230801232830520" />
    
-   年轮效应
    理想低通滤波器会把陡峭上升沿信号转换成逐渐衰减的年轮传递至无穷远
    <img src="./Learning.assets/image-20230801234319460.png" alt="image-20230801234319460" />

-   阶跃响应
    <img src="./Learning.assets/image-20230801235021342.png" alt="image-20230801235021342" style="zoom:200%;" />

    <img src="./Learning.assets/image-20230801235037761.png" alt="image-20230801235037761" />

    



### Butterworth滤波器

<img src="./Learning.assets/image-20230802123613668.png" alt="image-20230802123613668" />



### 二维信号的傅里叶变换和反变换

<img src="./Learning.assets/image-20230802125139095.png" alt="image-20230802125139095" />



### 通过傅里叶变换计算傅里叶级数

![image-20230802133756641](./Learning.assets/image-20230802133756641.png)

### 连续时间周期信号的傅里叶变换

<img src="./Learning.assets/image-20230802134135212.png" alt="image-20230802134135212" style="zoom:150%;" />











## 离散信号与系统频域分析

### 离散傅里叶变换

<img src="./Learning.assets/image-20230814232139683.png" alt="image-20230814232139683" />

$x(e^{jw})$是$w$以$2\pi$为周期的函数

证明如下：

<img src="./Learning.assets/image-20230802135251488.png" alt="image-20230802135251488" />
	

### 典型信号的傅里叶变换

![image-20230813225113813](./Learning.assets/image-20230813225113813.png)

<img src="./Learning.assets/image-20230813225122824.png" alt="image-20230813225122824" />

<img src="./Learning.assets/image-20230813230747666.png" alt="image-20230813230747666" />

<img src="./Learning.assets/image-20230813232514579.png" alt="image-20230813232514579" />

<img src="./Learning.assets/image-20230813235351303.png" alt="image-20230813235351303" />

<img src="./Learning.assets/image-20230814002234768.png" alt="image-20230814002234768" />

<img src="./Learning.assets/image-20230814002937606.png" alt="image-20230814002937606" />

### 离散傅里叶变换的性质

#### 线性性质

<img src="./Learning.assets/image-20230814222928273.png" alt="image-20230814222928273" />

#### 时移性质

<img src="./Learning.assets/image-20230814223143909.png" alt="image-20230814223143909" />

#### 频移性质

<img src="./Learning.assets/image-20230814223400293.png" alt="image-20230814223400293" />

#### 时域差分

<img src="./Learning.assets/image-20230814224028653.png" alt="image-20230814224028653" />

#### 频域差分

<img src="./Learning.assets/image-20230814225234884.png" alt="image-20230814225234884" />

#### 时域卷积性质

<img src="./Learning.assets/image-20230814225420116.png" alt="image-20230814225420116" />

#### 时域累加性质

<img src="./Learning.assets/image-20230814230630059.png" alt="image-20230814230630059" />









#### 时域扩展

<img src="./Learning.assets/image-20230814224750460.png" alt="image-20230814224750460" />

<img src="./Learning.assets/image-20230814224407444.png" alt="image-20230814224407444" />

相当于在两个相邻下标之间插入$k-1$个$0$

#### 调制性质

<img src="./Learning.assets/image-20230814232658012.png" alt="image-20230814232658012" />

#### 帕斯瓦尔定理

<img src="./Learning.assets/image-20230814235415999.png" alt="image-20230814235415999" />

#### 共轭性和共轭对称性

<img src="./Learning.assets/image-20230815000337951.png" alt="image-20230815000337951" />

### 离散傅里叶级数

<img src="./Learning.assets/image-20230815122944984.png" alt="image-20230815122944984" />

<img src="./Learning.assets/image-20230815123013247.png" alt="image-20230815123013247" />

<img src="./Learning.assets/image-20230815123029248.png" alt="image-20230815123029248" />

用$x(e^{jw})$在$w_0,w_1,...,w_{N-1}$的N点频谱值，用逆矩阵反解$x[n]$，其计算复杂度约为$O(N^3)$，目前约为$O(N^{2.812})$。

但是如果选一组特殊的$w_0,w_1,...,w_{N-1}$，其计算复杂度可降为$O(N^2)$。由库利和图基提出离散傅里叶级数，即在$w \in [0,2\pi)$上选取一组特殊的$w_0,w_1,...,w_{N-1}$（均匀采样）.

其中，$w_0=0,w_1=\frac{2\pi}{N},w_2=2\frac{2\pi}{N},w_3=3\frac{2\pi}{N},...,w_{N-1}=(N-1)\frac{2\pi}{N}$

<img src="./Learning.assets/image-20230815130604129.png" alt="image-20230815130604129" />

由上图可知，其复杂度由两个$\sum$中的求和与累加决定，大致为$O(N^2)$。而除此之外，库利和图基进一步证明，上述算法的时间复杂度可以简化为$O(NlogN)$

二人快速傅里叶变换（Fast Fourier Transform）的算法：

<img src="./Learning.assets/image-20230815131522517.png" alt="image-20230815131522517" />

<img src="./Learning.assets/image-20230815132517849.png" alt="image-20230815132517849" />

<img src="./Learning.assets/image-20230815132932799.png" alt="image-20230815132932799" />

![image-20230816115022786](./Learning.assets/image-20230816115022786.png)

再实现4点FFT

<img src="./Learning.assets/image-20230816120525038.png" alt="image-20230816120525038" />

<img src="./Learning.assets/image-20230816120609424.png" alt="image-20230816120609424" />

如果$N$是若干个素数的积，例如$N=12$可以分解成$N=2*2*3$，即可以用2点FFT和3点FFT实现12点FFT。

<img src="./Learning.assets/image-20230816121529387.png" alt="image-20230816121529387" />

<img src="./Learning.assets/image-20230816121542497.png" alt="image-20230816121542497" />

那么当N是质数时，可以通过插值的方法进行计算，方法如下：

​		<img src="./Learning.assets/image-20230816124236341.png" alt="image-20230816124236341" />

### 用FFT计算两个序列的卷积

<img src="./Learning.assets/image-20230816132038118.png" alt="image-20230816132038118" />

## 采样与调制

### 采样定理Sampling Theorem

设$x(t)$是某一带限信号，即当$|w|>w_M$时，有$X(e^{jw})=0$。如果采样频率，其中$w_s=\frac{2\pi}{T}$，$T$为采样周期。那么$x(t)$就唯一地由其样本值序列$x[n]=X(nT)$所确定（$n = ...,-2,-1,0,1,2,...$）,$w_M$是带限信号的截止频率。$2w_M$的称为奈奎斯特采样频率，$w_M$称为奈奎斯特频率。

要完全恢复，只能是$w_s>2w_M$,不能取等。

<img src="./Learning.assets/image-20230816135138655.png" alt="image-20230816135138655" />

<img src="./Learning.assets/image-20230816141807627.png" alt="image-20230816141807627" />

<img src="./Learning.assets/image-20230816143808406.png" alt="image-20230816143808406" />

再根据尺度变换，便可以画出图3。

### 带限内插公式

根据$X_p(jw)$恢复$X(jw)$：即将$X_p(jw)$通过一个低通滤波器。

<img src="./Learning.assets/image-20230816145311656.png" alt="image-20230816145311656" />

<img src="./Learning.assets/image-20230913212433361.png" alt="image-20230913212433361" />

<img src="./Learning.assets/image-20230913225139716.png" alt="image-20230913225139716" />

### 滤波器种类

#### 低通滤波器

<img src="./Learning.assets/image-20230913225341824.png" alt="image-20230913225341824" />

#### 高通滤波器

<img src="./Learning.assets/image-20230913225349662.png" alt="image-20230913225349662" />

#### 带通滤波器

<img src="./Learning.assets/image-20230913225400485.png" alt="image-20230913225400485" />

#### 带阻滤波器滤波器

<img src="./Learning.assets/image-20230913225418322.png" alt="image-20230913225418322" />

### 零阶保持和一阶保持

#### 零阶保持采样

<img src="./Learning.assets/image-20230913230019340.png" alt="image-20230913230019340" />

<img src="./Learning.assets/image-20230913230050626.png" alt="image-20230913230050626" />

#### 一阶保持采样

相邻点线段相连

![image-20230913230804766](./Learning.assets/image-20230913230804766.png)

## 希尔伯特变换

因果信号$x(t)$的傅里叶变换中，实部和虚部满足希尔伯特变换。
		$R(w)=H[I(w)]=\frac{1}{\pi}\int_{-\infty}^{+\infty}\frac{I(\lambda)}{w-\lambda}d\lambda$
		$I(w)=-H[R(w)]=-\frac{1}{\pi}\int_{-\infty}^{+\infty}\frac{R(w)}{w-\lambda}d\lambda$

<img src="./Learning.assets/image-20230916133527558.png" alt="image-20230916133527558" />













## 练习题

1.  第一题

    ![image-20230615114550030](./Learning.assets/image-20230615114550030.png)

2.  第二题

    <img src="./Learning.assets/image-20230615114558313.png" alt="image-20230615114558313" style="zoom: 80%;" />

    <img src="./Learning.assets/image-20230615122018978.png" alt="image-20230615122018978" style="zoom:50%;" />

3.  第三题

  ​							已知$x[n]=\delta[n+1]+2\delta[n]+\delta[n-1]+\delta[n-2]$

  ​							$h[n]=\delta[n]-\delta[n-1]-\delta[n-4]+\delta[n-5]$

  ​							求$y[n]=x[n] \ast h[n]$

  <img src="./Learning.assets/image-20230615124024146.png" alt="image-20230615124024146" style="zoom:50%;" />

4.  第四题

    假设$x[n]$长度为$N_1$，$h[n]$长度为 $N_2$，求$y[n]=x[n] \ast h[n]$的长度

    <img src="./Learning.assets/image-20230615125703397.png" alt="image-20230615125703397" style="zoom:50%;" />

5.  求差分器频率响应$h(e^{jw})$
    <img src="./Learning.assets/image-20230814231159895.png" alt="image-20230814231159895" />

6.  求累加器频率响应
    <img src="./Learning.assets/image-20230814231241612.png" alt="image-20230814231241612" />

7.  

8.  

9.  

10.  

11.  

12.  

13.  

14.  

15.  

16.  

17.  

18.  

19.  

20.  

21.  

22.  

23.  

# 通信原理

## 前置知识学习

### 复信号

<img src="./Learning.assets/image-20231031184243667.png" alt="image-20231031184243667" />

特别要注意两个复单频信号叠加时功率的计算

![image-20231031184341943](./Learning.assets/image-20231031184341943.png)

![image-20231031184400755](./Learning.assets/image-20231031184400755.png)

### 内积

定义任意信号（包括复信号）内积$<x(t),y(t)>=\int_{-\infty}^{+\infty}x(t)y^{*}(t)dt$

![image-20231031190013973](./Learning.assets/image-20231031190013973.png)

### 许瓦兹不等式

![image-20231031190107343](./Learning.assets/image-20231031190107343.png)

![image-20231031190622669](./Learning.assets/image-20231031190622669.png)



### 归一化相关系数

![image-20231031190703230](./Learning.assets/image-20231031190703230.png)

![image-20231031190902800](./Learning.assets/image-20231031190902800.png)

### 能量信号的相关函数

![image-20231031191352782](./Learning.assets/image-20231031191352782.png)

![image-20231031191457435](./Learning.assets/image-20231031191457435.png)

![image-20231031191806213](./Learning.assets/image-20231031191806213.png)

![image-20231031191931362](./Learning.assets/image-20231031191931362.png)

![image-20231031192007784](./Learning.assets/image-20231031192007784.png)

![image-20231031192057080](./Learning.assets/image-20231031192057080.png)



自相关函数在$\tau=0$时取得最大$E_x$

### 能量谱密度



![image-20231031192244331](./Learning.assets/image-20231031192244331.png)

![image-20231031192301568](./Learning.assets/image-20231031192301568.png)

![image-20231031192348622](./Learning.assets/image-20231031192348622.png)

![image-20231031192433403](./Learning.assets/image-20231031192433403.png)

### 功率信号的互相关函数

![image-20231031192718272](./Learning.assets/image-20231031192718272.png)

![image-20231031192748332](./Learning.assets/image-20231031192748332.png)

将互相关函数从能量信号推广到功率信号（取时间平均）

![image-20231031193029579](./Learning.assets/image-20231031193029579.png)

性质如下

![image-20231031193128320](./Learning.assets/image-20231031193128320.png)

![image-20231031193216240](./Learning.assets/image-20231031193216240.png)

![image-20231031193316300](./Learning.assets/image-20231031193316300.png)

![image-20231031193422634](./Learning.assets/image-20231031193422634.png)

### 功率谱密度

![image-20231031193601003](./Learning.assets/image-20231031193601003.png)

![image-20231031193646639](./Learning.assets/image-20231031193646639.png)

![image-20231031193734218](./Learning.assets/image-20231031193734218.png)

![image-20231031193822311](./Learning.assets/image-20231031193822311.png)

### 带宽

![image-20231031194056968](./Learning.assets/image-20231031194056968.png)

基带信号：信号的功率或能量主要集中在零频附近

带通信号（频带信号）：信号的功率或能量集中在某个载频附近

![image-20231031194400300](./Learning.assets/image-20231031194400300.png)

带宽是指：单边谱密度的宽度

带宽有很多种定义，主要有：绝对带宽、主瓣带宽、3dB带宽、等效矩形带宽、按能量占比定义的带宽

- 绝对带宽
  频谱在某个区间之外为0，在该区间的宽度是绝对带宽
  ![image-20231031194700783](./Learning.assets/image-20231031194700783.png)

  绝对带宽只是一个理想的模型（如果一个信号频带有限，则在时域上是无限的，现实中不可能存在）

  

- 主瓣带宽
  有些信号频谱呈现主瓣、旁瓣的特征，其带宽可以采用主瓣宽度进行衡量
  ![image-20231031195003798](./Learning.assets/image-20231031195003798.png)

- 3dB带宽
  频谱密度从峰值下降一半（3dB）的宽度
  ![image-20231031195131424](./Learning.assets/image-20231031195131424.png)

- 等效矩形带宽
  功率谱密度同高同面积的矩形的宽度
  ![image-20231031195317654](./Learning.assets/image-20231031195317654.png)
  
- 能量占比带宽
  ![image-20231101150624615](./Learning.assets/image-20231101150624615.png)

此外，对信号平方后，带宽也会发生改变

![image-20231101152122108](./Learning.assets/image-20231101152122108.png)

$x(t)$的带宽为W，则$x^2(t)$的带宽为2W



正弦调制后的带宽也会发生改变

$s(t)=x(t)cos(2\pi f_ct)$其中$f_c>W$，则调制后的绝对带宽是2W

![image-20231101152514222](./Learning.assets/image-20231101152514222.png)

![image-20231101152525666](./Learning.assets/image-20231101152525666.png)

### LTI系统

![image-20231101152710982](./Learning.assets/image-20231101152710982.png)



### 希尔伯特变换

![image-20231101153242813](./Learning.assets/image-20231101153242813.png)

![image-20231101153307415](./Learning.assets/image-20231101153307415.png)

![image-20231101153353618](./Learning.assets/image-20231101153353618.png)

![image-20231101153724372](./Learning.assets/image-20231101153724372.png)

![image-20231101153803150](./Learning.assets/image-20231101153803150.png)

![image-20231101154208269](./Learning.assets/image-20231101154208269.png)

### 带通信号三种表示方法

![image-20231101161719072](./Learning.assets/image-20231101161719072.png)

![image-20231101161917828](./Learning.assets/image-20231101161917828.png)





## 信道

能够传输光、电、无线电、声波的各种物理媒介介质，是以传输媒质为基础的信号通道。

<img src="./Learning.assets/image-20231030113649990.png" alt="image-20231030113649990" />

<img src="./Learning.assets/image-20231030113803332.png" alt="image-20231030113803332" />

### 有线信道

<img src="./Learning.assets/image-20231030114144787.png" alt="image-20231030114144787" />

### 无线信道

<img src="./Learning.assets/image-20231030114220384.png" alt="image-20231030114220384" />

电磁波的定义：电磁场的一种运动形态。

电磁波特性：低频电磁波可以在有形的导电体内传递；高频的电磁波可以在空间、导电体内传递。

<img src="./Learning.assets/image-20231030114508800.png" alt="image-20231030114508800" />

<img src="./Learning.assets/image-20231030114625362.png" alt="image-20231030114625362" />

### 调制信道

![image-20231102143259198](./Learning.assets/image-20231102143259198.png)

![image-20231102143456868](./Learning.assets/image-20231102143456868.png)

![image-20231102143546606](./Learning.assets/image-20231102143546606.png)

### 编码信道

![image-20231102143930082](./Learning.assets/image-20231102143930082.png)

![image-20231102144000851](./Learning.assets/image-20231102144000851.png)



### 恒参信道

![image-20231102144231055](./Learning.assets/image-20231102144231055.png)

![image-20231102144400878](./Learning.assets/image-20231102144400878.png)

![image-20231102144537068](./Learning.assets/image-20231102144537068.png)

![image-20231102144644810](./Learning.assets/image-20231102144644810.png)

### 随参信道

![image-20231102145440210](./Learning.assets/image-20231102145440210.png)

![image-20231102145614271](./Learning.assets/image-20231102145614271.png)

 ![image-20231102150010682](./Learning.assets/image-20231102150010682.png)

![image-20231102150135034](./Learning.assets/image-20231102150135034.png)

![image-20231102150437944](./Learning.assets/image-20231102150437944.png)

![image-20231102150525340](./Learning.assets/image-20231102150525340.png)

![image-20231102150626956](./Learning.assets/image-20231102150626956.png)



### 信道容量

![image-20231102151126045](./Learning.assets/image-20231102151126045.png)

![image-20231102151223315](./Learning.assets/image-20231102151223315.png)

![image-20231102151319458](./Learning.assets/image-20231102151319458.png)

![image-20231102151400797](./Learning.assets/image-20231102151400797.png)

![image-20231102151502895](./Learning.assets/image-20231102151502895.png)

![image-20231102151728506](./Learning.assets/image-20231102151728506.png)







## 噪声

![image-20231102150812375](./Learning.assets/image-20231102150812375.png)

![image-20231102150925203](./Learning.assets/image-20231102150925203.png)















## 调制

### 幅度调制

#### AM调制

本质是用消息信号控制正弦载波的幅度

![image-20231101164513221](./Learning.assets/image-20231101164513221.png)

在时域观察其波形、调制/解调的方法，在频域观察已调信号的频谱、带宽

![image-20231101164905296](./Learning.assets/image-20231101164905296.png)

载波调制后的频谱由载波分量、USB、LSB组成，带宽等于基带信号的二倍。

![image-20231101165552516](./Learning.assets/image-20231101165552516.png)

幅度调制又称为线性调制，波形的包络正比于$m(t)$

因为波形的包络正比于$m(t)$，可以采用简单的包络检波

![image-20231101165845527](./Learning.assets/image-20231101165845527.png)

![image-20231101165935806](./Learning.assets/image-20231101165935806.png)

<img src="./Learning.assets/image-20231109102923648.png" alt="image-20231109102923648" />

AM虽然调制解调简单，但是载波分量不含有用信息，所以会占用大量发射功率

#### DSB调制

<img src="./Learning.assets/image-20231109103020385.png" alt="image-20231109103020385" />

<img src="./Learning.assets/image-20231109103046247.png" alt="image-20231109103046247" />

<img src="./Learning.assets/image-20231109103120621.png" alt="image-20231109103120621" />

#### SSB

SSB ,Single Side Band 单边带调制

<img src="./Learning.assets/image-20231109103332458.png" alt="image-20231109103332458" />

<img src="./Learning.assets/image-20231109103417454.png" alt="image-20231109103417454" />

#### VSB

Vestigial Side Band 残留边带调制。旨在解决双边带中难以实现的陡峭滤波特性。

<img src="./Learning.assets/image-20231109103536693.png" alt="image-20231109103536693" />

<img src="./Learning.assets/image-20231109103628867-1699497390337-1.png" alt="image-20231109103628867" />

<img src="./Learning.assets/image-20231109103711282.png" alt="image-20231109103711282" />

![image-20231109103733780](./Learning.assets/image-20231109103733780.png)

<img src="./Learning.assets/image-20231109104013025.png" alt="image-20231109104013025" />





### 角度调制

<img src="./Learning.assets/image-20231109104140716.png" alt="image-20231109104140716" />

角度调制是 FM和PM的统称

<img src="./Learning.assets/15c98d09b829ebc961081267b5bf0de.jpg" alt="15c98d09b829ebc961081267b5bf0de" />

由于频率和相位是积分、微分关系，所以调频和调相可以相互转化

<img src="./Learning.assets/image-20231109112227947.png" alt="image-20231109112227947" />

在预先不知道消息信号$m(t)$变化规律的情况下，无法判断已调信号是PM还是FM。

## 模拟调制系统抗噪声性能



<img src="./Learning.assets/image-20231110125428859.png" alt="image-20231110125428859" />

<img src="./Learning.assets/image-20231110125550624.png" alt="image-20231110125550624" />

<img src="./Learning.assets/image-20231110125706284.png" alt="image-20231110125706284" />

<img src="./Learning.assets/image-20231110125736830.png" alt="image-20231110125736830" />

![image-20231110125845983](./Learning.assets/image-20231110125845983.png)

<img src="./Learning.assets/image-20231110125931916.png" alt="image-20231110125931916" />

<img src="./Learning.assets/image-20231110130004265.png" alt="image-20231110130004265" />

<img src="./Learning.assets/image-20231110130027476.png" alt="image-20231110130027476" />

<img src="./Learning.assets/image-20231110130057250.png" alt="image-20231110130057250" />

<img src="./Learning.assets/image-20231110130140750.png" alt="image-20231110130140750" />

![image-20231110130222447](./Learning.assets/image-20231110130222447.png)

<img src="./Learning.assets/image-20231110130447516.png" alt="image-20231110130447516" />

<img src="./Learning.assets/image-20231110130559908.png" alt="image-20231110130559908" />

## 数字基带传输系统

### 数字基带

数字指：状态可数、取值离散

基带指：零频附近、未经载波调制

#### 系统组成

<img src="./Learning.assets/image-20231110132114198.png" alt="image-20231110132114198" />

发送滤波器的作用是将终端传送的信号转换成适合在信道中传输的信号。主要包含码型变换和波形变换。所以“发送滤波器”也称“信道信号形成器”、“基带调制器”。

<img src="./Learning.assets/image-20231110132327754.png" alt="image-20231110132327754" />

接受滤波器的作用是滤除带外噪声、对信道特性均衡。

抽样判决器主要对接受滤波器输出的波形用未定时序列做抽样，并将抽样值与门限做比较，大于门限值则判为1码，否则判为0码，再生出相应的数字信号。错误码元主要来源于信道噪声和码间串扰ISI。

<img src="./Learning.assets/image-20231110132626318.png" alt="image-20231110132626318" />

### 数字基带信号

<img src="./Learning.assets/image-20231110132846042.png" alt="image-20231110132846042" />

<img src="./Learning.assets/image-20231110132936049.png" alt="image-20231110132936049" />   

<img src="./Learning.assets/image-20231110133110627.png" alt="image-20231110133110627" />

<img src="./Learning.assets/image-20231110133242723.png" alt="image-20231110133242723" />

因为信息码元序列中，0和1的出现都是随机的，难以以确定的方程描述，所以其是一个功率信号。

<img src="./Learning.assets/image-20231110133626211.png" alt="image-20231110133626211" />

<img src="./Learning.assets/image-20231110164912355.png" alt="image-20231110164912355" />

<img src="./Learning.assets/image-20231110165050088.png" alt="image-20231110165050088" />

### 设计和选码原则

<img src="./Learning.assets/image-20231110165553624.png" alt="image-20231110165553624" />



### 码间串扰

![image-20231110165715344](./Learning.assets/image-20231110165715344.png)

<img src="./Learning.assets/image-20231110165744961.png" alt="image-20231110165744961" />

<img src="./Learning.assets/image-20231110165929610.png" alt="image-20231110165929610" />

### 消除码间串扰

<img src="./Learning.assets/image-20231110170046534.png" alt="image-20231110170046534" />

前者的思路是：让前面时刻码元的波形在后面码元的抽样时刻到来前，衰减为0，现实中难以实现。

后者的思路是：关注抽样时刻，让前面时刻码元的波形在后面时刻码元的抽样时刻恰好为零。

<img src="./Learning.assets/image-20231110170233728.png" alt="image-20231110170233728" />

<img src="./Learning.assets/image-20231110170323533.png" alt="image-20231110170323533" />

<img src="./Learning.assets/image-20231110170554623.png" alt="image-20231110170554623" />

<img src="./Learning.assets/image-20231110170638353.png" alt="image-20231110170638353" />

<img src="./Learning.assets/image-20231110170734292.png" alt="image-20231110170734292" />

<img src="./Learning.assets/image-20231110170814799.png" alt="image-20231110170814799" />

<img src="./Learning.assets/image-20231110170840056.png" alt="image-20231110170840056" />

### 基带系统抗噪声性能

<img src="./Learning.assets/image-20231110172821756.png" alt="image-20231110172821756" />

<img src="./Learning.assets/image-20231110174744971.png" alt="image-20231110174744971" />

<img src="./Learning.assets/image-20231110174757325.png" alt="image-20231110174757325" />

<img src="./Learning.assets/image-20231110174944885.png" alt="image-20231110174944885" />

<img src="./Learning.assets/image-20231110175024408.png" alt="image-20231110175024408" />

<img src="./Learning.assets/image-20231110175049828.png" alt="image-20231110175049828" />

<img src="./Learning.assets/image-20231110175105134.png" alt="image-20231110175105134" />

<img src="./Learning.assets/image-20231110175237309.png" alt="image-20231110175237309" />

<img src="./Learning.assets/image-20231110175324887.png" alt="image-20231110175324887" />

<img src="./Learning.assets/image-20231110175422979.png" alt="image-20231110175422979" />

### 眼图

<img src="./Learning.assets/image-20231110175521017.png" alt="image-20231110175521017" />

$T_B$是码长，$T_C$为示波器水平扫描周期

<img src="./Learning.assets/image-20231110175606705.png" alt="image-20231110175606705" />

<img src="./Learning.assets/image-20231110175648596.png" alt="image-20231110175648596" />

<img src="./Learning.assets/image-20231110175707736.png" alt="image-20231110175707736" />

眼图可以反映ISI的大小和$n(t)$的强弱，从而估计系统性能的优劣，还可以指示接受滤波器的调整以减小ISI

<img src="./Learning.assets/image-20231110175915658.png" alt="image-20231110175915658" />

### 均衡技术

<img src="./Learning.assets/image-20231110180129094.png" alt="image-20231110180129094" />

<img src="./Learning.assets/image-20231110180234954.png" alt="image-20231110180234954" />

<img src="./Learning.assets/image-20231110180403309.png" alt="image-20231110180403309" />

<img src="./Learning.assets/image-20231110180445557.png" alt="image-20231110180445557" />



### 部分响应

<img src="./Learning.assets/image-20231110180558292.png" alt="image-20231110180558292" />

<img src="./Learning.assets/image-20231110180815990.png" alt="image-20231110180815990" />

<img src="./Learning.assets/image-20231110180859544.png" alt="image-20231110180859544" />

<img src="./Learning.assets/image-20231110181129556.png" alt="image-20231110181129556" />

## 数字带通传输系统

<img src="./Learning.assets/image-20231110181426563.png" alt="image-20231110181426563" />

<img src="./Learning.assets/image-20231110181506807.png" alt="image-20231110181506807" />

![image-20231110181623242](./Learning.assets/image-20231110181623242.png)





























# 音频信号

## 格式

格式众多，一般用WAV格式，如果将WAV的文件头部分去掉，只保留数据部分，则是PCM格式。WAV格式采用16b均匀量化编码，即2B表示一个采样点，取值范围为$[-32768,+32767]$，浮点表示$[-1,+1]$。

## 读取工具

<img src="./Learning.assets/image-20230916134116136.png" alt="image-20230916134116136" style="zoom:33%;" />

（使用时要注意库对硬件的支持，librosa对CQT变换仅支持CPU，数据量大时，尽量使用pyaudio）



## 预处理

### 静音消除（消前后）

<img src="./Learning.assets/image-20230916140223993.png" alt="image-20230916140223993" style="zoom: 50%;" />

### 静音消除（消所有）

<img src="./Learning.assets/image-20230916140727926.png" alt="image-20230916140727926" style="zoom:50%;" />



### 频域分析

<img src="./Learning.assets/image-20230916141159555.png" alt="image-20230916141159555" style="zoom: 50%;" />

<img src="./Learning.assets/image-20230916141927804.png" alt="image-20230916141927804" style="zoom:50%;" />

<img src="./Learning.assets/image-20230916142309220.png" alt="image-20230916142309220" style="zoom:50%;" />

### 预加重

<img src="./Learning.assets/image-20230916142614618.png" alt="image-20230916142614618" style="zoom:50%;" />

<img src="./Learning.assets/image-20230916142631192.png" alt="image-20230916142631192" style="zoom:50%;" />

### Mel滤波器

<img src="./Learning.assets/image-20230916142847378.png" alt="image-20230916142847378" style="zoom:50%;" />

要注意Mel的三角滤波器在不同的实现中可能不同，而且细节差异可能导致结果不同。

<img src="./Learning.assets/image-20230916144028795.png" alt="image-20230916144028795" style="zoom:67%;" />

<img src="./Learning.assets/image-20230916144101169.png" alt="image-20230916144101169" style="zoom:67%;" />

<img src="./Learning.assets/image-20230916144400566.png" alt="image-20230916144400566" style="zoom: 67%;" />



## 语音增强（语音去噪）

目的在于消除语音中存在的噪声，增加语音听感与可懂度。

<img src="./Learning.assets/image-20230918102359875.png" alt="image-20230918102359875" />

### 谱减法

<img src="./Learning.assets/image-20230916151341523.png" alt="image-20230916151341523" />

要注意减出来负值，要强制归整到0。最后利用干净语音的幅度谱和含躁语音的相位谱，经过逆离散傅里叶反变换，就可以得出干净语音信号。

简单的谱减法容易造成噪声残留，实际效果并不理想。

### 过减法

<img src="./Learning.assets/image-20230917123428985.png" alt="image-20230917123428985" style="zoom:67%;" />

<img src="./Learning.assets/image-20230917125029815.png" alt="image-20230917125029815" />

缺点：减量太多容易破坏原本连续的谱线，若要改进，则要引入平滑机制。

平滑机制为：最大噪声残差

<img src="./Learning.assets/image-20230917125209512.png" alt="image-20230917125209512" style="zoom:50%;" />

### Wiener滤波

<img src="./Learning.assets/image-20230917134523044.png" alt="image-20230917134523044" />

<img src="./Learning.assets/9f85517ee6578838aada304f5956d07.jpg" alt="9f85517ee6578838aada304f5956d07" />

<img src="./Learning.assets/image-20230917142026325.png" alt="image-20230917142026325" />

维纳滤波的变种

<img src="./Learning.assets/image-20230917142647142.png" alt="image-20230917142647142" />

<img src="./Learning.assets/image-20230917150909622.png" alt="image-20230917150909622" />

- 情景一
	设计滤波器时，必须预先知道无躁信号Clean，如果不知道无噪信号，则无法设计。在clean未知的情况下，可以利用谱减法去估计clean，再使用Wiener滤波器进行语音增强。
- 情景二
	如果已知噪声的某些分布特性，可以通过人为向干净语音加噪声的方法获取一组训练数据，利用这些数据训练维纳滤波器H进行滤波

局限性：

<img src="./Learning.assets/image-20230917160439399.png" alt="image-20230917160439399" style="zoom:50%;" />

### 最小均方误差估计

Minimum Mean Square Error Estimation

<img src="./Learning.assets/07f376838d792b5fdb7e67b1f014c0d.jpg" alt="07f376838d792b5fdb7e67b1f014c0d" style="zoom:50%;" />

<img src="./Learning.assets/image-20230917162701656.png" alt="image-20230917162701656" style="zoom:50%;" />

<img src="./Learning.assets/image-20230917163530878.png" alt="image-20230917163530878" style="zoom:50%;" />

<img src="./Learning.assets/image-20230917163807686.png" alt="image-20230917163807686" style="zoom:50%;" />

<img src="./Learning.assets/image-20230917164425256.png" alt="image-20230917164425256" style="zoom:50%;" />

<img src="./Learning.assets/image-20230917164514248.png" alt="image-20230917164514248" />

<img src="./Learning.assets/image-20230918083649620.png" alt="image-20230918083649620" style="zoom:50%;" />

<img src="./Learning.assets/image-20230918084211858.png" alt="image-20230918084211858" style="zoom: 67%;" />

<img src="./Learning.assets/image-20230918092919808.png" alt="image-20230918092919808" style="zoom:67%;" />

<img src="./Learning.assets/image-20230918092954899.png" alt="image-20230918092954899" style="zoom: 67%;" />

<img src="./Learning.assets/image-20230918093619528.png" alt="image-20230918093619528" />

<img src="./Learning.assets/image-20230918093722801.png" alt="image-20230918093722801" />

### 子空间法Subspace

参考文献：

> Yi Hu and P. C. Loizou, "A generalized subspace approach for enhancing speech corrupted by colored noise," in *IEEE Transactions on Speech and Audio Processing*, vol. 11, no. 4, pp. 334-341, July 2003, doi: 10.1109/TSA.2003.814458.

<img src="./Learning.assets/image-20230918093936878.png" alt="image-20230918093936878" />

即映射到信号子空间和噪声子空间（图中$P_iP_i$等应该有转置符号，并未写出）

<img src="./Learning.assets/image-20230918094410820.png" alt="image-20230918094410820" style="zoom:67%;" />

<img src="./Learning.assets/image-20230918094848898.png" alt="image-20230918094848898" />

<img src="./Learning.assets/image-20230918095026224.png" alt="image-20230918095026224" style="zoom:67%;" />

<img src="./Learning.assets/87aa6e0d4b39913158fbc067a90260e.jpg" alt="87aa6e0d4b39913158fbc067a90260e"  />

<img src="./Learning.assets/11d4d7e823a9ee2f577a9778b8a231f.jpg" alt="11d4d7e823a9ee2f577a9778b8a231f" />

<img src="./Learning.assets/image-20230918125350811.png" alt="image-20230918125350811" />

<img src="./Learning.assets/image-20230918131607730.png" alt="image-20230918131607730" />

<img src="./Learning.assets/image-20230918131727264.png" alt="image-20230918131727264" />



### DNN频谱映射

非传统统计方法，不需要人工设计滤波器

<img src="./Learning.assets/image-20230919115315514.png" alt="image-20230919115315514" />



### DNN-IRM















