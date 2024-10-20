
--- 
title:  Python 炫技操作：五种 Python 转义表示法 
tags: []
categories: [] 

---
### 1. 为什么要有转义？

ASCII 表中一共有 128 个字符。这里面有我们非常熟悉的字母、数字、标点符号，这些都可以从我们的键盘中输出。除此之外，还有一些非常特殊的字符，这些字符，我通常很难用键盘上的找到，比如制表符、响铃这种。

为了能将那些特殊字符都能写入到字符串变量中，就规定了一个用于转义的字符 `\` ，有了这个字符，你在字符串中看的字符，print 出来后就不一定你原来看到的了。

举个例子

```
&gt;&gt;&gt; msg = "hello\013world\013hello\013python"
&gt;&gt;&gt; print(msg)
hello
     world
          hello
               python
&gt;&gt;&gt; 

```

是不是有点神奇？变成阶梯状的输出了。

那个 `\013` 又是什么意思呢？
-  `\` 是转义符号，上面已经说过 -  `013` 是 ASCII 编码的八进制表示，注意前面是 `0` 且不可省略，而不是字母 `o` 
把八进制的 13 转成 10 进制后是 11

<img src="https://img-blog.csdnimg.cn/img_convert/c5403e441316e31f37aec6c72f017685.png" alt="">

对照查看 ASCII 码表，11 对应的是一个垂直定位符号，这就能解释，为什么是阶梯状的输出字符串。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-izM0SikI-1606375376406)(http://image.iswbm.com/image-20201125122651086.png)]

### 2. 转义的 5 种表示法

ASCII 有 128 个字符，如果用 八进制表示，至少得有三位数，才能将其全部表示。这就是为什么说上面的首位 `0` 不能省略的原因，即使现在用不上，我也得把它空出来。

而如果使用十六进制，只要两位数就其 ASCII 的字符全部表示出来。同时为了避免和八进制的混淆起来，所以在 `\` 后面要加上英文字母 `x` 表示十六进制，后面再接两位十六进制的数值。
- `\` 开头并接三位 0-7 的数值，表示 8 进制- `\x` 开头并接两位 0-f 的数值，表示 16进制
因此，当我定义一个字符串的值为 `hello` + 回车 + `world` 时，就有了多种方法：

```
# 第一种方法：8进制
&gt;&gt;&gt; msg = "hello\012world"
&gt;&gt;&gt; print(msg)
hello
world
&gt;&gt;&gt; 

# 第二种方法：16 进制
&gt;&gt;&gt; msg = "hello\x0aworld"
&gt;&gt;&gt; print(msg)
hello
world
&gt;&gt;&gt; 

```

通常我们很难记得住一个字符的 ASCII 编号，即使真记住了，也要去转换成八进制或者16进制，实在是太难了。

因此对于一些常用并且比较特殊字符，我们习惯用另一种类似别名的方式，比如使用 `\n` 表示换行，它与 `\012` 、`\x0a` 是等价的。

与此类似的表示法，还有如下这些

<img src="https://img-blog.csdnimg.cn/img_convert/1be9e8aea3385419610abbb91a5bb491.png" alt="">

于是，要实现 `hello` + 回车 + `world` ，就有了第三种方法

```
# 第三种方法：使用类似别名的方法
&gt;&gt;&gt; msg = "hello\nworld"
&gt;&gt;&gt; print(msg)
hello
world
&gt;&gt;&gt; 

```

到目前为止，我们掌握了 三种转义的表示法。

已经非常难得了，让我们的脑洞再大一点吧，接下来再介绍两种。

ASCII 码表所能表示字符实在太有限了，想打印一个中文汉字，抱歉，你得借助 Unicode 码。

Unicode 编码由 4 个16进制数值组合而成

```
&gt;&gt;&gt; print("\u4E2D")
中

```

什么？我为什么知道 `中` 的 unicode 是 `\u4E2D`？像下面这样打印就知道啦

```
# Python 2.7
&gt;&gt;&gt; a = u"中"
&gt;&gt;&gt; a
u'\u4e2d'

```

由此，要实现 `hello` + 回车 + `world` ，就有了第四种方法。

```
# 第四种方法：使用 unicode ，\u000a 表示换行
&gt;&gt;&gt; print('hello\u000aworld')
hello
world

```

看到这里，你是不是以为要结束啦？

不，还没有。下面还有一种。

Unicode 编码其实还可以由 8 个32进制数值组合而成，为了以前面的区分开来，这里用 `\U` 开头。

```
# 第五种方法：使用 unicode ，\U0000000A 表示换行
&gt;&gt;&gt; print('hello\U0000000Aworld')
hello
world

