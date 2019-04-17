
## 语法
PHP 脚本可以放在文档中的任何位置。</br>
PHP 脚本以 <?php 开始，以 ?> 结束：
```
<?php
// PHP 代码
?>
```
PHP 文件的默认文件扩展名是 ".php"</br>
一个简单的 PHP 文件实例，它可以向浏览器输出文本 "Hello World!"：
```
<!DOCTYPE html> 
<html> 
<body> 

<h1>My first PHP page</h1> 

<?php 
echo "Hello World!"; 
?> 

</body> 
</html>
```

PHP 中的每个代码行都必须以==分号==结束。分号是一种分隔符，用于把指令集区分开来。

通过 PHP，有两种在浏览器输出文本的基础指令：++echo++ 和 ++print++。


## 变量

**PHP 变量规则：**

- 变量以 $ 符号开始，后面跟着变量的名称
- 变量名必须以字母或者下划线字符开始
- 变量名只能包含字母数字字符以及下划线（A-z、0-9 和 _ ）
- 变量名不能包含空格
- 变量名是区分大小写的（$y 和 $Y 是两个不同的变量）
- 

**创建（声明）PHP 变量**
```
<?php
$txt="Hello world!";
$x=5;
$y=10.5;
?>
```

## PHP 变量作用域

PHP 有四种不同的变量作用域：

- local  局部
- global 全局
- static 静态
- parameter 参数

####  局部作用域
在 PHP 函数内部声明的变量是局部变量，仅能在函数内部访问
```
<?php 
$x=5; // 全局变量 

function myTest() 
{ 
    $y=10; // 局部变量 
    echo "<p>测试函数内变量:<p>"; 
    echo "变量 x 为: $x"; 
    echo "<br>"; 
    echo "变量 y 为: $y"; 
}  

myTest(); 

echo "<p>测试函数外变量:<p>"; 
echo "变量 x 为: $x"; 
echo "<br>"; 
echo "变量 y 为: $y"; 
?>
```

#### global 关键字
global 关键字用于函数内访问全局变量。
在函数内调用函数外定义的全局变量，我们需要在函数中的变量前加上 global 关键字：
```
<?php
$x=5;
$y=10;
 
function myTest()
{
    global $x,$y;
    $y=$x+$y;
}
 
myTest();
echo $y; // 输出 15
?>
```