#  PHP 是一种创建动态交互性站点的强有力的服务器端脚本语言。

PHP 变量规则：

1. 变量以 $ 符号开始，后面跟着变量的名称
2. 变量名必须以字母或者下划线字符开始
3. 变量名只能包含字母数字字符以及下划线（A-z、0-9 和 _ ）
4. 变量名不能包含空格
5. 变量名是区分大小写的（$y 和 $Y 是两个不同的变量）
```php
<?php
echo 'hellp,word!<br>';
$a=5;
$b=5;
echo $a+$b;
?>
```
## PHP 变量作用域
变量的作用域是脚本中变量可被引用/使用的部分。

PHP 有四种不同的变量作用域：

1. local
2. global
3. static
4. parameter

> 你可以在不同函数中使用相同的变量名称，因为这些函数内定义的变量名是局部变量，只作用于该函数内
```php
<?php
$a=5;
function myTest(){
    global $a;
    $b=5;
    echo $a+$b;
}

myTest();

echo $b;
?>
```
## `global`作用域
如果要在一个函数中访问一个全局变量，需要使用 global 关键字
但是如果要将外部调用局部变量，该如何做呢？
```php
<?php
$a=5;
function myTest(){
    global $a,$b;
    $b=5;
    echo $a+$b;
    $a=$a+$b;
}

myTest();

echo $a;
?>
```
很明显并不能，调用不是一个逆方向的方法。上述只是重新给全局变量a了一个新的值
或者`PHP `将所有全局变量存储在一个名为 $GLOBALS[index] 的数组中。 index 保存变量的名称。这个数组可以在函数内部访问，也可以直接用来更新全局变量。
```php
<?php
$a=5;
$b=3;
function mytest(){
    $GLOBALS['b']=$GLOBALS['a']+$GLOBALS['b'];
    $GLOBALS['a']=$GLOBALS['b'];
}

mytest();
echo "$a<br>$b";
?>
```
## Static 作用域
当一个函数完成时，它的所有变量通常都会被删除。然而，有时候您希望某个局部变量不要被删除。
要做到这一点，请在您第一次声明变量时使用 static 关键字，可以通过两个代码来明白
```php
<?php
function mytest(){
    $a=1;
    echo $a;
    echo PHP_EOL;
    $a++;
    echo $a;
}

mytest();
echo PHP_EOL; //此为php中的换行，之前的<br>是用了html的字符串串接
mytest();
?>
```
结果为：
```shell
1
2
1
2
```
```php
<?php
function mytest(){
    static $a=1;
    echo $a;
    echo PHP_EOL;
    $a++;
    echo $a;
}

mytest();
echo PHP_EOL;
mytest();
?>
```
结果为：
```shell
1
2
2
3
```
参数是通过调用代码将值传递给函数的局部变量。
参数是在参数列表中声明的，作为函数声明的一部分：
```php
<?php
function myTest($x)
{
    echo $x;
}
myTest(5);
//myTest($x=5);
?>
```
