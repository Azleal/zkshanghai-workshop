# 第5课 课后作业

## 第1题 $KZG$ 多项式承诺方案在 $Setup$ 阶段涉及到计算对秘密评估点 $\tau$ 的幂的承诺，这被称为“可信设置”，通常在被称为“Powers of Tau”的仪式中利用多方计算生成。 假如说有一天，你在一张纸条上找到了 $\tau$ 的值。 你怎么能用它来制作一个假的 $KZG$ 证明呢？

1. 选择一个随机的多项式 f(x) 。

2. 使用泄露的 tau 和该多项式来计算 KZG 承诺。这个承诺将形式为 g^(P(tau))，其中 g 是群的生成元。

3. 选择想要证明的一个点 x0（可以是任何值，不需要是多项式 f(x) 的一个根）以及一个想要证明的值 y0。

4. 制作一个证明，表明 P(x) 在 x0 处的值等于 y0。使用泄露的 tau 和选择的点可以计算出一个看起来像是对应于该多项式在该点的有效证明的假证明。这个假的 KZG 证明并没有真的证明 P(x) 在 x0 处的值等于 y0，而是因为 tau 的泄露，使得获取该 tau 的攻击者制作了这个实际假的但看起来有效的证明。


## 第2题 从 $KZG$ 多项式承诺方案构造一个**向量承诺方案**。 （提示：对于向量 $m=\left(m_{1}, \ldots, m_{q}\right)$，是否存在一个“插值多项式”$I(X)$ 使得 $I\left(x_{i}\right)=y_{i}$？）
::: tip 有趣的事实
Verkle 树 [1] 是一种使用向量承诺而不是哈希函数的 Merkle 树。 使用 KZG 向量承诺方案，您能看出为什么 Verkle 树更高效吗？
::::

1. 对于向量 $m =\left(m_{1}, ..., m_{q}\right)$，选择一组不同的点 $x_{1}, x_{2}, ..., x_{q}$，并将向量元素 $m_{i}$ 映射到点 $x_{i}$，得到一组点对 $\left(x_{i}, m_{i}\right)$。

2. 使用这些点对构造一个插值多项式 $I(X)$，满足 $I\left(x_{i}\right)$ = $m_{i}$ ( 对于所有的 i )。

3. 使用 $KZG$ 多项式承诺方案为插值多项式 $I(X)$ 生成承诺。

这样生成的承诺实际上就是向量 m 的承诺，能验证向量 m 的任意元素。


## 第3题  $KZG$ 多项式承诺方案对关系 $p(x)=$ $y$ 进行披露证明 $\pi$。 你能扩展这个方案来产生一个多重证明 $\pi$，让我们相信 $p\left(x_{i}\right)=y_{i}$ 对于点列表和评估 $\left(x_{i }, y_{i}\right)$ ？ （提示：假设您有一个插值多项式 $I(X)$ 使得 $I\left(x_{i}\right)=y_{i}$）。

1. 对于给定的点和评估 $\left(x_{i }, y_{i}\right)$，找到一个插值多项式 $I(X)$ ，满足 $I\left(x_{i}\right)=y_{i}$ 。

2. 使用 $KZG$ 多项式承诺方案为插值多项式 $I(X)$ 生成承诺，并生成对应的证明 $\pi$ 。

$\pi$ 就是多重证明，表明 $I\left(x_{i}\right)=y_{i}$ ( 对于所有的 i )。验证多重证明只需对每个 i 验证 $I\left(x_{i}\right)=y_{i}$。