```

好啦，目前我们掌握了五种转义的表示法。

总结一下：
1. `\` 开头并接三位 0-7 的数值（八进制） — 可以表示所有ASCII 字符1. `\x` 开头并接两位 0-f 的数值（十六进制） — 可以表示所有ASCII 字符1. `\u` 开头并接四位 0-f 的数值（十六进制） — 可以表示所有 Unicode 字符1. `\U` 开头并接八位 0-f 的数值（三十二进制）） — 可以表示所有 Unicode 字符1. `\` 开头后接除 x、u、U 之外的特定字符 — 仅可表示部分字符
为什么标题说，转义也可以炫技呢？

试想一下，假如你的同事，在打印日志时，使用这种 unicode 编码，然后你在定位问题的时候使用这个关键词去搜，却发现什么都搜不到？这就扑街了。

[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-za0JNg2d-1606375376413)(http://image.iswbm.com/image-20201126090917123.png)]

虽然这种行为真的很 sb，但在某些人看来也许是非常牛逼的操作呢？

五种转义的表示法到这里就介绍完成，接下来是更多转义相关的内容，也是非常有意思的内容，有兴趣的可以继续往下看。

### 3. raw 字符串

当一个字符串中具有转义的字符时，我们使用 print 打印后，正常情况下，输出的不是我们原来在字符串中看到的那样子。

那如果我们需要输出 `hello\nworld` ，不希望 Python 将 `\n` 转义成 换行符呢？

这种情况下，你可以在定义时将字符串定义成 raw 字符串，只要在字符串前面加个 `r` 或者 `R` 即可。

```
&gt;&gt;&gt; print(r"hello\nworld")
hello\nworld
&gt;&gt;&gt; 
&gt;&gt;&gt; print(R"hello\nworld")
hello\nworld

```

然而，不是所有时候都可以加 `r` 的，比如当你的字符串是由某个程序/函数返回给你的，而不是你自己生成的

```
# 假设这个是外来数据，返回 "hello\nworld"
&gt;&gt;&gt; body = spider()
&gt;&gt;&gt; print(body)
hello
world

```

这个时候打印它，`\n` 就是换行打印。

### 4. 使用 repr

对于上面那种无法使用 `r` 的情况，可以试一下 `repr` 来解决这个需求：

```
&gt;&gt;&gt; body = repr(spider())
&gt;&gt;&gt; print(body)
'hello\nworld'

```

经过 `repr` 函数的处理后，为让 print 后的结果，接近字符串本身的样子，它实际上做了两件事
1.  将 `\` 变为了 `\\` 1.  在字符串的首尾添加 `'` 或者 `"` 
你可以在 Python Shell 下敲入 变量 回车，就可以能看出端倪。

首尾是添加 `'` 还是 `"` ，取决于你原字符串。

```
&gt;&gt;&gt; body="hello\nworld"
&gt;&gt;&gt; repr(body)
"'hello\\nworld'"
&gt;&gt;&gt; 
&gt;&gt;&gt; 
&gt;&gt;&gt; body='hello\nworld'
&gt;&gt;&gt; repr(body)
"'hello\\nworld'"

```

### 5. 使用 string_escape

如果你还在使用 Python 2 ，其实还可以使用另一种方法。

那就是使用 `string.encode('string_escape')` 的方法，它同样可以达到 `repr` 的效果

```
&gt;&gt;&gt; "hello\nworld".encode('string_escape')
'hello\\nworld'
&gt;&gt;&gt; 

```

### 6. 查看原生字符串

综上，想查看原生字符串有两种方法：
1. 如果你在 Python Shell 交互模式下，那么敲击变量回车1. 如果不在 Python Shell 交互模式下，可先使用 `repr` 处理一下，再使用 print 打印
```
&gt;&gt;&gt; body="hello\nworld"
&gt;&gt;&gt; 
&gt;&gt;&gt; body
'hello\nworld'
&gt;&gt;&gt; 
&gt;&gt;&gt; print(repr(body))
'hello\nworld'
&gt;&gt;&gt; 

```

### 7. 恢复转义：转成原字符串

经过 `repr` 处理过或者 `\\` 取消转义过的字符串，有没有办法再回退出去，变成原先的有转义的字符串呢？

答案是：有。

如果你使用 Python 2，可以这样：

```
&gt;&gt;&gt; body="hello\\nworld"
&gt;&gt;&gt; 
&gt;&gt;&gt; body
'hello\\nworld'
&gt;&gt;&gt; 
&gt;&gt;&gt; body.decode('string_escape')
'hello\nworld'
&gt;&gt;&gt; 

```

如果你使用 Python 3 ，可以这样：

```
&gt;&gt;&gt; body="hello\\nworld"
&gt;&gt;&gt; 
&gt;&gt;&gt; body       
'hello\\nworld'
&gt;&gt;&gt; 
&gt;&gt;&gt; bytes(body, "utf-8").decode("unicode_escape")
'hello\nworld'
&gt;&gt;&gt; 

```

什么？还要区分 Python 2 和 Python 3？太麻烦了吧。

明哥教你用一种可以兼容 Python 2 和 Python 3 的写法。

首先是在 Python 2 中的输出

```
&gt;&gt;&gt; import codecs 
&gt;&gt;&gt; body="hello\\nworld"
&gt;&gt;&gt; 
&gt;&gt;&gt; codecs.decode(body, 'unicode_escape')
u'hello\nworld'
&gt;&gt;&gt;

```

然后再看看 Python 3 中的输出

```
&gt;&gt;&gt; import codecs
&gt;&gt;&gt; body="hello\\nworld"
&gt;&gt;&gt; 
&gt;&gt;&gt; codecs.decode(body, 'unicode_escape')
'hello\nworld'
&gt;&gt;&gt; 

```

可以看到 Pyhton 2 中的输出 有一个 `u` ，而 Python 3 的输出没有了 `u`，但无论如何 ，他们都取消了转义。

以上，就是我为大家整理的关于 Python 中转义的全部内容了，整理的过程，不断的发现新知识，帮助到大家的同时，自己也对转义的一些内容有了更深的理解。

如果本文对你有些许帮助，不如给明哥 **来个四连** ~ 比心
