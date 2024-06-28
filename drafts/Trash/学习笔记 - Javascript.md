## JS对象

### 运算符

#### 条件运算符

用于基于条件的赋值运算。

**语法**

```js
变量 = (条件) ? 值1:值2
```

**例子**

```javascript
voteable = (age < 18) ? "太年轻而不能":"年龄够";
```



## 语句参考手册

### 循环相关语句

#### continue

**定义和用法**

continue 用于跳过循环中的一个迭代，并继续执行循环中的下一个迭代。

continue 与 [break](https://www.runoob.com/jsref/jsref-break.html) 语句的区别是， break 是结束整个循环体，continue是结束单次循环。

但是，在执行 continue 语句时，表现出了两种不同类型的循环：

- 在 **while** 循环中，会先判断条件，如果条件为 true，循环再执行一次。
- 在 **for** 循环中，自增长表达式 (如：i++) 会先计算，然后再判断条件是否为true，再决定是否执行迭代。
