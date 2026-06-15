# 密码学 习题集 - 密钥交换与数论基础

---

## 第 1 题

考虑课上讨论的使用在线可信第三方（TTP）的玩具密钥交换协议。假设 Alice、Bob 和 Carol 是该系统中的三个用户（系统中还有许多其他用户），他们分别与 TTP 共享秘密密钥 $k_a$、$k_b$、$k_c$。

他们希望生成一个群组会话密钥 $k_{ABC}$，该密钥应当被 Alice、Bob 和 Carol 知道，但不能被窃听者知道。应如何修改课上的协议，使其支持这种群组密钥交换？（注意：这些协议都不能抵抗主动攻击。）

- [ ] Alice 联系 TTP。TTP 生成随机的 $k_{ABC}$，并发送给 Alice：

  $$
  E(k_a, k_{ABC}),\quad
  \text{ticket}_1 \leftarrow E(k_c, E(k_b, k_{ABC})),\quad
  \text{ticket}_2 \leftarrow E(k_b, E(k_c, k_{ABC}))
  $$

  Alice 将 $k_{ABC}$ 发送给 Bob，并将 $k_{ABC}$ 发送给 Carol。

- [ ] Bob 联系 TTP。TTP 生成随机的 $k_{AB}$ 和随机的 $k_{BC}$，并发送给 Bob：

  $$
  E(k_a, k_{AB}),\quad
  \text{ticket}_1 \leftarrow E(k_a, k_{AB}),\quad
  \text{ticket}_2 \leftarrow E(k_c, k_{BC})
  $$

  Bob 将 $\text{ticket}_1$ 发送给 Alice，将 $\text{ticket}_2$ 发送给 Carol。

- [x] Alice 联系 TTP。TTP 生成随机的 $k_{ABC}$，并发送给 Alice：

  $$
  E(k_a, k_{ABC}),\quad
  \text{ticket}_1 \leftarrow E(k_b, k_{ABC}),\quad
  \text{ticket}_2 \leftarrow E(k_c, k_{ABC})
  $$

  Alice 将 $\text{ticket}_1$ 发送给 Bob，将 $\text{ticket}_2$ 发送给 Carol。

---

## 第 2 题

设 $G$ 是一个有限循环群（例如 $G = \mathbb{Z}_p^*$），生成元为 $g$。假设 Diffie-Hellman 函数

$$
\operatorname{DH}_g(g^x, g^y) = g^{xy}
$$

在 $G$ 中难以计算。以下哪些函数也难以计算？

像往常一样，请找出下面的函数 $f$，使得如下逆否命题成立：如果 $f(\cdot,\cdot)$ 容易计算，那么 $\operatorname{DH}_g(\cdot,\cdot)$ 也容易计算。若能证明这一点，则可推出：如果 $\operatorname{DH}_g$ 在 $G$ 中是困难的，那么 $f$ 也必须是困难的。

- [x] $f(g^x, g^y) = g^{x(y+1)}$

- [ ] $f(g^x, g^y) = (g^{3xy}, g^{2xy})$（该函数输出 $G$ 中的一对元素）

- [ ] $f(g^x, g^y) = g^{x-y}$

---

## 第 3 题

假设我们对 Diffie-Hellman 协议做如下修改：Alice 像通常一样，随机选择 $a \in \{1,\ldots,p-1\}$，并向 Bob 发送

$$
A \leftarrow g^a
$$

但 Bob 随机选择 $b \in \{1,\ldots,p-1\}$，并向 Alice 发送

$$
B \leftarrow g^{1/b}
$$

他们可以生成什么共享秘密？应如何生成？

- [ ] 共享秘密为 $g^{a/b}$。Alice 计算 $B^{1/b}$，Bob 计算 $A^a$。

- [ ] 共享秘密为 $g^{ab}$。Alice 计算 $B^{1/a}$，Bob 计算 $A^b$。

- [x] 共享秘密为 $g^{a/b}$。Alice 计算 $B^a$，Bob 计算 $A^{1/b}$。

