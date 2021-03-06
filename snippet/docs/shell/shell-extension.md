
第六部分 扩展
===========

## 18 大括号扩展

语法                |   含义
-------------------|----------------------------
{str_1, str_2,  …} | 匹配{ }中的任何一个字符串


## 19 波浪线（~）扩展

语法     |           含义
--------|--------------------------------------
~       |  当前用户的工作主目录（$HOME）
~name   |  用户name的工作主目录
~+      |  当前工作目录（pwd）
~-      |  来自目录堆栈的前一个工作目录（OLDPWD）
~+n     |  目录堆栈中的第n条，从表的开始处计数，第一条为0
~-n     |  目录堆栈中的第n条，从表的末尾处计数，最后一条为0


## 20 参数扩展

语法                         |                                    含义
----------------------------|-----------------------------------------------------------
${varname:-word}            |  假如varname存在并且不为null，则返回它的值；否则，返回word。 目的：假如变量没有定义，则返回一个默认值。
${varname:=word}            |  假如varname存在并且不为null，则返回它的值；否则，把word的值赋值给varname， 然后返回它的值。 位置参数不能使用这种方法赋值。 目的：假如变量没有定义，则把它设置为一个默认值。
${varname:?nessage}         |  假如varname存在且不为null，则返回它的值； 否则，输出varname:，紧跟着输出message，并停止当前的命令或脚本 （仅适用于非交互式shell）。 省略message时会产生默认消息”parameter null or not set” 。 目的：捕获由于没有定义变量而引起的错误。
${varname:+word}            |  假如varname存在且不为null，则返回word的值；否则，返回null。 目的：测试一个变量是否存在。
${#varname}                 |  返回varname中字符的个数。目的：为了置换和提取子串做准备。
${variable#pattern}         |  如果pattern与variable值的开始部分匹配的话，则删除匹配的最短部分，并返回剩余的部分。
${variable##pattern}        |  如果pattern与variable值的开始部分匹配的话，则删除匹配的最长部分，并返回剩余的部分。
${variable%pattern}         |  如果pattern与variable值的末尾部分匹配的话，则删除匹配的最短部分，并返回剩余的部分。
${variable%%pattern}        |  如果pattern与variable值的末尾部分匹配的话，则删除匹配的最长部分，并返回剩余的部分。
${var/pat/sub}              |  pat在var中的首次出现用sub替换后，返回var。 应用到$*或$@中时，分开处理每个单词。 假如pat以#开始，则它只能匹配var的开头； 假如pat以%结束，则它只能匹配var的末尾。
${var//pat/sub}             |  pat在var中的每次出现都用sub替换后，返回var。
${variable^pattern}         |  把variable中第一个匹配的pattern中的小写字母转换成大写字母。
${variable^^pattern}        |  把variable在所有匹配的pattern中的小写字母转换成大写字母。
${variable,pattern}         |  把variable中第一个匹配的pattern中的大写字母转换成小写字母。
${variable,,pattern}        |  把variable在所有匹配的pattern中的大写字母转换成小写字母。
${variable:position}        |  提取variable中的子串，该子串从position位置开始直至结尾。
${variable:position:length} |  从variable中提取从position位置开始、长度为length的子串

**说明：**

	每个运算符内的冒号（:）都是可选的。
	如果省略冒号，则将每个含义中的“存在且非null”部分改为“存在”，
	也就是说，运算符仅用于测试变量是否存在，而不测试变量是否为空。

 
## 21 命令替换

命令替换有两种形式：\`cmd\`和 $(cmd)

### 21.1 \`cmd\`（反引号）

**语法：**
```shell
`cmd`
```

**语义：**

	该命令被替换成cmd命令的执行结果

### 21.2 $(cmd)

**语法：**
```shell
$(cmd)
```

**语义：**

	该命令被替换成cmd命令的执行结果

**说明：**

	命令置换可以嵌套。但当使用反引号（`）形式进行嵌套时，应使反斜杠对内层的反引号进行转义。
	如果置换出现在双引号内，单词分割与路径名扩展将不会完成。


## 22 算术扩展

参见“`14 算术扩展`”


## 23 进程替换
待写。


## 24 单词分割
待写。
 

## 25 模式匹配

### 25.1 特殊匹配字符（thespecial pattern character）

语法          |               含义
-------------|------------------------------------
\*           |  匹配0个或多个任意字符
?            |  匹配任何单个字符
[abc......]  |  匹配[ ]中的任何一个字符；可以使用连字符号指定范围（如：a-z，A-Z，0-9）， 但受到本地区域设置的影响。
[!abc......] [^abc......] | 匹配不在[ ]中的任何一个其他字符。
\*(模式表)     | 匹配给定模式表中0次或多次出现的“模式”，模式表中的各模式之间以“|”分隔。
 +(模式表)    | 匹配给定模式表中1次或多次出现的“模式”，模式表中的各模式之间以“|”分隔。
 ?(模式表)    | 匹配给定模式表中0次或1次出现的“模式”，模式表中的各模式之间以“|”分隔。
 @(模式表)    | 仅匹配模式表中给定的“模式”一次，模式表中的各模式之间以“|”分隔。
 !(模式表)    | 除给定模式中的“模式”外，它可以匹配其他任何东西，模式表中的各模式之间认“|”分隔。

注：模式表达式是可以递归的，即每个表达式都可以包含一个或多个模式。
