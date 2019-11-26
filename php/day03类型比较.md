虽然 PHP 是弱类型语言，但也需要明白变量类型及它们的意义，因为我们经常需要对 PHP 变量进行比较，包含松散和严格比较。
1.松散比较：使用两个等号 == 比较，只比较值，不比较类型。
2.严格比较：用三个等号 === 比较，除了比较值，也比较类型。
```php
<?php
if (41 == "41"){
    echo '11';
}
else{
    echo 22;
}
echo PHP_EOL;
if (41 === "41"){
    echo 11;
}
else {
    echo 22;
}
?>
```
PHP 常量:
1. 常量值被定义后，在脚本的其他任何地方都不能被改变。
2. 常量在定义后，默认是全局变量，可以在整个运行的脚本的任何地方使用
3. 一个常量由英文字母、下划线、和数字组成,但数字不能作为首字母出现。 (常量名不需要加 $ 修饰符)。
4. `define()`用法为 `bool define ( string $name , mixed $value [, bool $case_insensitive = false ] )`
> name：必选参数，常量名称，即标志符。
value：必选参数，常量的值。
case_insensitive ：可选参数，如果设置为 TRUE，该常量则大小写不敏感。默认是大小写敏感的。
```php
<?php
define("GG","快乐",true);
echo Gg;
?>
```
或者
```php
<?php
define("GG","快乐");
echo GG;
?>
```