- [ ] 共享秘密为 $g^{ab}$。Alice 计算 $B^a$，Bob 计算 $A^b$。

---

## 第 4 题

考虑课上的使用公钥加密的玩具密钥交换协议。

假设 Bob 向 Alice 发送回复 $c \leftarrow E(pk, x)$ 时，还在密文后附加一个 MAC 标签

$$
t := S(x, c)
$$

因此 Alice 收到的是二元组 $(c,t)$。Alice 验证标签 $t$，若标签验证失败，则拒绝 Bob 的消息。

这个额外步骤是否能阻止课上描述的中间人攻击？

- [ ] 取决于使用的 MAC 系统
- [ ] 能
- [x] 不能
- [ ] 取决于使用的公钥加密系统

---

## 第 5 题

7 和 23 互素，因此一定存在整数 $a$ 和 $b$，使得

$$
7a + 23b = 1
$$

请找出满足条件且 $a > 0$ 尽可能小的一组整数 $(a,b)$。

给定这组 $(a,b)$ 后，能否确定 $7$ 在 $\mathbb{Z}_{23}$ 中的逆元？

请按逗号分隔的格式填写 $a$、$b$，以及 $7^{-1}$ 在 $\mathbb{Z}_{23}$ 中的值。

答案：
# 第5题 解答

\[
\begin{align*}
23 &= 3 \times 7 + 2 \\
7  &= 3 \times 2 + 1
\end{align*}
\]

\[
\begin{align*}
1 &= 7 - 3 \times 2 \\
  &= 7 - 3 \times (23 - 3 \times 7) \\
  &= 10 \times 7 - 3 \times 23
\end{align*}
\]

因此 \(a = 10,\ b = -3\)。

\[
7 \times 10 \equiv 1 \pmod{23}
\]

故 \(7^{-1} \equiv 10 \pmod{23}\)。

---


## 第 6 题

求解 $\mathbb{Z}_{19}$ 中的方程：

$$
3x + 2 = 7
$$

答案：

\[
\begin{align*}
3x + 2 &= 7 \pmod{19} \\
3x &= 5 \pmod{19}
\end{align*}
\]

\[
\begin{align*}
19 &= 6 \times 3 + 1 \\
1 &= 19 - 6 \times 3 \\
-6 \times 3 &\equiv 1 \pmod{19} \\
13 \times 3 &\equiv 1 \pmod{19}
\end{align*}
\]

\[
\begin{align*}
x &\equiv 5 \times 13 \pmod{19} \\
x &\equiv 65 \pmod{19} \\
x &\equiv 8 \pmod{19}
\end{align*}
\]

---

## 第 7 题

$\mathbb{Z}_{35}^*$ 中有多少个元素？

答案：



\(\mathbb{Z}_{35}^*\) 表示模35的乘法群，其元素个数由欧拉函数 \(\varphi(35)\) 给出。

\[
\begin{align*}
\varphi(35) &= \varphi(5 \times 7) \\
&= \varphi(5) \times \varphi(7) \\
&= (5-1) \times (7-1) \\
&= 4 \times 6 \\
&= 24
\end{align*}
\]

因此，\(\mathbb{Z}_{35}^*\) 中有 **24** 个元素。

---

## 第 8 题

不使用计算器，求：

$$
2^{10001} \bmod 11
$$

提示：使用费马小定理。

答案：


\[
2^{10001} \bmod 11
\]

根据费马小定理，对素数 \(p=11\)，且 \(2\) 与 \(11\) 互素，有：
\[
2^{10} \equiv 1 \pmod{11}
\]

\[
\begin{align*}
10001 &= 10 \times 1000 + 1 \\
2^{10001} &= 2^{10 \times 1000 + 1} \\
&= (2^{10})^{1000} \times 2^1 \\
&\equiv 1^{1000} \times 2 \pmod{11} \\
&\equiv 2 \pmod{11}
\end{align*}
\]

\[
2^{10001} \bmod 11 = 2
\]

---

## 第 9 题

