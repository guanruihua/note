---
title: typora
date: 2020-09-08 20:51:24
tags:
	- typora
	- tool
---

# typora

## 快捷键


```
Ctrl+1  一阶标题    Ctrl+B  字体加粗 
Ctrl+2  二阶标题    Ctrl+I  字体倾斜 
Ctrl+3  三阶标题    Ctrl+U  下划线 
Ctrl+4  四阶标题    Ctrl+Home   返回Typora顶部 
Ctrl+5  五阶标题    Ctrl+End    返回Typora底部 
Ctrl+6  六阶标题    Ctrl+T  创建表格 
Ctrl+L  选中某句话   
Ctrl+K  创建超链接  Ctrl+D  选中某个单词  
Ctrl+F  搜索 			 Ctrl+E  选中相同格式的文字   
Ctrl+H  搜索并替换  Alt+Shift+5 删除线 
Ctrl+Shift+I    插入图片 
Ctrl+Shift+M    公式块 
Ctrl+Shift+Q    引用 
注：一些实体符号需要在实体符号之前加”\”才能够显示 
```

## 图

### 流程图

#### 横向流程图

```mermaid

graph LR

A[方形] -->B(圆角)

    B --> C{条件a}

    C -->|a=1| D[结果1]

    C -->|a=2| E[结果2]

    F[横向流程图]

```
#### 竖向流程图

```mermaid

graph TD

A[方形] -->B(圆角)

    B --> C{条件a}

    C -->|a=1| D[结果1]

    C -->|a=2| E[结果2]

    F[竖向流程图]

```
#### 标准流程图
```flow

st=>start: 开始框

op=>operation: 处理框

cond=>condition: 判断框(是或否?)

sub1=>subroutine: 子流程

io=>inputoutput: 输入输出框

e=>end: 结束框

st->op->cond

cond(yes)->io->e

cond(no)->sub1(right)->op

```
#### 标准流程源码（横向）
```flow

st=>start: 开始框

op=>operation: 处理框

cond=>condition: 判断框(是或否?)

sub1=>subroutine: 子流程

io=>inputoutput: 输入输出框

e=>end: 结束框

st(right)->op(right)->cond

cond(yes)->io(bottom)->e

cond(no)->sub1(right)->op

```

### 时序图

#### 时序图源码
```sequence

对象A->对象B: 对象B你好吗?（请求）

Note right of 对象B: 对象B的描述

Note left of 对象A: 对象A的描述(提示)

对象B-->对象A: 我很好(响应)

对象A->对象B: 你真的好吗？

```
#### 复杂时序图源码
```sequence

Title: 标题：复杂使用

对象A->对象B: 对象B你好吗?（请求）

Note right of 对象B: 对象B的描述

Note left of 对象A: 对象A的描述(提示)

对象B-->对象A: 我很好(响应)

对象B->小三: 你好吗

小三-->>对象A: 对象B找我了

对象A->对象B: 你真的好吗？

Note over 小三,对象B: 我们是朋友

participant C

Note right of C: 没人陪我玩

```
#### 标准时序图

```mermaid

%% 时序图例子,-> 直线，-->虚线，->>实线箭头

  sequenceDiagram

    participant 张三

    participant 李四

    张三->王五: 王五你好吗？

    loop 健康检查

        王五->王五: 与疾病战斗

    end

    Note right of 王五: 合理 食物 <br/>看医生...

    李四-->>张三: 很好!

    王五->李四: 你怎么样?

    李四-->王五: 很好!

```

### 甘特图

```mermaid

%% 语法示例
        gantt
        dateFormat  YYYY-MM-DD
        title 软件开发甘特图

        section 设计

        需求                      :done,    des1, 2014-01-06,2014-01-08

        原型                      :active,  des2, 2014-01-09, 3d

        UI设计                     :         des3, after des2, 5d

    未来任务                     :         des4, after des3, 5d

        section 开发

        学习准备理解需求                      :crit, done, 2014-01-06,24h

        设计框架                             :crit, done, after des2, 2d

        开发                                 :crit, active, 3d

        未来任务                              :crit, 5d

        耍                                   :2d

    

        section 测试

        功能测试                              :active, a1, after des3, 3d

        压力测试                               :after a1  , 20h

        测试报告                               : 48h

```

## 数学表达式

