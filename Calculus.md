## temp
$  $
## 可微?
## 0基础_status
* 01: done, but不等式? 
* 02: done 
* 03: 0:32:38 
* 04: 0:35:24
* 07: done, but反函数?
* 08: done

## concept
* 不定积分: 逆向还原导数, 得到函数的原函数
* 定积分: 计算函数在某一区间的累积量
> * __倍角公式__
> * $ sin2x = 2sinxcosx$
>
> * $ cos2x = cos^2x-sin^2x = 2cos^2x-1$
>
> * $ cos2x = cos^2x-sin^2x = 2cos^2x-1$
>
> * $ tan2x = {{2tanx} \over {1-tan^2x}}$ (推理时上下同除 `cos^2x`)

> * __高幂转低幂__
> * $sin^2x = {{1+cos2x} \over {2}}$
>
> * $cos^2x = {{1-cos2x} \over {2}}$
>
> * $tan^2x = {{1-cos2x} \over {1+cos2x}}$
>
> * (使用 $cos2x = 2cos^2x-1 = 1-2sin^2x$ 来推)

* > 半角公式
* $sin{a \over 2} = \pm\sqrt{{1-cosa}\over{2}}$
* $cos{a \over 2} = \pm\sqrt{{1+cosa}\over{2}}$
* $tan{a \over 2} = \pm\sqrt{{1-cosa}\over{1+cosa}}$
* 使用 `高幂转低幂` 公式中 2x 替换为 x, x 替换为 x/2, 开方就能得到

## theory
* 费马引理: 当原函数曲线 `平` 时, f'(x) == 0 
## 放起来没看的
* 三角函数中的万能公式
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
### 不等式 ?
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
## 无穷小
* 以 `0` 为极限的函数称为 `无穷小`
    * 满足 `函数` 和 `极限为 0` 两个条件就是无穷小

* 除了 `0` 以外, 函数是否是无穷小和 x 的趋向有关
> * 有函数 $ f(x) = 3(x-1)^2 $
>   * $ x\to 2, \lim f(x) = 2 $, 此时函数不是无穷小
>   * $ x\to 1, \lim f(x) = 0 $, 此时函数是无穷小
## 判断函数是`奇`还是`偶`
* 证明出 `f(x) == f(-x)` -> `偶`
* 证明出 `-f(x) == f(-x)` -> `奇`
## 1800 
* p4: 1