继续上一题，求：

$$
2^{245} \bmod 35
$$

提示：使用欧拉定理，你不需要计算器。

答案：

# 第9题 解答

\[
2^{245} \bmod 35
\]

欧拉函数：
\[
\varphi(35) = \varphi(5 \times 7) = \varphi(5)\varphi(7) = 4 \times 6 = 24
\]

根据欧拉定理，因 \(\gcd(2,35)=1\)，有：
\[
2^{24} \equiv 1 \pmod{35}
\]

指数化简：
\[
245 = 24 \times 10 + 5
\]
\[
2^{245} = 2^{24 \times 10 + 5} = (2^{24})^{10} \times 2^5
\]
\[
\equiv 1^{10} \times 2^5 \pmod{35}
\]
\[
\equiv 32 \pmod{35}
\]

\[
2^{245} \bmod 35 = 32
\]

---

## 第 10 题

2 在 $\mathbb{Z}_{35}^*$ 中的阶是多少？

答案：

\[
\begin{align*}
2^1 &\equiv 2 \not\equiv 1 \pmod{35} \\
2^2 &\equiv 4 \not\equiv 1 \pmod{35} \\
2^3 &\equiv 8 \not\equiv 1 \pmod{35} \\
2^4 &\equiv 16 \not\equiv 1 \pmod{35} \\
2^5 &\equiv 32 \not\equiv 1 \pmod{35} \\
2^6 &\equiv 64 \equiv 29 \not\equiv 1 \pmod{35} \\
2^7 &\equiv 58 \equiv 23 \not\equiv 1 \pmod{35} \\
2^8 &\equiv 46 \equiv 11 \not\equiv 1 \pmod{35} \\
2^9 &\equiv 22 \not\equiv 1 \pmod{35} \\
2^{10} &\equiv 44 \equiv 9 \not\equiv 1 \pmod{35} \\
2^{11} &\equiv 18 \not\equiv 1 \pmod{35} \\
2^{12} &\equiv 36 \equiv 1 \pmod{35}
\end{align*}
\]
故 \(2\) 在 \(\mathbb{Z}_{35}^*\) 中的阶为 \(12\)。

---
---

## 第 11 题

以下哪些数是 $\mathbb{Z}_{13}^*$ 的生成元？

- [ ] $4,\quad \langle 4 \rangle = \{1,4,3,12,9,10\}$

- [x] $6,\quad \langle 6 \rangle = \{1,6,10,8,9,2,12,7,3,5,4,11\}$

- [ ] $3,\quad \langle 3 \rangle = \{1,3,9\}$

- [x] $7,\quad \langle 7 \rangle = \{1,7,10,5,9,11,12,6,3,8,4,2\}$

- [ ] $8,\quad \langle 8 \rangle = \{1,8,12,5\}$

---

## 第 12 题

求解 $\mathbb{Z}_{23}$ 中的方程：

$$
x^2 + 4x + 1 = 0
$$

请使用二次公式方法。

答案：



求解 \(\mathbb{Z}_{23}\) 中的方程：
\[
x^2 + 4x + 1 = 0
\]

### 1. 计算判别式
\[
\Delta = b^2 - 4ac = 4^2 - 4 \times 1 \times 1 = 16 - 4 = 12 \pmod{23}
\]

### 2. 求 \(\Delta = 12\) 在 \(\mathbb{Z}_{23}\) 中的平方根
检验：
\[
\begin{align*}
5^2 &= 25 \equiv 2 \pmod{23} \\
6^2 &= 36 \equiv 13 \pmod{23} \\
7^2 &= 49 \equiv 3 \pmod{23} \\
8^2 &= 64 \equiv 18 \pmod{23} \\
9^2 &= 81 \equiv 12 \pmod{23}
\end{align*}
\]
因此 \(12\) 的平方根为 \(\pm 9\)，即 \(9\) 和 \(14\)（因为 \(-9 \equiv 14 \pmod{23}\)）。

### 3. 应用二次公式
\[
x = \frac{-b \pm \sqrt{\Delta}}{2a} = \frac{-4 \pm 9}{2} \pmod{23}
\]

先求 \(2\) 在 \(\mathbb{Z}_{23}\) 中的逆元：
\[
2 \times 12 = 24 \equiv 1 \pmod{23} \implies 2^{-1} = 12
\]

计算两个解：
\[
\begin{align*}
x_1 &= \frac{-4 + 9}{2} = \frac{5}{2} = 5 \times 12 = 60 \equiv 14 \pmod{23} \\
x_2 &= \frac{-4 - 9}{2} = \frac{-13}{2} = 10 \times 12 = 120 \equiv 5 \pmod{23}
\end{align*}
\]

### 4. 验证解
- \(x=5\): \(5^2 + 4 \times 5 + 1 = 25 + 20 + 1 = 46 \equiv 0 \pmod{23}\)
- \(x=14\): \(14^2 + 4 \times 14 + 1 = 196 + 56 + 1 = 253 \equiv 0 \pmod{23}\)

因此，方程的解为：
\[
x = 5, 14 \pmod{23}
\]

---

## 第 13 题

求 2 在 $\mathbb{Z}_{19}$ 中的 11 次根，即求：

$$
2^{1/11} \in \mathbb{Z}_{19}
$$

提示：注意 $11^{-1} = 5$ 在 $\mathbb{Z}_{18}$ 中成立。

答案：



求 \(2^{1/11}\) 在 \(\mathbb{Z}_{19}\) 中的值，即求解 \(x^{11} \equiv 2 \pmod{19}\)。

---

根据费马小定理，对于素数 \(p=19\)，有 \(a^{18} \equiv 1 \pmod{19}\)。
提示给出 \(11^{-1} \equiv 5 \pmod{18}\)，因为 \(11 \times 5 = 55 \equiv 1 \pmod{18}\)。

\[
\begin{align*}
x^{11} &\equiv 2 \pmod{19} \\
(x^{11})^5 &\equiv 2^5 \pmod{19} \\
x^{55} &\equiv 32 \pmod{19}
\end{align*}
\]

化简指数：
\[
55 = 3 \times 18 + 1
\]
\[
x^{55} = (x^{18})^3 \cdot x^1 \equiv 1^3 \cdot x \equiv x \pmod{19}
\]

因此：
\[
x \equiv 32 \pmod{19}
\]
\[
x \equiv 13 \pmod{19}
\]

---

验证：
\[
13^{11} \equiv 2 \pmod{19}
\]

\[
2^{1/11} \equiv 13 \pmod{19}
\]

---

## 第 14 题

求 $\mathbb{Z}_{13}$ 中以 2 为底、5 的离散对数：

$$
\operatorname{Dlog}_2(5)
$$

回忆：2 在 $\mathbb{Z}_{13}$ 中的幂为

$$
\langle 2 \rangle = \{1,2,4,8,3,6,12,11,9,5,10,7\}
$$

答案：



离散对数 \( \text{Dlog}_2(5) \) 定义为满足 \( 2^x \equiv 5 \pmod{13} \) 的最小非负整数 \( x \)。

已知 \( 2 \) 在 \( \mathbb{Z}_{13} \) 中的幂为：
\[
\langle 2 \rangle = \{1, 2, 4, 8, 3, 6, 12, 11, 9, 5, 10, 7\}
\]
按顺序对应 \( 2^0, 2^1, 2^2, \dots, 2^{11} \)。

观察序列可知，元素 \( 5 \) 位于第 \( 10 \) 个位置（从0开始计数），即：
\[
2^{9} \equiv 5 \pmod{13}
\]

因此：
\[
\text{Dlog}_2(5) = 9
\]

---

## 第 15 题

如果 $p$ 是素数，那么 $\mathbb{Z}_p^*$ 中有多少个生成元？

- [ ] $(p+1)/2$
- [ ] $\varphi(p)$
- [x] $\varphi(p-1)$
- [ ] $\sqrt{p}$