> - 需要在TeX或LaTeX格式的数学公式前后添加$$来实现
>
> - 可以使用数学公式块 "$$" + 回车
>   - 快捷键: Ctrl + Shift +  m
>   - 点击 "段落" + " 公式块" 
>
> - `$2^{2}$` : $2^{2}$
>
> - 
>
> - 公式块
>
>   - $$
>     y(x) = \begin{cases} \sqrt\frac{1}{x},x = 0\\ \sqrt\frac{2}{x}, x\neq0 \end{cases}
>     $$
>
> - 
>
> | 上/下标  | x^2, y_2                              | $x^2,y_2$                                 |
> | -------- | ------------------------------------- | ----------------------------------------- |
> | 分式     | 1/2, \frac{1}{2}                      | $1/2$, $ \frac{1}{2}$                     |
> | 省略号   | \cdots                                | $\cdots$                                  |
> | 开根号   | \sqrt{2}                              | $\sqrt{2}$                                |
> | 矢量     | \vec{a}                               | $\vec{a}$                                 |
> | 积分     | \int{x}dx, \int_{1}^{2}{x}dx          | $\int{x}dx$,$\int_{1}^{2}{x}dx$           |
> | 极限     | \lim{a+b}, \lim_{n\rightarrow+\infty} | $\lim{a+b}$, $\lim_{n\rightarrow+\infty}$ |
> | 累加     | \sum{a}, \sum_{n=1}^{100}{a_n}        | $\sum{a}$, $\sum_{n=1}^{100}{a_n}$        |
> | 累乘     | \prod{x},\prod_{n=1}^{n=99}{x_n}      | $\prod{x}$, $\prod_{n=1}^{99}{x_n}$       |
> | 三角函数 | \sin                                  | $\sin$                                    |
> | 对数函数 | \ln2, \log_2^8, \lg10                 | $\ln2$, $\log_2^8$,$\lg10$                |

### 关系运算符

| 运算符   | Markdown |
| -------- | -------- |
| $\pm$    | \pm      |
| $\times$ | \times   |
| $\cdot$  | \cdot    |
| $\div$   | \div     |
| $\neq$   | \neq     |
| $\leq$   | \leq     |
| $\geq$   | \geq     |
|          |          |

### 其他特殊字符

| 符号         | Markdown   |
| ------------ | ---------- |
| $\forall$    | \forall    |
| $\infty$     | \infty     |
| $\emptyset$  | \emptyset  |
| $\exists$    | \exists    |
| $\nabla$     | \nabla     |
| $\bot$       | \bot       |
| $\angle$     | \angle     |
| $\because$   | \because   |
| $\therefore$ | \therefore |
| 空格         | \quad      |
|              |            |



### 希腊字母

| 大写     | Markdown | 小写          | Markdown    |
| -------- | -------- | ------------- | ----------- |
| $A$      | A        | $\alpha$      | \alpha      |
| $B$      | B        | $\beta$       | \beta       |
| $\Gamma$ | \Gamma   | $\gamma$      | \gamma      |
| $\Delta$ | \Delta   | $\delta$      | \delta      |
| $E$      | E        | $\epsilon$    | \epsilon    |
|          |          | $\varepsilon$ | \varepsilon |
| $Z$      | Z        | $\zeta$       | \zeta       |
| $H$        | H        | $\eta$     | \eta     |
| $\Theta$   | \Theta   | $\theta$   | \theta   |
| $I$      | I        | $\iota$    | \iota    |
| $K$      | K        | $\kappa$   | \kappa   |
| $\Lambda$  | \Lambda  | $\lambda$  | \lambda  |
| $M$      | M        | $\mu$      | \mu      |
| $N$      | N        | $\nu$      | \nu      |
| $\Xi$      | \Xi      | $\xi$     | \xi      |
| $O$      | O        | $\omicron$ | \omicron |
| $\Pi$      | \Pi      | $\pi$      | \pi      |
| $P$      | P        | $\rho$     | \rho     |
| $\Sigma$   | \Sigma   | $\sigma$   | \sigma   |
| $T$      | T        | $\tau$     | \tau     |
| $\Upsilon$ | \Upsilon | $\upsilon$ | \upsilon |
| $\Phi$     | \Phi     | $\phi$     | \phi     |
|            |          | $\varphi$  | \varphi  |
| $X$      | X        | $\chi$     | \chi     |
| $\Psi$     | \Psi     | $\psi$     | \psi     |
| $\Omega$   | \Omega   | $\omega$   | \omega   |

## 其他

### 表格

> 快捷键 : Ctrl + T
>
> - 左对齐 | :---- |
> - 右对齐 | ----: |
> - 中对齐 | :----:|
```
| 表头  |      |      |
| ---- | ---- | ---- |
|      |      |      |
|      |      |      |
|      |      |      |
```

### 表情符号

> `: + 符号码`
>
> :smile:

