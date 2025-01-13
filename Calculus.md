## const
* $ A^3 + B^3 = (A + B)(A^2 - AB + B^2) $
* $ A^3 - B^3 = (A - B)(A^2 + AB + B^2) $

* 不定积分: 逆向还原导数, 得到函数的原函数
* 定积分: 计算函数在某一区间的累积量

* $ sin(x+y) = sin(x) * cos(y) + sin(y) * cos(x) $
* $ cos(x+y) = cos(x) * cos(y) - sin(y) * sin(x) $

* $  $

## 1800 可以重做的题
* p4: 1
## little point
* 费马引理: 当原函数曲线 `平` 时, f'(x) == 0 


## 放起来没看的
* 三角函数中的万能公式
## 三角函数
* `cot(Cotangent)`: 和 `tan` 互为倒数
* `sec(Secant)`: 和 `cos` 互为倒数
* `csc(Cosecant)`: 和 `sin` 互为倒数
### 同角
* $\mathrm{sec^2x = 1 + tan^2x}$
* $\mathrm{csc^2x = 1 + cot^2x}$
### 倍角
* $\mathrm{sin2x = 2sinxcosx}$
* $\mathrm{cos2x = cos^2x-sin^2x = 2cos^2x-1}$
* $\mathrm{cos2x = cos^2x-sin^2x = 2cos^2x-1}$
* $\mathrm{tan2x = {{2tanx} \over {1-tan^2x}}}$ (自己尝试推时上下同除 `cos^2x`)
### 幂
* $\mathrm{sin^2x = {{1+cos2x} \over {2}}}$
* $\mathrm{cos^2x = {{1-cos2x} \over {2}}}$
* $\mathrm{tan^2x = {{1-cos2x} \over {1+cos2x}}}$
* 使用 $cos2x = 2cos^2x-1 = 1-2sin^2x$ 来推
### 半角
* 使用 幂 公式中 2x 替换为 x, x 替换为 x/2, 开方就能得到
* $\mathrm{sin{a \over 2} = \pm\sqrt{{1-cosa}\over{2}}}$
* $\mathrm{cos{a \over 2} = \pm\sqrt{{1+cosa}\over{2}}}$
* $\mathrm{tan{a \over 2} = \pm\sqrt{{1-cosa}\over{1+cosa}}}$
### 和差化积
* $\mathrm{sin(a \pm b) = sin(a)cos(b) \pm sin(b)cos(a)}$
* $\mathrm{cos(a + b) = cos(a)cos(b) - sin(b)sin(a)}$
* $\mathrm{sin(a - b) = cos(a)cos(b) + sin(b)sin(a)}$
* $\mathrm{tan(a+b) = {{tan(a) + tan(b)}\over{1-tan(a)tan(b)}}}$
### 积化和差
* 使用 `和差化积` 中的公式`相加`或者`相减`得到
* $\mathrm{sin(a)cos(b) = {1\over2}\{sin(a+b) + sin(a-b)\}}$ 
* $\mathrm{cos(a)cos(b) = {1\over2}\{cos(a+b) + cos(a-b)\}}$ 
* $\mathrm{sin(a)sin(b) = {1\over2}\{cos(a+b) - cos(a-b)\}}$ 
### 反三角
* 就是交换 三角函数中 `x` 和 `y`(输入和输出) 的位置
### 不等式(写下了, 但是还是不懂, 得取研究下)
* 三角不等式:
    * $||a|-|b|| \le |a \pm b| \le |a| + |b|$
* 算术几何不等式: 
    * $a^2 + b^2 \ge 2ab$
    * $|ab| \le {{a^2+b^2}\over{2}}$
    * $a_i \ge 0$, ${{a_1 + ... + a_n} \over n} \ge ^n\sqrt{a_1...a_n}$
* 柯西不等式(不懂的)
# 柯西不等式, 此为标记

## 基本初等函数
* 初等函数的成分里最基础的单位, 不能再分的单位
* $y = x^a$
* $y = a^x$
* $y = log_ax$
* $sinx, cosx, tanx, cotx, secx, cscx$
* $arcsinx, arccosx, arctanx, arccotx$
## 初等函数
* 有`常数`, `基本初等函数`构成的函数
## 奇偶性
* 关于`原点`对称: `奇`, 如`sinx`
* 关于`y 轴`对成: `偶`, 如`cosx`
### 判断函数是`奇`还是`偶`
* 证明出 `f(x) == f(-x)` -> `偶`
* 证明出 `-f(x) == f(-x)` -> `奇`
